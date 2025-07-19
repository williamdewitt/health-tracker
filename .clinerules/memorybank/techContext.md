# Tech Context

This document outlines the technologies, development setup, technical constraints, and infrastructure for the Health Tracker project.

## Technologies Used
- Backend: .NET (C#) for API development.
- Frontend: React with TypeScript for building the user interface.
- Database: (Not explicitly stated, but likely used in backend for data persistence).
- API Communication: RESTful API design.

## Development Setup
- Backend and frontend are separated into distinct directories.
- Backend uses .NET project structure with controllers, models, and data context.
- Frontend uses React with modular components and API service modules.
- Docker is used for containerization (Dockerfile present in both backend and frontend).
- docker-compose.yml at the repo root orchestrates multi-service local development.
- Automated Docker Hub builds are supported for deployment.
- Development environment supports hot reloading and debugging.

## Repository Structure
- Documentation and system designs are centralized in the .docs directory.
- Source code and tests are organized under /src, with backend and frontend subdirectories.
- .github contains AI prompts, state tracking, and CI/CD workflows.
- .vscode provides workspace settings and recommended extensions.
- README.md links to all major documentation and guides.

## Docker Support
- Local development: Run `docker-compose up` in the repo root to start all services.
- Docker Hub: Automated builds and public images are available.
- Example compose and Dockerfile templates are provided in .docs/docker-support.md.
- Windows users must ensure Docker is set to Linux containers.

## Technical Constraints
- Security and privacy are prioritized, especially in authentication and data handling.
- The system must be extensible to support future health tracking features.
- Performance considerations for responsive UI and efficient API communication.
- Codebase must be maintainable and well-documented.

## Dependencies
- Backend dependencies managed via .NET project files.
- Frontend dependencies managed via npm (package.json present).

## Tool Usage Patterns
- Use of RESTful API calls from frontend to backend.
- React hooks and context for state management.
- Dependency injection in backend services.
