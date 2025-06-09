# 🗂️ Path Standards Guide

**AI Coding Framework Path Standardization Reference**

## 📋 Overview

This guide establishes consistent path patterns for all AI Coding Framework documentation to ensure reliable AI navigation and eliminate workspace confusion.

## 🎯 Core Path Standards

### Repository Root Relative Paths

**ALWAYS use relative paths from repository root with `./` prefix:**

```markdown
✅ CORRECT PATH PATTERNS:
./.docs/ai/guides/
./.docs/ai/templates/
./.docs/ai/checklists/
./.docs/designs/
./.github/plans/
./.github/progress/
./src/backend/
./src/frontend/
./README.md
./package.json
```

```markdown
❌ INCORRECT PATH PATTERNS:
/.docs/ai/guides/          (absolute filesystem path - confuses AI)
docs/ai/guides/            (no prefix - ambiguous)
../docs/ai/guides/         (relative to current file - unreliable)
/src/backend/              (absolute filesystem path)
src/backend/               (no prefix - ambiguous)
```

### Working Directory Assumptions

**ALWAYS assume current working directory IS the project root:**

```markdown
✅ CORRECT WORKSPACE LANGUAGE:
"The current working directory is the project root"
"Create project structure in the current workspace"
"Use relative paths from the current directory"
"All project files are relative to the workspace root"

❌ INCORRECT WORKSPACE LANGUAGE:
"Please navigate to the project root"
"Select the project directory"
"Open the project folder"
"Change to the project directory"
"Navigate to the workspace"
```

## 📁 Path Categories

### 1. Documentation Paths
```markdown
✅ Framework Documentation:
./.docs/ai/prompts/initialize.md
./.docs/ai/guides/path-standards-guide.md
./.docs/ai/templates/enhanced-session-state-template.md
./.docs/ai/checklists/context-validation-checklist.md

✅ Design Documents:
./.docs/designs/1-use-cases.md
./.docs/designs/2-system-components.md
./.docs/designs/3-class.md
./.docs/designs/4-sequence.md
./.docs/designs/5-frontend.md

✅ Framework Guides:
./.docs/design.md
./.docs/repo-structure.md
./.docs/ai/guides/quickstart.md
```

### 2. GitHub Integration Paths
```markdown
✅ GitHub Paths:
./.github/plans/project-plan.md
./.github/progress/session-state.md
./.github/workflows/ci-cd.yml
./.github/ISSUE_TEMPLATE/
./.github/PULL_REQUEST_TEMPLATE.md
```

### 3. Source Code Paths
```markdown
✅ Backend Paths:
./src/backend/ProjectName.Api/
./src/backend/ProjectName.Core/
./src/backend/ProjectName.Shared/
./src/backend/ProjectName.Tests/

✅ Frontend Paths:
./src/frontend/src/components/
./src/frontend/src/pages/
./src/frontend/src/utils/
./src/frontend/public/
```

### 4. Configuration Paths
```markdown
✅ Configuration Paths:
./docker-compose.yml
./Dockerfile.ProjectName
./.env.example
./.gitignore
./package.json
./README.md
```

## 🔍 Path Validation Rules

### Documentation Writing Standards

**When referencing files in documentation:**

```markdown
✅ CORRECT REFERENCES:
"Read the initialization prompt at `./.docs/ai/prompts/initialize.md`"
"Follow the template in `./.docs/ai/templates/session-state-template.md`"
"Reference the design document at `./.docs/designs/1-use-cases.md`"
"Check the project plan in `./.github/plans/project-plan.md`"

❌ INCORRECT REFERENCES:
"Read the initialization prompt at `/.docs/ai/prompts/initialize.md`"
"Follow the template in `/docs/ai/templates/session-state-template.md`"
"Reference the design document at `docs/designs/1-use-cases.md`"
```

**When providing file paths in commands:**

```markdown
✅ CORRECT COMMAND PATHS:
`read_file ./.docs/ai/prompts/initialize.md`
`create_file ./src/backend/Controllers/UserController.cs`
`list_dir ./src/frontend/src/components/`

❌ INCORRECT COMMAND PATHS:
`read_file /.docs/ai/prompts/initialize.md`
`create_file /src/backend/Controllers/UserController.cs`
`list_dir src/frontend/src/components/`
```

## 🧭 Workspace Navigation Standards

### AI Working Directory Protocol

**MANDATORY workspace assumptions:**

1. **Current Directory IS Project Root**: Never ask users to navigate or change directories
2. **All Paths Are Relative**: Use `./` prefix for all project references
3. **No Directory Changes**: Never use `cd` commands or request navigation
4. **Workspace Assumption**: Assume current working directory contains project structure

**Implementation in AI prompts:**

```markdown
✅ CORRECT WORKSPACE GUIDANCE:
"Create the backend structure in `./src/backend/`"
"Initialize the project in the current workspace"
"All project files will be created relative to the current directory"
"The workspace root is the current working directory"

❌ INCORRECT WORKSPACE GUIDANCE:
"Navigate to the project root directory"
"Please select the project folder"
"Change to the workspace directory"
"Open the project in your preferred location"
```

## 📊 Path Consistency Checklist

### Documentation Review Checklist

**Before publishing any framework documentation:**

- [ ] All file paths use `./` prefix for repository root relative paths
- [ ] No absolute paths starting with `/` (except for system paths)
- [ ] No ambiguous paths without prefix
- [ ] All workspace references assume current working directory
- [ ] No navigation or directory change instructions
- [ ] Path patterns are consistent throughout the document
- [ ] All code examples use correct path patterns
- [ ] All command examples use relative paths

### Implementation Validation

**For AI navigation testing:**

- [ ] AI can read all referenced files with new path patterns
- [ ] No file reading failures due to path issues
- [ ] Workspace navigation works without directory changes
- [ ] All framework files are accessible with standardized paths
- [ ] Context validation includes path consistency checks

## 🚨 Common Path Mistakes

### Mistake 1: Absolute Filesystem Paths
```markdown
❌ WRONG: /.docs/ai/guides/quickstart.md
✅ RIGHT: ./.docs/ai/guides/quickstart.md

ISSUE: Leading / indicates absolute filesystem path
SOLUTION: Use ./ prefix for repository root relative paths
```

### Mistake 2: Missing Path Prefix
```markdown
❌ WRONG: docs/ai/guides/quickstart.md
✅ RIGHT: ./.docs/ai/guides/quickstart.md

ISSUE: No prefix makes path ambiguous
SOLUTION: Always use ./ prefix for clarity
```

### Mistake 3: Navigation Instructions
```markdown
❌ WRONG: "Navigate to the project directory and run..."
✅ RIGHT: "Run the following command in the current workspace..."

ISSUE: Asking for navigation creates user friction
SOLUTION: Assume current directory is correct workspace
```

### Mistake 4: Inconsistent Patterns
```markdown
❌ WRONG: Mix of /.docs/ and ./docs/ in same document
✅ RIGHT: Consistent ./.docs/ pattern throughout

ISSUE: Inconsistency confuses AI navigation
SOLUTION: Use same pattern consistently throughout
```

## 🔧 Implementation Examples

### Framework Documentation Example

```markdown
✅ CORRECT DOCUMENTATION PATTERN:

## Framework Files

- **Initialize Prompt**: `./.docs/ai/prompts/initialize.md`
- **Session State Template**: `./.docs/ai/templates/enhanced-session-state-template.md`
- **Context Validation**: `./.docs/ai/checklists/context-validation-checklist.md`

## Design Documents

Follow the templates in `./.docs/designs/` for all system design:
- Use Cases: `./.docs/designs/1-use-cases.md`
- System Components: `./.docs/designs/2-system-components.md`
- Class Diagrams: `./.docs/designs/3-class.md`

## Implementation

Create your backend structure in `./src/backend/` following the patterns
shown in `./.docs/repo-structure.md`. All source code should be organized
relative to the current workspace directory.
```

### AI Command Example

```markdown
✅ CORRECT AI COMMAND PATTERN:

1. Read the current session state:
   `read_file ./.github/progress/session-state.md`

2. Check the project plan:
   `read_file ./.github/plans/project-plan.md`

3. Create the backend structure:
   `create_file ./src/backend/ProjectName.Api/Controllers/UserController.cs`

4. Update the documentation:
   `insert_edit_into_file ./.docs/designs/3-class.md`
```

## 📈 Path Standards Enforcement

### Quality Assurance Process

1. **Documentation Review**: Check all path patterns before publishing
2. **AI Testing**: Validate AI can navigate with new path patterns
3. **Consistency Audit**: Regular reviews for path pattern consistency
4. **Template Updates**: Ensure all templates use correct path patterns

### Continuous Improvement

- Monitor AI navigation success rates with standardized paths
- Collect feedback on path clarity and usability
- Update standards based on practical usage patterns
- Maintain backward compatibility during transitions

---

**Created**: 2025-06-09  
**Last Updated**: 2025-06-09  
**Version**: 1.0  
**Status**: Active Standard
