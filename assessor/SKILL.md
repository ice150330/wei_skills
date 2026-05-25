---
name: assessor
description: Task complexity assessor with multi-factor scoring and confidence levels. Analyzes requests using keywords, file context, and historical accuracy to determine execution mode.
triggers:
  - always: true
  - priority: highest
---

# Task Assessor

## Purpose

Fast complexity assessment (under 3 seconds) with **confidence scoring** to route tasks accurately.

## Assessment Factors

```
Score = (keyword_match × 0.4) + (file_complexity × 0.3) + (historical × 0.3)
```

### 1. Keyword Analysis (权重 40%)

Load `heuristics.yaml` for weighted keywords:
- Complex keywords ("platform", "architecture"): +0.8-0.9
- Moderate keywords ("feature", "api"): +0.5-0.6
- Simple keywords ("fix typo", "print"): +0.1-0.2

### 2. File Context (权重 30%)

```
if git_status shows:
  - 1 file, <50 lines → Simple
  - 2-5 files, 50-500 lines → Moderate
  - 5+ files, >500 lines → Complex
```

### 3. Historical Accuracy (权重 30%)

Track past assessments:
- Was this type of task assessed correctly?
- Adjust based on actual execution time

## Confidence Levels

| Level | Range | Action |
|-------|-------|--------|
| **High** | >0.8 | Direct routing, no confirmation |
| **Medium** | 0.5-0.8 | Brief confirmation with user |
| **Low** | <0.5 | Ask clarifying questions |

## Decision Flow

```
User Input
    ↓
┌─────────────────┐
│ Calculate Score │
│ Load heuristics │
└────────┬────────┘
         ↓
┌─────────────────┐
│ Check Confidence│
└────────┬────────┘
         ↓
    ┌────┴────┐
   High     Medium/Low
    │          │
    ▼          ▼
 Route    Confirm/Ask
    │          │
    └────┬─────┘
         ↓
   Activate Mode
```

## Feedback Loop

After task completion:
1. Record actual complexity
2. Compare with assessment
3. Adjust weights if needed
4. Update historical accuracy

## Assessment Criteria

### Quick Mode (< 10 minutes)
**Indicators:**
- Single command or question
- Under 20 lines of code
- Existing solution available
- No design decisions needed

**Examples:**
- "How to print in Python?"
- "Fix this typo"
- "Run the tests"
- "Explain this error"

**Action:** Direct answer, no workflow, no planning.

---

### Normal Mode (10 minutes - 4 hours)
**Indicators:**
- 1-3 files affected
- Single feature or component
- Clear requirements
- Existing codebase context

**Examples:**
- "Add email validation to the form"
- "Create a user list API"
- "Fix this React component bug"
- "Optimize this database query"

**Action:** Use expert(s) with brief planning (5 min).

---

### Deep Mode (4+ hours)
**Indicators:**
- 4+ files or new project
- Architecture decisions required
- Multiple components/integration
- Unclear or evolving requirements

**Examples:**
- "Build an e-commerce platform"
- "Refactor the authentication system"
- "Design a real-time chat feature"
- "Create a new mobile app"

**Action:** Full planning with multiple experts, phased execution.

## Quick Decision Tree

```
1. Is it a question about existing code?
   YES → Quick

2. Is it a single file change under 50 lines?
   YES → Quick

3. Does it require design/architecture decisions?
   YES → Go to 5

4. Does it span multiple modules or need coordination?
   YES → Deep
   NO → Normal

5. Is it a greenfield project or major refactor?
   YES → Deep
   NO → Normal
```

## Response Patterns

### Quick Response
```
This is a quick task. I'll handle it directly:

[Direct solution]

✅ Done (X seconds)
```

### Normal Response
```
This is a normal complexity task. I'll use [expert] mode:

Plan (5 min):
1. [Step 1]
2. [Step 2]
3. [Step 3]

[Execute...]

✅ Complete
```

### Deep Response
```
This is a complex project. I'll use deep mode with full planning:

📋 Phase 1: Requirements & Design
📋 Phase 2: Implementation
📋 Phase 3: Quality Assurance
📋 Phase 4: Deployment

[Begin Phase 1...]
```

## Context Awareness

The assessor considers:
- Current directory (is there a CLAUDE.md?)
- Git status (existing codebase vs new)
- File types in context
- User's historical preferences
- Recent conversation context

## Adaptation

If during execution complexity changes:
```
Started as Normal, but discovered:
- Requires database migration
- Needs API versioning
- Affects 5+ files

→ Escalating to Deep mode
```
