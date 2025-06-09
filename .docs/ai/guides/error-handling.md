# Error Handling & Recovery Guidelines

This document provides comprehensive guidelines for handling errors and recovering from failures during development and in production. These patterns ensure that the system is robust, maintainable, and provides a good user experience even when things go wrong.

## Error Handling Principles

### 1. Fail Fast, Fail Safely
- Detect errors as early as possible in the execution flow
- Validate inputs at system boundaries
- Use assertions and preconditions for internal consistency checks
- When failure occurs, preserve system state and avoid corruption

### 2. Error Categorization
Categorize errors into distinct types to handle them appropriately:

- **Expected Business Errors**: Normal business rule violations (e.g., insufficient funds)
- **Validation Errors**: Invalid input or state
- **External System Failures**: Dependency failures (database, services)
- **Transient Failures**: Temporary glitches that may self-resolve
- **System Errors**: Unexpected internal errors
- **Configuration Errors**: Incorrect system setup

### 3. Appropriate Response by Error Type

| Error Type | User Experience | Logging | Retry | Example Handling |
|------------|----------------|---------|-------|------------------|
| Business Rule | Clear message explaining rule violation | Info level | No | Return validation response with details |
| Validation | Display specific fields with issues | Info level | No | Return 400 Bad Request with field errors |
| External System | Generic message, retry option | Warning level | Yes | Implement retry with exponential backoff |
| Transient | Automatic retry, spinner | Warning level | Yes | Circuit breaker pattern |
| System Error | Apologize, alternative contact | Error level | No | Return 500, alert ops team |
| Configuration | Maintenance message | Critical level | No | Fail startup, alert ops team |

## Implementation Patterns

### Backend (C#/.NET)

#### Exception Handling
```csharp
// Global exception handling middleware
public class GlobalExceptionHandlerMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<GlobalExceptionHandlerMiddleware> _logger;

    public GlobalExceptionHandlerMiddleware(RequestDelegate next, ILogger<GlobalExceptionHandlerMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (BusinessRuleException ex)
        {
            _logger.LogInformation(ex, "Business rule violation");
            context.Response.StatusCode = StatusCodes.Status400BadRequest;
            await WriteResponseAsync(context, new ErrorResponse 
            { 
                Code = "BUSINESS_RULE_VIOLATION", 
                Message = ex.Message, 
                Details = ex.Details 
            });
        }
        catch (ValidationException ex)
        {
            _logger.LogInformation(ex, "Validation error");
            context.Response.StatusCode = StatusCodes.Status400BadRequest;
            await WriteResponseAsync(context, new ErrorResponse
            {
                Code = "VALIDATION_ERROR",
                Message = "One or more validation errors occurred.",
                Errors = ex.Errors
            });
        }
        catch (ExternalSystemException ex) when (ex.IsTransient)
        {
            _logger.LogWarning(ex, "Transient external system error");
            context.Response.StatusCode = StatusCodes.Status503ServiceUnavailable;
            context.Response.Headers.Add("Retry-After", "30");
            await WriteResponseAsync(context, new ErrorResponse 
            { 
                Code = "TEMPORARY_ERROR", 
                Message = "Service temporarily unavailable. Please retry later." 
            });
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "Unhandled exception");
            context.Response.StatusCode = StatusCodes.Status500InternalServerError;
            await WriteResponseAsync(context, new ErrorResponse 
            { 
                Code = "SERVER_ERROR", 
                Message = "An unexpected error occurred. Please contact support." 
            });
        }
    }

    private static Task WriteResponseAsync(HttpContext context, ErrorResponse response)
    {
        context.Response.ContentType = "application/json";
        return context.Response.WriteAsync(JsonSerializer.Serialize(response, new JsonSerializerOptions
        {
            PropertyNamingPolicy = JsonNamingPolicy.CamelCase
        }));
    }
}
```

#### Custom Exception Types
```csharp
// Base exception for all application-specific exceptions
public abstract class ApplicationException : Exception
{
    protected ApplicationException(string message) : base(message) { }
    protected ApplicationException(string message, Exception innerException) : base(message, innerException) { }
}

// Business rule violations
public class BusinessRuleException : ApplicationException
{
    public object Details { get; }
    
    public BusinessRuleException(string message, object details = null) : base(message)
    {
        Details = details;
    }
}

// Validation errors
public class ValidationException : ApplicationException
{
    public IDictionary<string, string[]> Errors { get; }
    
    public ValidationException(IDictionary<string, string[]> errors) 
        : base("One or more validation errors occurred.")
    {
        Errors = errors;
    }
}

// External system failures
public class ExternalSystemException : ApplicationException
{
    public bool IsTransient { get; }
    public string ServiceName { get; }
    
    public ExternalSystemException(string message, string serviceName, bool isTransient = false) 
        : base(message)
    {
        ServiceName = serviceName;
        IsTransient = isTransient;
    }
}
```

#### Retry Patterns
```csharp
// Retry utility
public static class RetryHelper
{
    public static async Task<T> RetryAsync<T>(
        Func<Task<T>> operation, 
        int maxRetries = 3,
        int initialDelayMs = 100,
        double backoffFactor = 2.0,
        CancellationToken cancellationToken = default)
    {
        int retryCount = 0;
        int delay = initialDelayMs;
        
        while (true)
        {
            try
            {
                return await operation();
            }
            catch (Exception ex) when (ShouldRetry(ex) && retryCount < maxRetries)
            {
                // Log retry attempt
                retryCount++;
                if (retryCount >= maxRetries) throw;
                
                // Wait with exponential backoff
                await Task.Delay(delay, cancellationToken);
                delay = (int)(delay * backoffFactor);
            }
        }
    }
    
    private static bool ShouldRetry(Exception ex)
    {
        // Determine which exceptions should trigger retries
        return ex is ExternalSystemException { IsTransient = true } ||
               ex is HttpRequestException ||
               ex is TimeoutException ||
               ex is IOException;
    }
}
```

#### Circuit Breaker
```csharp
// Basic circuit breaker implementation
public class CircuitBreaker
{
    private readonly int _threshold;
    private readonly TimeSpan _resetTimeout;
    private int _failureCount;
    private DateTime? _lastFailureTime;
    private bool _isOpen;

    public CircuitBreaker(int threshold = 5, TimeSpan? resetTimeout = null)
    {
        _threshold = threshold;
        _resetTimeout = resetTimeout ?? TimeSpan.FromMinutes(1);
    }

    public async Task<T> ExecuteAsync<T>(Func<Task<T>> operation)
    {
        if (_isOpen)
        {
            // Check if timeout has elapsed to try again
            if (_lastFailureTime.HasValue && 
                DateTime.UtcNow - _lastFailureTime.Value > _resetTimeout)
            {
                // Allow a single trial call through
                _isOpen = false;
            }
            else
            {
                throw new CircuitBreakerOpenException("Circuit breaker is open");
            }
        }

        try
        {
            T result = await operation();
            
            // Success resets the failure count
            ResetFailureCount();
            
            return result;
        }
        catch (Exception ex)
        {
            // Record the failure
            _failureCount++;
            _lastFailureTime = DateTime.UtcNow;
            
            // Open circuit if threshold reached
            if (_failureCount >= _threshold)
            {
                _isOpen = true;
            }
            
            throw;
        }
    }
    
    private void ResetFailureCount()
    {
        _failureCount = 0;
        _lastFailureTime = null;
        _isOpen = false;
    }
}

public class CircuitBreakerOpenException : Exception
{
    public CircuitBreakerOpenException(string message) : base(message) { }
}
```

### Frontend (React/TypeScript)

#### API Error Handling
```typescript
// Error types
export interface ApiError {
  code: string;
  message: string;
  errors?: Record<string, string[]>;
  details?: unknown;
}

// API client with error handling
export class ApiClient {
  private baseUrl: string;
  
  constructor(baseUrl: string) {
    this.baseUrl = baseUrl;
  }
  
  async get<T>(endpoint: string): Promise<T> {
    return this.request<T>('GET', endpoint);
  }
  
  async post<T>(endpoint: string, data: unknown): Promise<T> {
    return this.request<T>('POST', endpoint, data);
  }
  
  // Additional methods (put, delete, etc.)
  
  private async request<T>(method: string, endpoint: string, data?: unknown): Promise<T> {
    try {
      const response = await fetch(`${this.baseUrl}${endpoint}`, {
        method,
        headers: {
          'Content-Type': 'application/json',
          'Accept': 'application/json',
          'Authorization': `Bearer ${this.getToken()}`
        },
        body: data ? JSON.stringify(data) : undefined
      });
      
      // Handle different response types
      const contentType = response.headers.get('content-type');
      const isJson = contentType?.includes('application/json');
      
      if (!response.ok) {
        if (isJson) {
          const errorData: ApiError = await response.json();
          throw new ApiRequestError(
            response.status,
            errorData.code || 'UNKNOWN_ERROR',
            errorData.message || 'An unknown error occurred',
            errorData.errors,
            errorData.details
          );
        } else {
          throw new ApiRequestError(
            response.status,
            'HTTP_ERROR',
            response.statusText || 'An error occurred'
          );
        }
      }
      
      // Return response data or empty object for no-content responses
      return isJson ? await response.json() : {} as T;
    } catch (error) {
      // Network errors or other fetch failures
      if (!(error instanceof ApiRequestError)) {
        throw new ApiRequestError(
          0, 
          'NETWORK_ERROR',
          error instanceof Error ? error.message : 'Network error'
        );
      }
      throw error;
    }
  }
  
  private getToken(): string {
    // Get authentication token from storage
    return localStorage.getItem('auth_token') || '';
  }
}

// Custom error class
export class ApiRequestError extends Error {
  public statusCode: number;
  public code: string;
  public validationErrors?: Record<string, string[]>;
  public details?: unknown;
  
  constructor(
    statusCode: number,
    code: string,
    message: string,
    validationErrors?: Record<string, string[]>,
    details?: unknown
  ) {
    super(message);
    this.statusCode = statusCode;
    this.code = code;
    this.validationErrors = validationErrors;
    this.details = details;
    this.name = 'ApiRequestError';
    
    // Ensure proper prototype chain for instanceof checks
    Object.setPrototypeOf(this, ApiRequestError.prototype);
  }
  
  isValidationError(): boolean {
    return this.statusCode === 400 && !!this.validationErrors;
  }
  
  isAuthError(): boolean {
    return this.statusCode === 401 || this.statusCode === 403;
  }
  
  isNotFoundError(): boolean {
    return this.statusCode === 404;
  }
  
  isServerError(): boolean {
    return this.statusCode >= 500;
  }
}
```

#### React Error Boundary
```tsx
// Error boundary component
import React, { Component, ErrorInfo, ReactNode } from 'react';

interface ErrorBoundaryProps {
  fallback?: ReactNode | ((error: Error, resetError: () => void) => ReactNode);
  children: ReactNode;
  onError?: (error: Error, errorInfo: ErrorInfo) => void;
}

interface ErrorBoundaryState {
  hasError: boolean;
  error: Error | null;
}

export class ErrorBoundary extends Component<ErrorBoundaryProps, ErrorBoundaryState> {
  constructor(props: ErrorBoundaryProps) {
    super(props);
    this.state = {
      hasError: false,
      error: null
    };
  }

  static getDerivedStateFromError(error: Error): ErrorBoundaryState {
    return {
      hasError: true,
      error
    };
  }

  componentDidCatch(error: Error, errorInfo: ErrorInfo): void {
    // Log the error
    console.error('React Error Boundary caught an error:', error, errorInfo);
    
    // Call the onError callback if provided
    if (this.props.onError) {
      this.props.onError(error, errorInfo);
    }
  }
  
  resetError = (): void => {
    this.setState({
      hasError: false,
      error: null
    });
  }

  render(): ReactNode {
    if (this.state.hasError) {
      // Use the provided fallback if available
      if (this.props.fallback) {
        if (typeof this.props.fallback === 'function') {
          return this.props.fallback(this.state.error!, this.resetError);
        }
        return this.props.fallback;
      }
      
      // Default error UI
      return (
        <div className="error-boundary">
          <h2>Something went wrong.</h2>
          <p>{this.state.error?.message}</p>
          <button onClick={this.resetError}>Try Again</button>
        </div>
      );
    }

    return this.props.children;
  }
}
```

#### Error Toast Notifications
```tsx
// Toast notification for errors
import React, { createContext, useContext, useState, ReactNode } from 'react';
import { ApiRequestError } from './api-client';

interface Toast {
  id: string;
  type: 'success' | 'error' | 'warning' | 'info';
  message: string;
  details?: string;
}

interface ToastContextValue {
  toasts: Toast[];
  addToast: (toast: Omit<Toast, 'id'>) => void;
  removeToast: (id: string) => void;
  showErrorToast: (error: Error | string) => void;
}

const ToastContext = createContext<ToastContextValue | undefined>(undefined);

export const ToastProvider: React.FC<{ children: ReactNode }> = ({ children }) => {
  const [toasts, setToasts] = useState<Toast[]>([]);
  
  const addToast = (toast: Omit<Toast, 'id'>) => {
    const id = Math.random().toString(36).substring(2, 9);
    setToasts((prevToasts) => [...prevToasts, { ...toast, id }]);
    
    // Auto-remove toast after timeout
    setTimeout(() => {
      removeToast(id);
    }, 5000);
  };
  
  const removeToast = (id: string) => {
    setToasts((prevToasts) => prevToasts.filter(toast => toast.id !== id));
  };
  
  const showErrorToast = (error: Error | string) => {
    if (typeof error === 'string') {
      addToast({
        type: 'error',
        message: error
      });
      return;
    }
    
    // Handle API errors specially
    if (error instanceof ApiRequestError) {
      const message = getErrorMessage(error);
      const details = error.isValidationError() 
        ? Object.entries(error.validationErrors || {})
            .map(([field, errors]) => `${field}: ${errors.join(', ')}`)
            .join('\n')
        : undefined;
      
      addToast({
        type: 'error',
        message,
        details
      });
      return;
    }
    
    // Generic errors
    addToast({
      type: 'error',
      message: error.message || 'An unexpected error occurred'
    });
  };
  
  return (
    <ToastContext.Provider value={{ toasts, addToast, removeToast, showErrorToast }}>
      {children}
      <ToastContainer />
    </ToastContext.Provider>
  );
};

const getErrorMessage = (error: ApiRequestError): string => {
  if (error.isValidationError()) {
    return 'Please check the form for errors';
  }
  
  if (error.isAuthError()) {
    return error.statusCode === 401 
      ? 'Your session has expired. Please log in again.' 
      : 'You don\'t have permission to perform this action.';
  }
  
  if (error.isNotFoundError()) {
    return 'The requested resource was not found.';
  }
  
  if (error.isServerError()) {
    return 'The server encountered an error. Please try again later.';
  }
  
  return error.message || 'An unexpected error occurred';
};

export const useToast = () => {
  const context = useContext(ToastContext);
  if (context === undefined) {
    throw new Error('useToast must be used within a ToastProvider');
  }
  return context;
};

// Toast container component
const ToastContainer = () => {
  const { toasts, removeToast } = useToast();
  
  return (
    <div className="toast-container">
      {toasts.map(toast => (
        <div key={toast.id} className={`toast toast-${toast.type}`}>
          <div className="toast-header">
            <strong>{toast.type.toUpperCase()}</strong>
            <button onClick={() => removeToast(toast.id)}>×</button>
          </div>
          <div className="toast-body">
            <p>{toast.message}</p>
            {toast.details && (
              <details>
                <summary>Details</summary>
                <pre>{toast.details}</pre>
              </details>
            )}
          </div>
        </div>
      ))}
    </div>
  );
};
```

## Error Recovery Strategies

### Database Transactions
- Use transactions for multi-step operations that must succeed or fail as a unit
- Implement compensating transactions when needed for distributed operations
- Keep transactions short-lived to avoid blocking resources

### Saga Pattern for Distributed Transactions
- Break long-running processes into a series of local transactions
- Implement compensating actions that can undo each step if a later step fails
- Track transaction state in a durable store

### Data Validation
- Validate early and often (client-side, API boundary, business layer)
- Use strong typing and schemas (JSON Schema, TypeScript, etc.)
- Implement cross-field validation rules as needed
- Return all validation errors at once when possible

### Fault Isolation
- Use bulkheads to prevent failures in one component from affecting others
- Implement timeouts for external calls
- Use circuit breakers to fail fast when dependencies are unhealthy

### Graceful Degradation
- Design components that can operate with reduced functionality
- Implement fallbacks for critical features
- Prioritize core business functionality during partial outages

### Monitoring & Recovery
- Log all errors with context (user, action, stack trace)
- Set up alerting for critical errors and error rate spikes
- Implement health checks and readiness probes
- Use automated recovery where safe (auto-restart, scale up)

### Testing Error Scenarios
- Write unit tests that verify error handling logic
- Implement chaos testing to simulate failures
- Test circuit breakers and retry logic

## User Experience During Errors

### Error Message Guidelines
- Use plain language, avoid technical jargon
- Be specific about what went wrong
- Suggest next steps or solutions when possible
- Maintain brand voice (friendly, helpful)

### Form Error Handling
- Show field-level errors next to the relevant input
- Provide a summary of all errors at form level
- Use appropriate visual cues (color, icons)
- Support both server-side and client-side validation

### Critical Error Recovery
- Provide clear path to recover from session timeouts
- Allow for data recovery when possible (save drafts)
- Give users contact options for critical failures
- Consider compensation for service disruptions
