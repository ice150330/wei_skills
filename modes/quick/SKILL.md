---
name: quick-mode
description: Quick execution mode for simple tasks under 10 minutes. No planning, no coordination, direct execution.
triggers:
  - complexity: simple
  - estimated_time: <10min
  - files_affected: 1
---

# Quick Mode

## Purpose

Zero-overhead execution for trivial tasks. No planning, no coordination, no documentation.

## When to Use

- Single command or question
- Under 20 lines of code
- Existing solution available
- No design decisions needed
- One file affected

## Execution Flow

```
User Request → Direct Execution → ✅ Done
```

## Response Pattern

```
This is a quick task. I'll handle it directly:

[Direct solution]

✅ Done (X seconds)
```

## Rules

1. **No planning** - Execute immediately
2. **No experts** - Use your own capability
3. **No documentation** - Beyond minimal inline comments
4. **No tests** - Unless explicitly requested
5. **Single action** - No branching workflows

## Escalation Triggers

During execution, escalate to Normal mode if:
- Files affected > 1
- Execution time > 10 minutes
- User asks follow-up requiring new files
- Complexity discovered higher than expected

Escalation phrase: `⬆️ Escalating to Normal mode: [reason]`

## Examples

### ✅ Good Quick Tasks
- "How to print in Python?"
- "Fix this typo"
- "Run the tests"
- "Explain this error"
- "Format this file"

### ❌ Not for Quick Mode
- "Add user authentication"
- "Design a database schema"
- "Refactor the codebase"

## Output Format

Keep responses minimal:
- Code: Just the fix
- Questions: Direct answer
- Errors: Root cause + fix
- No meta-commentary about the process
