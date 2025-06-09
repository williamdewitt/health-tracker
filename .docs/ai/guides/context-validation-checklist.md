# ✅ Context Validation Checklist

**Version**: 2.0  
**Purpose**: Mandatory validation checklist for AI coding framework sessions  
**Usage**: Execute this checklist every 5 actions or before major implementation phases

---

## 🚨 **MANDATORY PRE-VALIDATION REQUIREMENTS**

### **Action Counter Check**
```markdown
CURRENT ACTION COUNT: ___/5

STATUS CHECK:
□ Actions 1-3: Normal operation continues
□ Action 4: Context warning issued - validation due next action
□ Action 5: MANDATORY validation checkpoint - MUST complete before proceeding
□ Action 5+: CRITICAL - Validation overdue, HALT until completed
```

### **Session State File Access**
```markdown
SESSION STATE FILE STATUS:
□ .github/progress/session-state.md EXISTS and is readable
□ File was updated within last 24 hours
□ File contains complete information (all sections filled)
□ File timestamp matches expected development timeline

IF FILE MISSING OR STALE:
□ Create new session state from enhanced template
□ Populate all sections with current project context
□ Validate against current conversation and project state
```

---

## 📋 **CONTEXT CONSISTENCY VALIDATION**

### **1. Architectural Context Validation**
```markdown
ARCHITECTURE CONSISTENCY CHECK:
□ Current conversation mentions match documented architecture pattern
□ No conflicting architectural decisions in recent conversation
□ Technology stack remains consistent with documented choices
□ Design patterns align with selected framework example

VALIDATION QUESTIONS:
- Does current conversation suggest same architecture as session state?
- Have any technology choices been questioned or changed?
- Are we following the same design patterns established earlier?
- Is the framework example pattern still being applied?

RED FLAGS:
❌ Conversation suggests different architecture (monolith vs microservices)
❌ Technology stack changes mentioned without documentation update
❌ Design patterns contradict established patterns
❌ Framework example switched without validation
```

### **2. Business Requirements Validation**
```markdown
REQUIREMENTS CONSISTENCY CHECK:
□ Current business logic discussions match documented requirements
□ No new requirements introduced without documentation
□ User stories remain consistent with original understanding
□ Business rules haven't changed without explicit discussion

VALIDATION QUESTIONS:
- Are we solving the same business problems as documented?
- Have any new requirements been discovered or introduced?
- Do current implementation discussions align with use cases?
- Are business rules being consistently applied?

RED FLAGS:
❌ New business requirements mentioned without documentation
❌ User stories changed without explicit requirement evolution
❌ Business logic contradicts documented rules
❌ Implementation doesn't serve documented use cases
```

### **3. Implementation Progress Validation**
```markdown
PROGRESS CONSISTENCY CHECK:
□ Current implementation matches documented progress percentage
□ Completed work aligns with milestone descriptions
□ Next actions match documented planned activities
□ Quality gates status reflects actual project state

VALIDATION QUESTIONS:
- Does current progress match documented milestone percentage?
- Are we working on the expected next actions?
- Do quality gates (build/test/lint) match documented status?
- Is timeline tracking accurate and realistic?

RED FLAGS:
❌ Progress tracking significantly out of sync with actual work
❌ Working on different tasks than documented next actions
❌ Quality gate status doesn't match actual project state
❌ Timeline expectations unrealistic or outdated
```

### **4. Design Document Alignment**
```markdown
DESIGN DOCUMENT CONSISTENCY CHECK:
□ Current implementation follows documented design specifications
□ No implementation decisions contradict design documents
□ Component structure matches designed architecture
□ API endpoints align with designed system interfaces

VALIDATION QUESTIONS:
- Are we implementing components as designed in system documents?
- Do current API discussions match designed interfaces?
- Is class structure following documented design patterns?
- Are UI components aligned with frontend design specifications?

RED FLAGS:
❌ Implementation differs significantly from design documents
❌ API changes made without design document updates
❌ Component relationships don't match designed architecture
❌ UI implementation ignores design system specifications
```

### **5. Document Anchoring Validation**
```markdown
DOCUMENT ANCHORING CHECK:
□ Original requirements/prompt read within appropriate timeframe
□ Design documents reviewed for current component work
□ Implementation plan validated against current progress
□ AI positioning status is current and accurate

TIMEFRAME REQUIREMENTS:
□ Requirements: Read within last 15 actions OR before major component
□ Design Docs: Read relevant sections within last 10 actions
□ Plan: Validated within last 8 actions OR at milestone checkpoints
□ AI Position: Updated within last 5 actions

AI POSITIONING STATUS:
□ Mission alignment status known and current (🟢🟡🔴⚠️)
□ Architecture alignment status validated (🟢🟡🔴⚠️)
□ Plan alignment status confirmed (🟢🟡🔴⚠️)
□ Quality alignment status assessed (🟢🟡🔴⚠️)

DOCUMENT REVIEW TRIGGERS:
□ Before implementing new major component
□ At 25%, 50%, 75%, 100% milestone completion
□ When context validation detects potential drift
□ When 15 actions passed since last requirements review

RED FLAGS:
❌ Original requirements not reviewed in 20+ actions
❌ Design documents not referenced during component implementation
❌ Implementation plan ignored or significantly deviated from
❌ AI positioning status unknown or contains ⚠️ indicators
❌ Mission drift indicators detected (🔴 status in positioning)
❌ Architecture deviation from documented specifications
```

---

## 🔧 **CONTEXT RECOVERY VALIDATION**

### **Recovery Trigger Assessment**
```markdown
RECOVERY NEEDED IF ANY OF THESE ARE TRUE:
□ Architectural inconsistencies detected
□ Business requirements misalignment found
□ Progress tracking significantly inaccurate
□ Design document contradictions identified
□ Document anchoring failures detected
□ AI positioning status contains critical warnings
□ Technology stack confusion present
□ Quality gate status unreliable

RECOVERY ACTIONS COMPLETED:
□ All relevant documentation files read
□ Inconsistencies identified and analyzed
□ Root cause of inconsistencies determined
□ Conflicting information reconciled
□ Session state updated with validated information
□ Context anchors rebuilt with accurate information
```

### **Recovery Validation Checklist**
```markdown
POST-RECOVERY VALIDATION:
□ Session state file contains accurate, current information
□ All sections of session state align with project reality
□ Conversation context matches documented context
□ No remaining contradictions between sources
□ Clear path forward with aligned context

RECOVERY SUCCESS CRITERIA:
✅ Single source of truth established (session state file)
✅ All inconsistencies resolved with clear reasoning
✅ Context carries forward accurately
✅ Development can proceed with confidence
✅ Quality gates reflect actual project status
```

---

## 📊 **VALIDATION OUTCOME ASSESSMENT**

### **Validation Results**
```markdown
OVERALL VALIDATION STATUS:
□ 🟢 VALIDATED: All checks passed, context fully consistent
□ 🟡 MINOR ISSUES: Small inconsistencies resolved, proceeding
□ 🟠 MAJOR ISSUES: Significant inconsistencies, recovery required
□ 🔴 CRITICAL: Context completely inconsistent, full recovery needed

VALIDATION SCORE: ___/20 checks passed

SCORE INTERPRETATION:
- 20/20: 🟢 Excellent - Perfect context consistency
- 18-19/20: 🟡 Good - Minor issues, low risk
- 15-17/20: 🟠 Warning - Address issues before major work
- <15/20: 🔴 Critical - Mandatory recovery required
```

### **Required Actions Based on Results**
```markdown
🟢 VALIDATED (20/20 or 19/20):
□ Update action counter to 0/5
□ Proceed with planned implementation
□ Continue normal development workflow
□ Schedule next validation in 5 actions

🟡 MINOR ISSUES (18-19/20):
□ Document specific inconsistencies found
□ Make minor corrections to session state
□ Verify corrections with quick re-validation
□ Proceed with heightened awareness
□ Reset action counter to 0/5

🟠 MAJOR ISSUES (15-17/20):
□ Halt current implementation work
□ Execute formal context recovery protocol
□ Update all affected documentation
□ Perform full validation re-check
□ Only proceed after achieving 🟢 status

🔴 CRITICAL (< 15/20):
□ STOP all development work immediately
□ Execute emergency context recovery
□ Rebuild context from authoritative sources
□ Update session state comprehensively
□ Validate recovery with fresh context validation
□ Document lessons learned to prevent recurrence
```

---

## 🎯 **POST-VALIDATION ACTIONS**

### **Successful Validation Completion**
```markdown
REQUIRED POST-VALIDATION TASKS:
□ Update session state with validation timestamp
□ Reset action counter to 0/5
□ Document validation results in session log
□ Confirm next 1-2 planned actions
□ Update context anchor in next progress message

VALIDATION LOG ENTRY FORMAT:
[YYYY-MM-DD HH:MM] - Context Validation: [STATUS] - [BRIEF SUMMARY]
Example: [2025-06-09 14:30] - Context Validation: 🟢 VALIDATED - All checks passed, architecture consistent
```

### **Enhanced Progress Message Format**
```markdown
NEXT PROGRESS MESSAGE MUST INCLUDE:
📍 **[MILESTONE: {name}] ({progress}%) - {action}**
🔄 Context: {current_phase} | Pattern: {example_pattern_used}
🏗️ Stack: {tech_decisions} | Design: {visual_direction_status}
📚 Docs: {design_docs_referenced} | Next: {next_2_actions}
✅ Quality: {linting_status} | {build_status} | {test_status}
🎯 Session: {timestamp} | State: .github/progress/session-state.md
🧭 AI Position: {mission_status} | {architecture_status} | {plan_status}
🧠 Context Check: {validation_status} | Actions Since Last: 0/5

WHERE validation_status IS:
- 🟢 VALIDATED: Full consistency confirmed
- 🟡 MINOR RESOLVED: Small issues addressed
- ✅ RECOVERED: Major issues resolved successfully

WHERE positioning statuses ARE:
- Mission: 🟢🟡🔴⚠️ based on business purpose alignment
- Architecture: 🟢🟡🔴⚠️ based on design document compliance
- Plan: 🟢🟡🔴⚠️ based on implementation plan adherence
```

---

## ⚡ **EMERGENCY CONTEXT RECOVERY**

### **Critical Context Loss Indicators**
```markdown
EMERGENCY RECOVERY TRIGGERS:
🚨 Cannot locate or read session state file
🚨 Session state file is empty or corrupted
🚨 Conversation context completely contradicts all documentation
🚨 Major architectural decisions being reconsidered without cause
🚨 Technology stack being questioned without documented reasoning
🚨 Business requirements seem unfamiliar or changed dramatically

EMERGENCY RECOVERY PROTOCOL:
1. HALT all development activity immediately
2. READ all available project documentation
3. ANALYZE conversation history for context clues
4. RECONSTRUCT session state from available information
5. VALIDATE reconstructed context with project reality
6. DOCUMENT recovery process and lessons learned
7. IMPLEMENT additional safeguards to prevent recurrence
```

### **Recovery Success Validation**
```markdown
EMERGENCY RECOVERY COMPLETE WHEN:
□ Session state file exists and is comprehensive
□ All major architectural decisions documented and validated
□ Technology stack choices clearly established and consistent
□ Business requirements understood and documented
□ Progress tracking accurate and realistic
□ Design documents align with implementation reality
□ Quality gates status reflects actual project state
□ Clear path forward established with high confidence

RECOVERY CONFIDENCE LEVEL:
□ High: All context fully recovered and validated
□ Medium: Most context recovered, some gaps remain
□ Low: Partial recovery, significant uncertainties remain

PROCEED ONLY WITH HIGH CONFIDENCE RECOVERY
```

---

**⚠️ CRITICAL REMINDER**: This validation checklist is MANDATORY every 5 actions. No exceptions. Context consistency is the foundation of effective AI-driven development. Skipping validation leads to inconsistent, inefficient development cycles and poor-quality outcomes.
