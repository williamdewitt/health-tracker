# 🎯 Pattern Recognition Implementation Guide

## Actionable AI Instructions for Smart Decision Making

This guide provides concrete, executable instructions for AI agents to implement the framework's pattern recognition and automatic decision-making capabilities.

## 1. Project Classification Algorithm (Execute Immediately)

### Step 1: Requirements Analysis

When user provides initial project description, analyze the text for:

```markdown
**Entity Count Analysis:**

- Count distinct nouns representing data entities
- Examples: user, product, order, payment, notification, report, etc.
- Simple: 1-5 entities | Medium: 6-15 entities | Complex: 16+ entities

**Action Verb Detection:**

- Identify primary actions/operations
- Examples: create, read, update, delete, process, analyze, integrate, etc.
- Count unique action types across entities

**Integration Complexity:**

- Detect external service mentions
- Keywords: API, payment, email, SMS, real-time, analytics, ML, etc.
- Count integration points

**Complexity Score = Entities × Action Types × Integration Points**
```

### Step 2: Automatic Classification

```markdown
**Classification Rules:**

- Score 1-25: Simple Project → Use task-manager example patterns
- Score 26-150: Medium Project → Use e-commerce example patterns
- Score 151+: Complex Project → Use social-media example patterns
- Any analytics/IoT keywords → Use iot-dashboard patterns regardless of score
```

### Step 3: Apply Framework Example

```markdown
**Immediate Actions:**

1. Announce classification: "Based on analysis, this is a [Simple/Medium/Complex] project"
2. Reference example: "I'll apply patterns from .docs/examples/[pattern-name]/"
3. Read example documentation: Use read_file on the chosen example directory
4. Apply example's architecture, tech stack, and patterns automatically
```

## 2. Feature Pattern Recognition (Execute During Requirements)

### Keyword Detection & Response Matrix

```markdown
**Payment Keywords → E-commerce Security Pattern:**

- Keywords: payment, checkout, billing, subscription, stripe, paypal
- Actions:
  1. Read .docs/examples/ecommerce/ patterns
  2. Apply PCI DSS security requirements
  3. Implement payment service abstraction
  4. Add financial audit logging

**Real-time Keywords → WebSocket Pattern:**

- Keywords: real-time, live, instant, chat, notifications, updates
- Actions:
  1. Add SignalR/WebSocket implementation
  2. Implement event-driven architecture
  3. Add real-time database triggers
  4. Include connection management

**Analytics Keywords → Data Pattern:**

- Keywords: analytics, reports, dashboard, metrics, charts
- Actions:
  1. Read .docs/examples/iot-dashboard/ patterns
  2. Implement time-series database design
  3. Add chart/visualization libraries
  4. Include data aggregation services

**File Keywords → Media Pattern:**

- Keywords: upload, files, images, media, documents
- Actions:
  1. Implement file storage service
  2. Add cloud storage integration (AWS S3/Azure Blob)
  3. Include file validation and security
  4. Add media processing capabilities

**Admin Keywords → RBAC Pattern:**

- Keywords: admin, roles, permissions, users, management
- Actions:
  1. Implement role-based access control
  2. Add user management interfaces
  3. Include permission validation
  4. Add audit logging for admin actions
```

## 3. Smart Technology Stack Selection (Execute Automatically)

### Architecture Pattern Selection

```markdown
**Based on Classification:**

- Simple Projects: Monolithic architecture
  - Single deployable unit
  - Shared database
  - Integrated frontend/backend
- Medium Projects: Modular monolith
  - Clear module boundaries
  - Shared database with domain separation
  - API-driven frontend
- Complex Projects: Microservices
  - Service per domain
  - Database per service
  - API gateway pattern
- Data-Intensive: CQRS architecture
  - Command/Query separation
  - Event sourcing
  - Time-series optimizations
```

### Technology Stack Defaults

```markdown
**Automatic Stack Selection:**

**Simple Projects (Monolith):**

- Frontend: React 18 + TypeScript + Vite
- Backend: ASP.NET Core 8.0 + Web API
- Database: PostgreSQL + Entity Framework Core
- Auth: JWT + Refresh Tokens
- Real-time: SignalR (if needed)

**Medium Projects (Modular Monolith):**

- Frontend: React 18 + TypeScript + Next.js
- Backend: ASP.NET Core 8.0 + Clean Architecture
- Database: PostgreSQL + EF Core + Redis
- Auth: Identity + JWT + RBAC
- Integration: MediatR + FluentValidation

**Complex Projects (Microservices):**

- Frontend: React 18 + TypeScript + Micro-frontends
- Backend: ASP.NET Core 8.0 + Docker + Kubernetes
- Database: PostgreSQL + MongoDB + Redis
- Messaging: RabbitMQ + Apache Kafka
- Gateway: Ocelot + YARP

**Data-Intensive (CQRS):**

- Frontend: React 18 + D3.js + Chart libraries
- Backend: ASP.NET Core + CQRS + Event Sourcing
- Database: PostgreSQL + InfluxDB + Redis
- Processing: Apache Kafka + Apache Flink
- ML: Python services + TensorFlow/PyTorch
```

## 4. Enhanced Context Management (Execute Continuously)

### Session State Updates

```markdown
**Update Frequency:** Every 15% progress or major milestone
**Update Triggers:**

- Architecture decisions made
- Technology stack chosen
- Visual design direction established
- Major components implemented
- Quality gates passed/failed

**State File Content:**

1. Use .github/progress/session-state-template.md as base
2. Update all sections with current context
3. Include visual design references and decisions
4. Track framework pattern being followed
5. Record smart defaults applied
6. Include recovery commands
```

### Progress Anchoring Format

```markdown
**Use This Exact Format Every 3-5 Actions:**
📍 **[MILESTONE: {name}] ({progress}%) - {action}**
🔄 Context: {current_phase} | Pattern: {example_pattern_used}
🏗️ Stack: {tech_decisions} | Design: {visual_direction_status}
📚 Docs: {design_docs_referenced} | Next: {next_2_actions}
✅ Quality: {linting_status} | {build_status} | {test_status}
🎯 Session: {timestamp} | State: .github/progress/session-state.md

**Example:**
📍 **[MILESTONE: Backend API Setup] (35%) - Creating user management endpoints**
🔄 Context: Implementation Phase | Pattern: task-manager monolith
🏗️ Stack: ASP.NET Core + PostgreSQL + JWT | Design: Linear-inspired clean UI
📚 Docs: Referenced system_components.md, class.md | Next: Auth middleware, user tests  
✅ Quality: ✅ Linting | ✅ Build | ⏳ Tests pending
🎯 Session: 2024-01-15T14:30 | State: .github/progress/session-state.md
```

## 5. Error Recovery Protocol (Execute When Issues Occur)

### Error Detection Triggers

```markdown
**Automatic Error Detection:**

- Build failures → Dependency, configuration, or syntax issues
- Test failures → Business logic or integration problems
- Linting violations → Code quality or style issues
- Design misalignment → Implementation doesn't match specs
- Context inconsistency → Session state doesn't match workspace
```

### Resolution Strategies

```markdown
**Build Failures:**

1. Check package.json/csproj for missing dependencies
2. Verify configuration files (appsettings.json, etc.)
3. Validate code syntax and imports
4. Run package restore/update commands
5. Update session state with resolution

**Test Failures:**

1. Review test setup and configuration
2. Validate business logic implementation
3. Check test data and mocking
4. Verify integration test environment
5. Update tests if business requirements changed

**Linting Violations:**

1. Run automatic code formatting
2. Fix TypeScript/C# type issues
3. Resolve unused import/variable warnings
4. Apply consistent naming conventions
5. Update ESLint/analyzer configurations

**Design Misalignment:**

1. Read original design documents
2. Compare implementation with specifications
3. Identify specific discrepancies
4. Update implementation to match design
5. Document any necessary design changes
```

## 6. Quality Gate Integration (Execute Throughout Development)

### Continuous Quality Monitoring

```markdown
**After Each File Creation:**

- Run linting and formatting tools
- Verify syntax and compilation
- Check for unused imports/variables
- Validate naming conventions

**After Each Component:**

- Execute build verification
- Run relevant unit tests
- Check code coverage metrics
- Validate architectural compliance

**After Each Milestone:**

- Full test suite execution
- Security scan and validation
- Performance baseline testing
- Documentation completeness check
- Design-implementation alignment verification
```

### Quality Gate Automation Commands

```markdown
**Linting Commands:**

- Frontend: npm run lint && npm run format
- Backend: dotnet format && dotnet build --verbosity minimal

**Testing Commands:**

- Frontend: npm run test:coverage
- Backend: dotnet test --collect:"XPlat Code Coverage"

**Security Commands:**

- npm audit fix
- dotnet list package --vulnerable

**Build Verification:**

- Frontend: npm run build
- Backend: dotnet build --configuration Release
```

## Implementation Checklist

### ✅ At Project Start:

- [ ] Analyze requirements for complexity classification
- [ ] Detect feature patterns and apply appropriate templates
- [ ] Select optimal technology stack automatically
- [ ] Announce decisions and reasoning to user
- [ ] Create initial session state file

### ✅ During Development:

- [ ] Use enhanced progress anchoring format every 3-5 actions
- [ ] Update session state every 15% progress
- [ ] Execute continuous quality monitoring
- [ ] Apply error recovery protocols when issues arise
- [ ] Reference appropriate framework documentation

### ✅ At Milestones:

- [ ] Validate implementation against design documents
- [ ] Execute full quality gate validation
- [ ] Update session state with milestone completion
- [ ] Prepare context anchors for next phase
- [ ] Document any pattern adaptations made

This implementation guide transforms the conceptual intelligence enhancements into concrete, executable steps that AI agents can follow to deliver more autonomous, intelligent, and consistent software development outcomes using the AI Coding Framework.
