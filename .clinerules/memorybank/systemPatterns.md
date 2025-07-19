# System Patterns

This document outlines the system architecture, key technical decisions, and design patterns for the Health Tracker project, now updated to reflect iDesign architectural principles and the latest documentation.

## System Architecture
- The system is a full-stack web application with a clear separation between backend and frontend.
- Backend API is built with .NET, exposing RESTful endpoints for data management and authentication.
- Frontend is a React-based single-page application consuming the backend API.
- The architecture follows iDesign principles, emphasizing separation of concerns, strict dependency direction, and maintainability.

### iDesign 3-Layer Hierarchical Structure

| Layer           | Description              | Responsibilities                                                     |
| --------------- | ------------------------ | -------------------------------------------------------------------- |
| Managers        | Orchestration Layer      | Entry points, use case orchestration, business workflow coordination |
| Engines         | Business Logic Layer     | Complex operations, business rules, domain-specific algorithms       |
| Data Access     | Infrastructure Layer     | I/O operations, database access, external service integration        |
| Models          | Data Structures          | DTOs, entities, value objects, enums, contracts                      |

#### Dependency Rules
- Managers depend on Engines, Data Access, Models
- Engines depend on Data Access, Models (never Managers)
- Data Access depends on Models (never Managers or Engines)
- Models are self-contained

## Key Technical Decisions
- Use of RESTful API design to ensure scalability and maintainability.
- Secure authentication mechanisms implemented in the backend.
- Modular React components for frontend to promote reusability and ease of maintenance.
- Data models designed to support nutrition, exercise, and health metrics tracking.
- Strict adherence to iDesign dependency rules for testability and scalability.

## Design Patterns
- Repository pattern for data access in the backend.
- Dependency injection for service management in the backend.
- Component-based architecture in React frontend.
- State management using React hooks and context where appropriate.
- Interface segregation and dependency inversion for maintainable code.

## Testing Strategy

- 100% unit test coverage for business logic (Engines layer)
- Layer-specific testing using mocks/stubs
- API endpoint integration tests for controllers
- End-to-end tests for user journeys from UI to database
- Visual regression testing for frontend using Playwright
- Performance and security gates in CI/CD

## Component Relationships
- Backend controllers (Managers) handle API requests and orchestrate business workflows.
- Engines encapsulate business logic and rules.
- Data Access layer manages persistence and external integrations.
- Frontend components interact with backend API via dedicated API service modules.
- Authentication flow managed through dedicated auth components and API endpoints.

## Critical Implementation Paths
- User authentication and authorization.
- Data logging and retrieval for health metrics.
- Responsive UI rendering and state synchronization.
- Automated testing and CI/CD integration.
