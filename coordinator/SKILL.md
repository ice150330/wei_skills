---
name: coordinator
description: 专家协调器，负责多专家通信、冲突解决和协作编排。
triggers:
  - experts_count: ">1"
  - mode: [normal, deep]
---

# 专家协调器

## 目的

当多个专家同时参与任务时，协调工作边界、交接信息和冲突处理，避免重复劳动或方向不一致。

## 通信协议

### 消息格式

```yaml
message:
  from: expert_name      # 发送者
  to: expert_name | all  # 接收者
  type: request | response | broadcast | conflict
  priority: low | normal | high | critical
  content: string
  context:
    task_id: string
    phase: planning | implementation | quality | deployment
```

### 消息类型

| Type | 使用场景 | 示例 |
|------|----------|------|
| `request` | 请求其他专家输入 | PM 请求 Architect 给出 API 设计 |
| `response` | 回复请求 | Architect 返回设计方案 |
| `broadcast` | 通知所有专家 | “阶段 1 已完成” |
| `conflict` | 发现分歧 | PM 与 Architect 对范围判断不同 |

## 冲突解决

### 冲突类型

```yaml
conflicts:
  scope:
    resolver: pm
  technical:
    resolver: architect
  implementation:
    resolver: discussion
  priority:
    resolver: pm
```

| 冲突类型 | 默认处理者 | 原则 |
|----------|------------|------|
| 范围冲突 | PM | 以用户目标和验收标准为准 |
| 技术冲突 | Architect | 以架构一致性和长期维护为准 |
| 实现冲突 | 讨论达成一致 | 以简单、可验证、低风险为准 |
| 优先级冲突 | PM | 以用户价值和阻塞关系为准 |

### 处理流程

```
发现冲突
   ↓
识别类型
   ↓
能否按规则自动解决？
   ↓
是 → 应用规则 → 记录决定
否 → 向用户澄清 → 记录决定
```

## 专家激活规则

```yaml
activation:
  sequential:
    planning: [pm, architect, designer]
    implementation: [dev]
    quality: [qa]
    deployment: [devops]

  parallel:
    implementation: [frontend, backend]
    review: [architect, qa]

  conditional:
    designer:
      if: "ui_changes > 0"
    devops:
      if: "deployment_required"
    qa:
      if: "code_changes > 50_lines"
```

## 交接协议

一个专家完成、另一个专家开始时，应保留必要上下文：

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

## 不同模式下的协调

### Normal Mode（1-2 个专家）

- 轻量协调。
- 直接交接。
- 分歧优先由用户确认。

### Deep Mode（多专家）

- 分阶段协调。
- 明确质量门禁。
- 按冲突规则自动处理可确定的问题。
- 在关键节点同步。

## Deep Mode 协调示例

```
阶段 1：规划
  PM：明确需求
    ↓ 交接
  Architect：设计系统
    ↓ 交接
  Designer：设计 UI
    ↓ 同步
  [规划专家同步]

阶段 2：实现
  Dev：编写代码
    ↓ 广播
  QA：并行准备测试

阶段 3：质量
  QA：审查和测试
    ↓ 请求
  Dev：修复问题

阶段 4：部署
  DevOps：部署
    ↓ 广播
  [通知所有专家]
```
