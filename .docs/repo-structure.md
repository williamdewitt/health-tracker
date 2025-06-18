[<< Back](../README.md)

## Repo Structure

This document describes the desired repository structure. This may be used for AI coding when scaffolding the solution from scratch, for example.

### Structure

- ROOT (The repository root)
  - /.ai (AI coding framework files - initialization and core intelligence)
    - init.md (Main AI prompt and instructions)
  - /.github (GitHub-related content and AI state management)
    - /state (AI session and project state tracking)
      - plan.md (Generated project plan and milestones)
      - session-state.md (Current session progress tracking)
    - /workflows (GitHub action workflows)
      - <WORKFLOW_NAME>\_workflow.yml (Singular GitHub action)
  - /.docs (The collection of repository documents and system designs etc. This directory should be documented in [README.md](../README.md) too.)
    - /designs (System designs)
      - <DESIGN_NAME>.md (A system design file)
    - <DOCUMENT_NAME>.md (a system documentation file)
  - /.github (GitHub-related content)
    - /workflows (GitHub action workflows)
      - <WORKFLOW_NAME>\_workflow.yml (Singular GitHub action)
  - /.vscode (VS Code workspace settings & recommended extensions)
    - settings.json
    - extensions.json
  - /src
    - / tests (where Playwright tests etc go)
      ...
    - / backend (where .NET services go)
      - / <PROJECT_NAME>.Api (ASP.NET Core Web API project)
        - Controllers/
        - Program.cs
        - appsettings.json
        - <PROJECT_NAME>.Api.csproj
      - / <PROJECT_NAME>.Core (Business logic and domain models)
        - / Services
          - / Managers (iDesign Manager layer)
            - UserManager.cs
            ...
          - / Engines (iDesign Engine layer)
            - AuthenticationEngine.cs
            ...
          - / Data (iDesign Data Access layer)
            - UserRepository.cs
            - ApplicationDbContext.cs
            ...
        - / Models (Domain models and DTOs)
          - User.cs
          - UserDto.cs
          ...
        - / Interfaces (Shared interfaces)
          - / Managers
            - IUserManager.cs
          - / Engines
            - IAuthenticationEngine.cs
          - / Data
            - IUserRepository.cs
        - <PROJECT_NAME>.Core.csproj
      - / <PROJECT_NAME>.Infrastructure (External concerns)
        - / Persistence
          - ApplicationDbContext.cs
          - Migrations/
        - / Services (External service integrations)
        - <PROJECT_NAME>.Infrastructure.csproj
      - <PROJECT_NAME>.sln
    - / frontend (where React apps go)
      - public/
      - src/
        - components/
        - pages/
        - store/ (Redux store)
        - services/ (API services)
        - types/
        - App.tsx
        - index.tsx
      - package.json
      - tsconfig.json
      - tailwind.config.js
      - ...
    - ...
  - .gitignore
  - docker-compose.yml (Wire up the entire stack with all the dockerfiles)
  - Dockerfile.<PROJECT_NAME> (frontend / backend etc)
  - LICENSE
    - MIT
  - README.icon.png (The project thumbnail / icon)
  - README.md
    - Link to various documents in the .docs dir, in a neat table format.

# Description

This repository follows a structured approach designed for AI-enhanced software development. Each directory serves a specific purpose in the development lifecycle:

## Core Directories

### `.ai/` - AI Framework Intelligence

The heart of the AI coding framework, containing the orchestration files that guide the AI through the development process:

- **init.md**: The master prompt containing comprehensive instructions for AI agents
- **plan.md**: Auto-generated project plan with milestones and deliverables
- **session-state.md**: Live tracking of development progress and current status

### `.docs/` - Documentation Hub

Centralized location for all project documentation:

- **designs/**: System architecture and design documents following the 5-template structure
- **design.md**: Main design document with links to all architectural templates
- **repo-structure.md**: This document explaining the repository organization
- **docker-support.md**: Container setup and deployment guidelines

### `src/` - Source Code Organization

Following clean architecture principles with clear separation of concerns:

- **backend/**: API and business logic layers with proper dependency injection
- **frontend/**: User interface applications (web, mobile, desktop)

## Configuration & DevOps

### `.github/` - CI/CD Pipeline

- **workflows/**: Automated build, test, and deployment processes
- Supports containerization, security scanning, and multi-environment deployments

### `.vscode/` - Development Environment

- **settings.json**: Consistent code formatting and linting rules
- **extensions.json**: Recommended extensions for optimal development experience

## Project Files

- **README.md**: Main project documentation with quick start guide
- **docker-compose.yml**: Multi-service container orchestration
- **Dockerfile.\***: Service-specific container definitions
- **.gitignore**: Version control exclusion patterns
- **LICENSE**: MIT license for open source distribution

This structure ensures that AI agents can navigate the codebase efficiently while maintaining clean separation between documentation, source code, and infrastructure components.

[<< Back](../README.md)
