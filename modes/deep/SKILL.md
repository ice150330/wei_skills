---
name: deep-mode
description: Deep execution mode for complex tasks (4+ hours). Full planning, all 7 experts, phased execution with quality gates.
triggers:
  - complexity: complex
  - estimated_time: 4hr+
  - files_affected: 5+
---

# Deep Mode

## Purpose

Comprehensive approach for complex projects. Full planning, expert collaboration, phased execution with quality gates.

## When to Use

- 4+ files or new project
- Architecture decisions required
- Multiple components/integration
- Unclear or evolving requirements
- Estimated 4+ hours

## Execution Flow

```
User Request
    ↓
Phase 1: Requirements & Design (PM, Architect, Designer)
    ↓
Phase 2: Implementation (Frontend, Backend, QA parallel)
    ↓
Phase 3: Quality Assurance (QA deep review)
    ↓
Phase 4: Deployment (DevOps)
    ↓
✅ Complete
```

## Response Pattern

```
This is a complex project. Using Deep Mode with full planning:

📋 Phase 1: Requirements & Design
   🎯 PM: Clarify requirements
   🏗️ Architect: Design system
   🎨 Designer: Create UI/UX

📋 Phase 2: Implementation
   ⚡ Frontend: Build UI
   🔧 Backend: Build API
   🧪 QA: Write tests

📋 Phase 3: Quality Assurance
   🧪 QA: Code review & testing

📋 Phase 4: Deployment
   🚀 DevOps: Deploy to production

[Begin Phase 1...]
```

## Phase Details

### Phase 1: Requirements & Design

**Duration:** 30-60 minutes
**Experts:** PM, Architect, Designer

```
PM outputs:
- Feature specification
- User stories
- Acceptance criteria

Architect outputs:
- System design
- API contracts
- Database schema

Designer outputs:
- Wireframes
- Design system
- Mockups (if needed)
```

### Phase 2: Implementation

**Duration:** Variable based on scope
**Experts:** Frontend, Backend, QA

```
Parallel work streams:
- Frontend: Component development
- Backend: API implementation
- QA: Test case preparation

Sync points:
- API contract validation
- Integration testing
```

### Phase 3: Quality Assurance

**Duration:** 20% of total time
**Experts:** QA

```
Activities:
- Code review
- Unit/integration testing
- Security review
- Performance check
```

### Phase 4: Deployment

**Duration:** 30-60 minutes
**Experts:** DevOps

```
Activities:
- Environment setup
- CI/CD pipeline
- Monitoring configuration
- Rollback plan
```

## Expert Coordination

### Communication Flow

```
PM ↔ Architect ↔ Designer
     ↕
Frontend ↔ Backend
     ↕
    QA
     ↕
  DevOps
```

### Sync Points

1. **After Phase 1** - Design review with all experts
2. **Mid Phase 2** - Integration checkpoint
3. **Before Phase 3** - Feature complete review
4. **Before Phase 4** - Go/no-go decision

## Rules

1. **Complete planning first** - No jumping to code
2. **Document everything** - ADRs, API docs, README
3. **Quality gates** - Each phase must complete before next
4. **Regular sync** - Don't let experts work in silos
5. **User checkpoints** - Confirm direction at key points

## Mode Transitions

### De-escalate to Normal if:
- Task simpler than initial assessment
- Clear solution emerges early
- No architecture changes needed
- Can be completed by 1-2 experts
- Timeline < 4 hours

De-escalation phrase: `⬇️ Switching to Normal mode: [reason]`

### Reassess if:
- Scope significantly changes
- New requirements emerge
- Technical blockers found
- Timeline estimates were wrong

Reassessment phrase: `🔄 Reassessing complexity...`

## Examples

### ✅ Good Deep Tasks
- "Build an e-commerce platform"
- "Refactor the authentication system"
- "Design a real-time chat feature"
- "Create a new mobile app"
- "Migrate to microservices"

### ❌ Not for Deep Mode
- "Fix this bug" → Use Normal Mode
- "How do I..." → Use Quick Mode
