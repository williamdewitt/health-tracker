[<< Back](../README.md)

## Repo Structure
This document describes the desired repository structure. This may be used for AI coding when scaffolding the solution from scratch, for example.

### Structure
- ROOT (The repository root)
  - /.docs (The colelction of repository documents and system designs etc. This directory should be documented in [README.md](../README.md) too.)
    - /designs (System designs)
      - <DESIGN_NAME>.md (A system design file)
    - <DOCUMENT_NAME>.md (a system documentation file)
  - /.github (GitHub-related content)
    - / plans
    - / prompts
    - / workflows (GitHub action workflows)
      - <WORKFLOW_NAME>_workflow.yml (Singular GitHub action)
  - /.vscode (VS Code workspace settings & recommended extensions)
    - settings.json
    - extensions.json
  - /src
    - / backend (where services go)
      - / <PROJECT_NAME>.Api
      - / <PROJECT_NAME>.Core
        - / Services
          - / Managers
            ...
          - / Engines
            ...
          - / Data
            ...
      - / <PROJECT_NAME>.Shared
        - / Interfaces
          - / Managers
          - / Engines
          - / Data
            - IDatabaseContext.cs
            - ...
          - ...
        - / Const
          ...
        - / Enums
          ...
        - / Models
          ...
      - <PROJECT_NAME>.sln
    - / frontend (where frontend apps go)
  - .gitignore
  - docker-compose.yml (Wire up the entire stack with all the dockerfiles)
  - Dockerfile.<PROJECT_NAME> (frontend / backend etc)
  - LICENSE
    - MIT
  - README.md
    - Link to various documents in the .docs dir, in a neat table format.

# Description
Descriptions of the above layed out structure to follow.

[<< Back](../README.md)