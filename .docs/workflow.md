[<< Back](../README.md)

## Workflow
Workflows leverage GitHub actions. The following describes the rules for contributing workflows (Actions) to this repo.

### Introduction
See the GitHib Workflow file(s) in `<REPO_ROOT>/.github/workflows/<WORKFLOW_NAME>.yml`.

## Workflows
### Containerization Example
This workflow simply builds a Dockerfile in the repository root and push it to the correct image in Docker Hub based on the environment variables specified on the [Support & Contribute](./support-contribute.md) page. This workflow also updates that image's description to match that of our README.md file.

[<< Back](../README.md)