[<< Back](./../design.md)

# Error Handling Sequence Diagrams
This document provides sequence diagrams specifically for error handling flows. It shows how errors are propagated through the system layers and how recovery mechanisms work.

## Common Error Handling Flows

### HTTP API Error Handling Flow
```mermaid
sequenceDiagram
    participant C as Client
    participant API as API Controller
    participant G as Global Exception Handler
    participant M as Manager (Green)
    participant E as Engine (Orange)
    participant D as Data Access (Grey)
    participant DB as Database
    participant Log as Logger

    C->>API: HTTP Request
    activate API
    
    API->>M: Process Request
    activate M
    
    M->>E: Execute Business Logic
    activate E
    
    E->>D: Access Data
    activate D
    
    D->>DB: Execute Query
    activate DB
    
    alt Database Error
        DB-->>D: Throws SQLException
        deactivate DB
        
        D->>Log: Log Error (Warning)
        D-->>E: Throw DataAccessException
        deactivate D
        
        E->>Log: Log Error (Error)
        E-->>M: Propagate Exception
        deactivate E
        
        M-->>API: Propagate Exception
        deactivate M
        
        API->>G: Handle Exception
        activate G
        
        G->>Log: Log Error (Error)
        G-->>C: Return 503 Service Unavailable
        deactivate G
        deactivate API
        
    else Business Rule Violation
        DB-->>D: Return Data
        deactivate DB
        
        D-->>E: Return Data
        deactivate D
        
        E->>E: Business Rule Check Failed
        E->>Log: Log Business Violation (Info)
        E-->>M: Throw BusinessRuleException
        deactivate E
        
        M-->>API: Propagate Exception
        deactivate M
        
        API->>G: Handle Exception
        activate G
        
        G->>Log: Log Business Error (Info)
        G-->>C: Return 400 Bad Request with Details
        deactivate G
        deactivate API
        
    else Unexpected Error
        DB-->>D: Return Data
        deactivate DB
        
        D-->>E: Return Data
        deactivate D
        
        E->>E: Unexpected Error Occurs
        E->>Log: Log Critical Error
        E-->>M: Throw Exception
        deactivate E
        
        M-->>API: Propagate Exception
        deactivate M
        
        API->>G: Handle Exception
        activate G
        
        G->>Log: Log Error (Critical)
        G-->>C: Return 500 Internal Server Error
        deactivate G
        deactivate API
    end
```

### Retry Pattern Flow
```mermaid
sequenceDiagram
    participant C as Client
    participant API as API Controller
    participant M as Manager (Green)
    participant E as Engine (Orange)
    participant R as Retry Handler
    participant D as Data Access (Grey)
    participant ES as External Service
    participant Log as Logger

    C->>API: HTTP Request
    activate API
    
    API->>M: Process Request
    activate M
    
    M->>E: Execute Business Logic
    activate E
    
    E->>R: Execute with Retry
    activate R
    
    loop Retry Logic (max 3 attempts)
        R->>D: Perform Operation
        activate D
        
        D->>ES: Call External Service
        activate ES
        
        alt Successful Response
            ES-->>D: Return Data
            deactivate ES
            
            D-->>R: Operation Succeeded
            deactivate D
            
            R-->>E: Return Result
            deactivate R
            
            E-->>M: Return Result
            deactivate E
            
            M-->>API: Return Result
            deactivate M
            
            API-->>C: Return Success Response
            deactivate API
            
        else Transient Error (Attempt < Max)
            ES--xD: Throws Transient Error
            deactivate ES
            
            D->>Log: Log Retry Attempt
            D-->>R: Throw Transient Exception
            deactivate D
            
            R->>R: Wait (Exponential Backoff)
            R->>Log: Log Retry Attempt
            note over R: Retry with backoff
        end
    end
    
    alt Max Retries Exceeded
        R->>Log: Log Retry Exhausted
        R-->>E: Throw RetryExhaustedException
        deactivate R
        
        E->>Log: Log Service Unavailable
        E-->>M: Propagate Exception
        deactivate E
        
        M-->>API: Propagate Exception
        deactivate M
        
        API-->>C: Return 503 Service Unavailable
        deactivate API
    end
```

### Circuit Breaker Pattern Flow
```mermaid
sequenceDiagram
    participant C as Client
    participant API as API Controller
    participant M as Manager (Green)
    participant E as Engine (Orange)
    participant CB as Circuit Breaker
    participant D as Data Access (Grey)
    participant ES as External Service
    participant Log as Logger

    C->>API: HTTP Request
    API->>M: Process Request
    M->>E: Execute Business Logic
    
    alt Circuit Open (Previous Failures)
        E->>CB: Execute Operation
        CB--xE: Circuit Open Exception
        E->>Log: Log Circuit Open
        E->>E: Use Fallback Strategy
        E-->>M: Return Fallback Result
        M-->>API: Return Result
        API-->>C: Return Degraded Response
        
    else Circuit Closed (Normal Operation)
        E->>CB: Execute Operation
        CB->>D: Perform Operation
        D->>ES: Call External Service
        
        alt Successful Call
            ES-->>D: Return Data
            D-->>CB: Operation Succeeded
            CB->>CB: Reset Failure Count
            CB-->>E: Return Result
            E-->>M: Return Result
            M-->>API: Return Result
            API-->>C: Return Success Response
            
        else Service Failure
            ES--xD: Service Error
            D-->>CB: Operation Failed
            CB->>CB: Increment Failure Count
            CB->>Log: Log Failure
            
            alt Failure Threshold Reached
                CB->>CB: Open Circuit
                CB->>Log: Log Circuit Opened
            end
            
            CB--xE: Propagate Error
            E->>E: Use Fallback Strategy
            E-->>M: Return Fallback Result
            M-->>API: Return Result
            API-->>C: Return Degraded Response
        end
        
    else Circuit Half-Open (Testing Recovery)
        E->>CB: Execute Operation
        CB->>D: Perform Test Operation
        D->>ES: Call External Service
        
        alt Service Recovered
            ES-->>D: Return Data
            D-->>CB: Operation Succeeded
            CB->>CB: Close Circuit
            CB->>Log: Log Circuit Closed
            CB-->>E: Return Result
            E-->>M: Return Result
            M-->>API: Return Result
            API-->>C: Return Success Response
            
        else Service Still Failed
            ES--xD: Service Error
            D-->>CB: Operation Failed
            CB->>CB: Keep Circuit Open
            CB->>Log: Log Recovery Failed
            CB--xE: Propagate Error
            E->>E: Use Fallback Strategy
            E-->>M: Return Fallback Result
            M-->>API: Return Result
            API-->>C: Return Degraded Response
        end
    end
```

### Fallback Pattern Flow
```mermaid
sequenceDiagram
    participant C as Client
    participant API as API Controller
    participant M as Manager (Green)
    participant E as Engine (Orange)
    participant PC as Primary Component
    participant FC as Fallback Component
    participant Log as Logger

    C->>API: HTTP Request
    API->>M: Process Request
    M->>E: Execute Business Logic
    
    E->>PC: Execute Primary Strategy
    
    alt Primary Succeeds
        PC-->>E: Return Result
        E-->>M: Return Result
        M-->>API: Return Result
        API-->>C: Return Success Response
        
    else Primary Fails
        PC--xE: Throws Exception
        E->>Log: Log Primary Failure
        
        E->>FC: Execute Fallback Strategy
        
        alt Fallback Succeeds
            FC-->>E: Return Fallback Result
            E->>Log: Log Using Fallback
            E-->>M: Return Result (Degraded)
            M-->>API: Return Result
            API-->>C: Return Success Response (with fallback data)
            
        else Fallback Fails
            FC--xE: Throws Exception
            E->>Log: Log Complete Failure
            E-->>M: Propagate Exception
            M-->>API: Propagate Exception
            API-->>C: Return Error Response
        end
    end
```

### Bulkhead Pattern Flow
```mermaid
sequenceDiagram
    participant C1 as Client 1
    participant C2 as Client 2
    participant API as API Gateway
    participant BH as Bulkhead
    participant S1 as Service 1
    participant S2 as Service 2
    participant Log as Logger

    C1->>API: Request to Service 1
    API->>BH: Route to Service 1
    
    alt Service 1 Available (Under Threshold)
        BH->>S1: Forward Request
        S1-->>BH: Return Response
        BH-->>API: Return Response
        API-->>C1: Return Success Response
        
    else Service 1 Overloaded
        BH->>Log: Log Rejection (Capacity)
        BH-->>API: Reject Request (429 Too Many Requests)
        API-->>C1: Return 429 Response
    end
    
    C2->>API: Request to Service 2
    API->>BH: Route to Service 2
    
    note over BH,S2: Service 2 operates normally even if Service 1 is overloaded
    
    BH->>S2: Forward Request
    S2-->>BH: Return Response
    BH-->>API: Return Response
    API-->>C2: Return Success Response
```

### Timeout Pattern Flow
```mermaid
sequenceDiagram
    participant C as Client
    participant API as API Controller
    participant M as Manager (Green)
    participant E as Engine (Orange)
    participant TH as Timeout Handler
    participant D as Data Access (Grey)
    participant ES as External Service
    participant Log as Logger

    C->>API: HTTP Request
    activate API
    
    API->>M: Process Request
    activate M
    
    M->>E: Execute Business Logic
    activate E
    
    E->>TH: Execute with Timeout
    activate TH
    
    TH->>D: Perform Operation with Deadline
    activate D
    
    D->>ES: Call External Service
    activate ES
    
    alt Response Within Timeout
        ES-->>D: Return Data
        deactivate ES
        
        D-->>TH: Operation Completed
        deactivate D
        
        TH-->>E: Return Result
        deactivate TH
        
        E-->>M: Return Result
        deactivate E
        
        M-->>API: Return Result
        deactivate M
        
        API-->>C: Return Success Response
        deactivate API
        
    else Timeout Occurred
        note over ES: Still processing...
        
        TH->>Log: Log Timeout
        TH-->>E: Throw TimeoutException
        deactivate D
        deactivate TH
        
        E->>Log: Log Service Timeout
        E-->>M: Propagate Exception
        deactivate E
        
        M-->>API: Propagate Exception
        deactivate M
        
        API-->>C: Return 504 Gateway Timeout
        deactivate API
        
        note over ES: Eventually completes or abandons task
        deactivate ES
    end
```

## Transaction Management Flows

### Distributed Saga Pattern Flow
```mermaid
sequenceDiagram
    participant C as Client
    participant API as API Gateway
    participant O as Orchestrator
    participant S1 as Service 1
    participant S2 as Service 2
    participant S3 as Service 3
    participant DB as Saga State DB
    participant Log as Logger

    C->>API: Request Multi-Step Operation
    API->>O: Begin Saga
    
    O->>DB: Record Saga Started
    O->>S1: Step 1
    
    alt Step 1 Succeeds
        S1-->>O: Step 1 Complete
        O->>DB: Record Step 1 Complete
        O->>S2: Step 2
        
        alt Step 2 Succeeds
            S2-->>O: Step 2 Complete
            O->>DB: Record Step 2 Complete
            O->>S3: Step 3
            
            alt Step 3 Succeeds
                S3-->>O: Step 3 Complete
                O->>DB: Record Saga Complete
                O-->>API: Saga Complete
                API-->>C: Operation Complete
                
            else Step 3 Fails
                S3--xO: Step 3 Failed
                O->>Log: Log Failure
                O->>DB: Record Step 3 Failed
                
                note over O: Begin Compensation
                O->>S2: Compensate Step 2
                S2-->>O: Step 2 Compensated
                O->>S1: Compensate Step 1
                S1-->>O: Step 1 Compensated
                O->>DB: Record Saga Compensated
                
                O-->>API: Saga Failed (Rolled Back)
                API-->>C: Operation Failed
            end
            
        else Step 2 Fails
            S2--xO: Step 2 Failed
            O->>Log: Log Failure
            O->>DB: Record Step 2 Failed
            
            note over O: Begin Compensation
            O->>S1: Compensate Step 1
            S1-->>O: Step 1 Compensated
            O->>DB: Record Saga Compensated
            
            O-->>API: Saga Failed (Rolled Back)
            API-->>C: Operation Failed
        end
        
    else Step 1 Fails
        S1--xO: Step 1 Failed
        O->>Log: Log Failure
        O->>DB: Record Step 1 Failed
        O->>DB: Record Saga Failed
        
        O-->>API: Saga Failed
        API-->>C: Operation Failed
    end
```

## Frontend Error Handling Flows

### API Error Handling in React
```mermaid
sequenceDiagram
    participant U as User
    participant C as React Component
    participant EB as Error Boundary
    participant H as API Hook
    participant A as API Client
    participant BE as Backend API
    participant TS as Toast Service
    
    U->>C: Interact (e.g., Submit Form)
    activate C
    
    C->>H: Call API Operation
    activate H
    
    H->>A: Execute API Call
    activate A
    
    A->>BE: HTTP Request
    activate BE
    
    alt Success Response
        BE-->>A: 200 OK with Data
        deactivate BE
        
        A-->>H: Return Data
        deactivate A
        
        H-->>C: Return Data
        deactivate H
        
        C->>C: Update UI with Data
        C-->>U: Show Success State
        deactivate C
        
    else Validation Error
        BE-->>A: 400 Bad Request
        deactivate BE
        
        A->>A: Parse Validation Errors
        A-->>H: Throw ApiRequestError
        deactivate A
        
        H->>H: Map to Form Errors
        H-->>C: Return Field Errors
        deactivate H
        
        C->>C: Display Field Errors
        C-->>U: Show Validation Issues
        deactivate C
        
    else Authentication Error
        BE-->>A: 401 Unauthorized
        deactivate BE
        
        A-->>H: Throw AuthError
        deactivate A
        
        H->>TS: Show Auth Error Toast
        H-->>C: Return Auth Error
        deactivate H
        
        C->>C: Redirect to Login
        C-->>U: Show Login Required
        deactivate C
        
    else Server Error
        BE-->>A: 500 Server Error
        deactivate BE
        
        A-->>H: Throw ServerError
        deactivate A
        
        H->>TS: Show Error Toast
        H-->>C: Return Error
        deactivate H
        
        C->>C: Show Error State
        C-->>U: Display Friendly Error
        deactivate C
        
    else Network Error
        A--xBE: Connection Failed
        A-->>H: Throw NetworkError
        deactivate A
        
        H->>TS: Show Network Error Toast
        H-->>C: Return Network Error
        deactivate H
        
        C->>C: Show Offline State
        C-->>U: Display Connection Issue
        deactivate C
    end
    
    alt Component Error (Uncaught)
        C->>C: Unexpected Error
        C--xEB: Propagate Error
        activate EB
        
        EB->>EB: Capture Error
        EB->>TS: Show Error Notification
        EB-->>U: Show Fallback UI
        deactivate EB
    end
```

[<< Back](./../design.md)
