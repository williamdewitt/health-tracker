# 🎯 Enhanced Session State Template

**🚨 CRITICAL**: This template MUST be used for ALL AI coding framework sessions. Copy this template to create `session-state.md` and update it continuously throughout development.

---

## 📍 **SESSION CONTEXT ANCHOR**

### **Project Identity**
- **Project Name**: [Project Name]
- **Project Type**: [Task Manager | E-commerce | Social Media | IoT Dashboard | Custom]
- **Complexity Level**: [Simple (1-5 use cases) | Medium (6-15) | Complex (16+) | Data-Intensive]
- **Session ID**: [Unique session identifier]
- **Session Start Date**: [YYYY-MM-DD]
- **Last Updated**: [YYYY-MM-DD HH:MM]

### **Current Development Phase**
- **Phase**: [Discovery | Planning | Design | Implementation | Testing | Deployment]
- **Milestone**: [Specific milestone name]
- **Progress**: [X%] - [Detailed progress description]
- **Next Action**: [Specific next 1-2 actions]
- **Context Status**: [Fresh Start | Conversation Resume | Post-Summary | Context Recovered]

---

## 🏗️ **ARCHITECTURAL CONTEXT**

### **Architecture Pattern** *(CRITICAL FOR CONSISTENCY)*
```markdown
SELECTED PATTERN: [Monolith | Modular Monolith | Microservices | CQRS/Event Sourcing]

SELECTION REASONING:
- Complexity Score: [Calculated score]
- Use Case Count: [Number]
- Integration Requirements: [List key integrations]
- Scale Requirements: [Expected users/data volume]

PATTERN VALIDATION:
✅ Matches complexity level
✅ Supports required integrations  
✅ Aligns with team capabilities
✅ Meets performance requirements
```

### **Technology Stack** *(NO CHANGES WITHOUT VALIDATION)*
```markdown
FRONTEND:
- Framework: [React 18 | Next.js | Vue | Angular]
- Language: [TypeScript | JavaScript]
- Build Tool: [Vite | Webpack | Next.js]
- UI Library: [Tailwind CSS | Material-UI | Ant Design]
- State Management: [Zustand | Redux | Context API]

BACKEND:
- Framework: [ASP.NET Core 8.0 | Node.js | Python FastAPI]
- Language: [C# | TypeScript | Python]
- API Style: [REST | GraphQL | gRPC]
- Authentication: [JWT | OAuth2 | Auth0]

DATABASE:
- Primary: [PostgreSQL | MongoDB | SQL Server]
- Cache: [Redis | Memcached | In-Memory]
- Search: [Elasticsearch | None]
- Time-Series: [InfluxDB | None]

INFRASTRUCTURE:
- Deployment: [Docker | Kubernetes | Cloud Functions]
- CI/CD: [GitHub Actions | Azure DevOps | Jenkins]
- Monitoring: [Application Insights | DataDog | Prometheus]
- Cloud: [Azure | AWS | GCP | On-Premise]
```

### **Framework Pattern Applied**
```markdown
EXAMPLE PATTERN: [task-manager | ecommerce | social-media | iot-dashboard]

PATTERN JUSTIFICATION:
- Feature Alignment: [How project features match example]
- Complexity Match: [How complexity levels align]
- Architecture Fit: [How architecture patterns match]
- Technology Overlap: [How tech stacks align]

PATTERN ADAPTATIONS:
- [List any modifications from the base pattern]
- [Explain reasoning for each adaptation]
```

---

## 📋 **REQUIREMENTS CONTEXT**

### **Business Requirements** *(COMPLETE UNDERSTANDING)*
```markdown
PRIMARY USE CASES: [List 3-5 core use cases]
1. [Use case 1 with acceptance criteria]
2. [Use case 2 with acceptance criteria]
3. [Use case 3 with acceptance criteria]

SECONDARY USE CASES: [List additional use cases]
- [Use case A]
- [Use case B]

BUSINESS RULES: [Key business logic constraints]
- [Rule 1: Description and impact]
- [Rule 2: Description and impact]

NON-FUNCTIONAL REQUIREMENTS:
- Performance: [Specific performance requirements]
- Security: [Security requirements and compliance]
- Scalability: [Expected scale and growth]
- Availability: [Uptime and reliability requirements]
```

### **User Personas & Flows**
```markdown
PRIMARY USERS:
- [User Type 1]: [Description, needs, and key workflows]
- [User Type 2]: [Description, needs, and key workflows]

SECONDARY USERS:
- [User Type A]: [Description and limited workflows]

CRITICAL USER FLOWS:
1. [Flow 1]: [Step-by-step user journey]
2. [Flow 2]: [Step-by-step user journey]
```

---

## 🎨 **DESIGN CONTEXT**

### **Visual Design Direction**
```markdown
DESIGN INSPIRATION: [Description of visual references]
- Style: [Modern | Classic | Minimalist | Bold | Industry-specific]
- Color Palette: [Primary colors and reasoning]
- Typography: [Font choices and hierarchy]
- Layout Style: [Grid system, spacing, component approach]

DESIGN SYSTEM STATUS:
✅ Color palette defined
✅ Typography scale established
✅ Component library selected
✅ Responsive breakpoints set
□ Design tokens created
□ Component documentation

ACCESSIBILITY REQUIREMENTS:
- WCAG Level: [A | AA | AAA]
- Screen Reader Support: [Required | Optional]
- Keyboard Navigation: [Full | Partial]
- Color Contrast: [Validated | In Progress]
```

### **UI/UX Patterns**
```markdown
COMPONENT PATTERNS:
- Navigation: [Top nav | Side nav | Mobile drawer]
- Forms: [Multi-step | Single page | Modal]
- Data Display: [Tables | Cards | Lists]
- Feedback: [Toasts | Modals | Inline messages]

INTERACTION PATTERNS:
- Loading States: [Skeletons | Spinners | Progressive]
- Error Handling: [Inline | Toast | Page-level]
- Success Feedback: [Notifications | Animations | Messages]
```

---

## 📚 **DOCUMENTATION CONTEXT**

### **Design Documents Created**
```markdown
DESIGN DOCUMENT STATUS:
✅ [./.docs/designs/1-use-cases.md] - Complete with all user stories
✅ [./.docs/designs/2-system-components.md] - Architecture and components
✅ [./.docs/designs/3-class.md] - Class diagrams and relationships
□ [./.docs/designs/4-sequence.md] - Business flow diagrams
□ [./.docs/designs/5-frontend.md] - UI specifications and mockups

DOCUMENT VALIDATION:
- Use Cases: [Validated against requirements | Needs review]
- System Design: [Validated against architecture | Needs update]
- Class Design: [Validated against implementation | Needs revision]
```

### **Implementation Documentation**
```markdown
CODE DOCUMENTATION STATUS:
✅ README.md - Project overview and setup
✅ API Documentation - [Swagger | Postman | GraphQL Schema]
□ Database Schema Documentation
□ Deployment Guide
□ Contributing Guidelines

DOCUMENTATION QUALITY:
- API Coverage: [X%] - [All endpoints documented | Needs update]
- Code Comments: [Comprehensive | Minimal | Needs improvement]
- Example Usage: [Complete | Partial | Missing]
```

---

## ⚡ **IMPLEMENTATION CONTEXT**

### **Current Implementation Status**
```markdown
PROJECT STRUCTURE:
✅ Backend project structure (Clean Architecture)
✅ Frontend project structure (React + TypeScript)
✅ Database schema and migrations
□ API endpoints implementation
□ Frontend components implementation
□ Integration testing setup

COMPLETED COMPONENTS:
1. [Component 1]: [Description and validation status]
2. [Component 2]: [Description and validation status]
3. [Component 3]: [Description and validation status]

IN-PROGRESS COMPONENTS:
1. [Component A]: [Current status and next steps]
2. [Component B]: [Current status and next steps]

PENDING COMPONENTS:
1. [Component X]: [Dependencies and planned approach]
2. [Component Y]: [Dependencies and planned approach]
```

### **Quality Gates Status**
```markdown
CODE QUALITY:
- Linting: [✅ Passing | ⚠️ Warnings | ❌ Errors] - [Details]
- Formatting: [✅ Consistent | ❌ Needs formatting] - [Tool used]
- Type Safety: [✅ Full TypeScript | ⚠️ Some any types | ❌ Not typed]

BUILD STATUS:
- Backend Build: [✅ Passing | ❌ Failing] - [Last build time]
- Frontend Build: [✅ Passing | ❌ Failing] - [Last build time]
- Docker Build: [✅ Passing | ❌ Not configured] - [Container status]

TESTING STATUS:
- Unit Tests: [X% coverage] - [✅ Passing | ❌ Some failing]
- Integration Tests: [✅ Passing | ❌ Not implemented]
- E2E Tests: [✅ Passing | ❌ Not implemented]

DEPLOYMENT STATUS:
- Local Development: [✅ Working | ❌ Issues] - [Setup complexity]
- Staging Environment: [✅ Deployed | ❌ Not configured]
- Production Environment: [⚠️ Ready | ❌ Not ready]
```

### **Frontend Quality Status**
```markdown
UI/UX REQUIREMENTS:
- Requirements Status: [✅ Complete | 🔄 In Progress | ❌ Not Started | ⚪ Not Applicable]
- UI/UX Template Used: [✅ Yes | ❌ No | ⚪ Not Required]
- Visual Specifications: [✅ Documented | ⚠️ Partial | ❌ Missing]
- Interactive States Defined: [✅ Complete | ⚠️ Basic | ❌ None]
- Responsive Requirements: [✅ Documented | ⚠️ Basic | ❌ Missing]

BEAUTY STANDARDS COMPLIANCE:
- Beauty Score: [___/100] - [🌟 Exceptional | ✅ Professional | ⚠️ Acceptable | ❌ Needs Work]
- Color & Contrast: [✅ Passed | ❌ Failed | ⚪ Not Applicable]
- Typography & Readability: [✅ Passed | ❌ Failed | ⚪ Not Applicable]
- Layout & Spacing: [✅ Passed | ❌ Failed | ⚪ Not Applicable]
- Component Quality: [✅ Passed | ❌ Failed | ⚪ Not Applicable]

FRONTEND TESTING STATUS:
- Dev Console Testing: [✅ Complete | 🔄 In Progress | ❌ Not Done | ⚪ Not Applicable]
- Responsive Testing: [✅ All Breakpoints | ⚠️ Basic | ❌ Not Done]
- Interactive States Testing: [✅ Complete | ⚠️ Basic | ❌ Not Done]
- Cross-Browser Testing: [✅ Complete | ⚠️ Primary Only | ❌ Not Done]
- Performance Validation: [✅ Passed | ⚠️ Acceptable | ❌ Failed]

QUALITY GATE STATUS:
- Pre-Development Gate: [✅ Passed | ❌ Failed | 🔄 In Progress | ⚪ Not Required]
- Mid-Development Gate: [✅ Passed | ❌ Failed | 🔄 In Progress | ⚪ Not Required]
- Pre-Release Gate: [✅ Passed | ❌ Failed | 🔄 In Progress | ⚪ Not Required]

FRONTEND ISSUES TRACKING:
- Blocking Issues: [None | List specific issues requiring resolution]
- Visual Quality Debt: [None | List components needing beauty improvements]
- Testing Gaps: [None | List untested or partially tested components]
- Performance Issues: [None | List performance bottlenecks or concerns]
```

---

## 🔄 **CONTEXT PERSISTENCE TRACKING**

### **Context Validation History**
```markdown
VALIDATION LOG:
[YYYY-MM-DD HH:MM] - ✅ Context validated - No inconsistencies
[YYYY-MM-DD HH:MM] - ⚠️ Minor inconsistency resolved - Tech stack clarification
[YYYY-MM-DD HH:MM] - ❌ Major inconsistency detected - Architecture alignment issue
[YYYY-MM-DD HH:MM] - ✅ Context recovered - Full validation passed

INCONSISTENCY PATTERNS:
- Most Common: [Type of inconsistency and frequency]
- Resolution Time: [Average time to resolve context issues]
- Prevention: [Strategies applied to prevent future issues]
```

### **Context Carry-over Checklist**
```markdown
BEFORE EACH IMPLEMENTATION PHASE:
□ Session state file read and validated
□ Architectural decisions confirmed
□ Technology stack validated
□ Design document requirements reviewed
□ Business logic understanding confirmed
□ Quality gate status checked
□ Visual design direction confirmed
□ Previous context successfully carried over

CONTEXT HEALTH SCORE: [X/8] - [Excellent | Good | Needs Attention | Poor]
```

---

## 🎯 **SESSION RECOVERY COMMANDS**

### **Quick Context Recovery**
```markdown
RECOVERY PROTOCOL FOR NEW SESSIONS:

1. READ THIS FILE COMPLETELY
2. VALIDATE each section against current project state
3. READ referenced design documents:
   - ./.docs/designs/1-use-cases.md
   - ./.docs/designs/2-system-components.md
   - ./.docs/designs/3-class.md
4. CONFIRM architectural pattern and technology stack
5. CHECK build and test status
6. REVIEW next planned actions
7. EXECUTE context validation checkpoint
8. PROCEED with full context awareness

EMERGENCY CONTEXT COMMANDS:
- "Read session state and validate context"
- "Execute context recovery protocol"  
- "Validate architectural consistency"
- "Check design document alignment"
- "Confirm technology stack decisions"
```

### **Context Validation Triggers**
```markdown
MANDATORY VALIDATION SCENARIOS:
✅ Every 5 actions (action counter enforcement)
✅ Before major implementation phases
✅ After conversation summarization
✅ When architectural decisions are considered
✅ Before technology stack changes
✅ After design document updates
✅ Before quality gate execution
✅ When inconsistencies are suspected

VALIDATION SUCCESS CRITERIA:
- All sections of this file are current and accurate
- No contradictions between conversation and documented context
- Clear alignment between design documents and implementation
- Consistent architectural and technology decisions
- Accurate progress tracking and milestone status
```

---

## 📋 **DOCUMENT REVIEW TRACKING**

### **Document Anchoring Status**
```markdown
DOCUMENT REVIEW STATUS: [🟢 Current | 🟡 Due Soon | 🔴 Overdue]

REQUIREMENTS/PROMPT REVIEW:
- Last Reviewed: [YYYY-MM-DD HH:MM] - [X actions ago]
- Review Status: [🟢🟡🔴⚠️] - [Brief alignment assessment]
- Key Findings: [Any important observations from last review]
- Next Review Due: [When based on 15-action rule or milestone]

DESIGN DOCUMENT REVIEW:
- Last Reviewed: [YYYY-MM-DD HH:MM] - [X actions ago]
- Documents Reviewed: [List specific design docs referenced]
- Review Status: [🟢🟡🔴⚠️] - [Brief compliance assessment]
- Architecture Compliance: [Any deviations or confirmations noted]
- Next Review Due: [When based on 10-action rule or component work]

IMPLEMENTATION PLAN REVIEW:
- Last Reviewed: [YYYY-MM-DD HH:MM] - [X actions ago]
- Plan Status: [🟢🟡🔴⚠️] - [Brief adherence assessment]
- Progress Validation: [Actual vs planned progress comparison]
- Plan Adjustments Needed: [Any scope or timeline changes required]
- Next Review Due: [When based on 8-action rule or milestone]
```

### **AI Positioning Status**
```markdown
POSITIONING LAST UPDATED: [YYYY-MM-DD HH:MM]

MISSION ALIGNMENT: [🟢🟡🔴⚠️]
- Status: [Brief description of business purpose alignment]
- Last Mission Review: [When original prompt was re-read]
- Drift Risk: [Low | Medium | High]

ARCHITECTURE ALIGNMENT: [🟢🟡🔴⚠️]
- Status: [Brief description of design document compliance]
- Last Architecture Review: [When design docs were referenced]
- Compliance Issues: [Any known deviations or concerns]

PLAN ALIGNMENT: [🟢🟡🔴⚠️]
- Status: [Brief description of plan adherence]
- Last Plan Review: [When implementation plan was validated]
- Plan Deviation: [None | Minor | Major - with details]

QUALITY ALIGNMENT: [🟢🟡🔴⚠️]
- Status: [Brief description of quality standard compliance]
- Quality Gate Status: [Current state of testing, linting, etc.]
- Quality Debt: [Any technical debt or quality issues]
```

### **Document Evolution Tracking**
```markdown
DOCUMENT CHANGE LOG:
- [YYYY-MM-DD]: [Document] - [Change description]
- [YYYY-MM-DD]: [Document] - [Change description]

DOCUMENT FRESHNESS ASSESSMENT:
- Requirements: [Fresh | Aging | Stale] - [Last significant update]
- Design Docs: [Fresh | Aging | Stale] - [Last significant update]  
- Implementation Plan: [Fresh | Aging | Stale] - [Last significant update]

REQUIRED DOCUMENT UPDATES:
□ [Document] needs update because [reason]
□ [Document] needs update because [reason]
```

---

## 📊 **SESSION METRICS**

### **Development Velocity Tracking**
```markdown
VELOCITY METRICS:
- Actions per Hour: [Average rate of meaningful progress]
- Milestone Completion Rate: [On track | Behind | Ahead of schedule]
- Context Switch Overhead: [Time spent on context recovery]
- Decision Reversal Rate: [Frequency of changed decisions]

QUALITY METRICS:
- Context Consistency Score: [X%] - [Excellent | Good | Poor]
- Documentation Completeness: [X%] - [All docs current and accurate]
- Implementation Alignment: [X%] - [Code matches design documents]
- Framework Compliance: [X%] - [Following framework patterns]
```

### **Session Health Indicators**
```markdown
HEALTH STATUS: [🟢 Excellent | 🟡 Good | 🟠 Needs Attention | 🔴 Critical]

POSITIVE INDICATORS:
✅ Consistent progress toward milestones
✅ No architectural decision reversals
✅ Quality gates consistently passing
✅ Context validation successful each time
✅ Design-implementation alignment maintained

WARNING SIGNS:
⚠️ Repeated context validation failures
⚠️ Frequent technology stack reconsiderations
⚠️ Quality gate failures
⚠️ Design document inconsistencies
⚠️ Milestone deadline slippage

CRITICAL ISSUES:
🚨 Major architectural decision reversals
🚨 Complete context loss requiring full recovery
🚨 Build/deployment pipeline failures
🚨 Security or compliance violations
```

---

**📝 TEMPLATE USAGE**: Copy this template, rename to `session-state.md`, and update continuously throughout development. This is your primary source of truth for context persistence.
