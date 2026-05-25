---
name: coordinator
description: Expert coordinator. Manages communication between experts, resolves conflicts, and orchestrates collaborative tasks.
triggers:
  - experts_count: ">1"
  - mode: [normal, deep]
---

# Expert Coordinator

## Purpose

When multiple experts are active, coordinate their work and resolve conflicts.

## Communication Protocol

### Message Format

```yaml
message:
  from: expert_name      # 发送者
  to: expert_name | all  # 接收者
  type: request | response | broadcast
  priority: low | normal | high | critical
  content: string
  context:
    task_id: string
    phase: planning | implementation | quality | deployment
```

### Message Types

| Type | Use Case | Example |
|------|----------|---------|
| `request` | Ask another expert | PM asks Architect for API design |
| `response` | Reply to request | Architect responds with design |
| `broadcast` | Notify all experts | "Phase 1 complete" |
| `conflict` | Disagreement detected | PM vs Architect on scope |

## Conflict Resolution

### Conflict Types

```yaml
conflicts:
  scope:      # PM vs others
    resolver: pm  # PM has final say

  technical:  # Architect vs Dev
    resolver: architect  # Architect decides

  implementation:  # Dev vs QA
    resolver: discussion  # Discuss and agree

  priority:   # Any disagreement on order
    resolver: pm  # PM prioritizes
```

### Resolution Flow

```
Conflict Detected
       ↓
┌────────────────┐
│ Identify Type  │
└────────┬───────┘
         ↓
┌────────────────┐
│ Auto Resolve?  │
└────────┬───────┘
         ↓
    ┌────┴────┐
   Yes        No
    │          │
    ▼          ▼
 Apply Rule  Escalate
    │       to User
    └────┬─────┘
         ↓
   Record Decision
```

## Expert Activation Rules

```yaml
activation:
  # 顺序激活（某些专家需要等前一个完成）
  sequential:
    planning: [pm, architect, designer]
    implementation: [dev]
    quality: [qa]
    deployment: [devops]

  # 并行激活（可同时工作）
  parallel:
    implementation: [frontend, backend]  # 如果是分开的专家
    review: [architect, qa]  # 代码审查可以并行

  # 条件激活
  conditional:
    designer:
      if: "ui_changes > 0"
    devops:
      if: "deployment_required"
    qa:
      if: "code_changes > 50_lines"
```

## Handoff Protocol

When one expert finishes and another starts:

```yaml
handoff:
  from: pm
  to: architect
  deliverables:
    - requirements_doc
    - acceptance_criteria
    - constraints
  context:
    - user_preferences
    - technical_constraints
    - timeline
```

## Coordination in Different Modes

### Normal Mode (1-2 experts)
- Light coordination
- Direct communication
- User resolves conflicts

### Deep Mode (all experts)
- Full coordination
- Structured phases
- Auto conflict resolution
- Regular sync points

## Example: Deep Mode Coordination

```
Phase 1: Planning
  PM: Define requirements
    ↓ handoff
  Architect: Design system
    ↓ handoff
  Designer: Create UI
    ↓ sync
  [All planning experts sync]

Phase 2: Implementation
  Dev: Write code
    ↓ broadcast
  QA: Prepare tests (parallel)

Phase 3: Quality
  QA: Review and test
    ↓ request
  Dev: Fix issues

Phase 4: Deployment
  DevOps: Deploy
    ↓ broadcast
  [All experts notified]
```