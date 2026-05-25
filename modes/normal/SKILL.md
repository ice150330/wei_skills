---
name: normal-mode
description: Standard execution mode for moderate tasks (10 minutes - 4 hours). Brief planning, 1-2 experts, focused execution.
triggers:
  - complexity: moderate
  - estimated_time: 10min-4hr
  - files_affected: 2-5
---

# Normal Mode

## Purpose

Balanced approach for single features or bug fixes. Brief planning, focused execution, minimal overhead.

## When to Use

- 1-3 files affected
- Single feature or component
- Clear requirements
- Existing codebase context
- Estimated 10 min - 4 hours

## Execution Flow

```
User Request
    ↓
5-Min Planning
    ↓
Load Expert(s)
    ↓
Execute
    ↓
Quick Review
    ↓
✅ Complete
```

## Response Pattern

```
This is a normal complexity task. Using [expert] mode:

Plan (5 min):
1. [Step 1]
2. [Step 2]
3. [Step 3]

[Execute...]

✅ Complete
```

## Expert Selection

| Task Type | Primary Expert | Secondary |
|-----------|---------------|-----------|
| UI component | Frontend | Designer |
| API endpoint | Backend | QA |
| Database query | Backend | Architect |
| Form validation | Frontend | QA |
| Bug fix | Domain expert | QA |

## Planning Template (5 minutes)

```
1. Understanding: What exactly needs to be done?
2. Approach: How will I do it?
3. Files: Which files will be modified?
4. Risks: What could go wrong?
```

## Rules

1. **Brief planning only** - 5 minutes max
2. **1-2 experts max** - No full team
3. **Focus on execution** - Less talk, more code
4. **Minimal documentation** - README update if needed
5. **Quick sanity check** - Self-review before completion

## Mode Transitions

### Escalate to Deep if:
- Files affected > 5
- Architecture decisions emerge
- Integration complexity discovered
- Timeline extends > 4 hours
- Requires > 2 experts

Escalation phrase: `⬆️ Escalating to Deep mode: [reason]`

### De-escalate to Quick if:
- Task simpler than expected
- Only 1 file affected
- Solution < 20 lines
- Completed in < 10 min

De-escalation phrase: `⬇️ Completing as Quick mode: [reason]`

## Examples

### ✅ Good Normal Tasks
- "Add email validation to the form"
- "Create a user list API"
- "Fix this React component bug"
- "Optimize this database query"
- "Add CSV export feature"

### ❌ Not for Normal Mode
- "Build an e-commerce platform" → Use Deep Mode
- "How do I print?" → Use Quick Mode
