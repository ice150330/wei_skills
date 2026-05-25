---
name: core-workflow
description: 核心工作流程技能 - 从任务规划到完成交付的完整流程，包括任务拆分、设计探索、计划编写、执行和完成
triggers:
  keywords:
    - "plan"
    - "计划"
    - "implement"
    - "实现"
    - "开发"
    - "feature"
    - "功能"
    - "project"
    - "项目"
    - "task"
    - "任务"
    - "design"
    - "设计"
    - "architecture"
    - "架构"
    - "execute"
    - "执行"
    - "finish"
    - "完成"
    - "new project"
    - "新项目"
    - "workflow"
    - "流程"
  priority: high
auto_trigger: true
---

# Core Workflow

> 🔄 **自动触发提示**: 当检测到复杂任务、项目启动或需要工作流程管理时，此技能会自动应用。

## 自动触发场景

| 触发词 | 应用原则 |
|--------|----------|
| "plan", "计划", "project", "项目" | Task Planning: 四象限优先级评估 |
| "design", "设计", "架构" | Brainstorming: 设计探索流程 |
| "execute", "执行", "开始开发" | Plan Execution: 选择执行模式 |
| "finish", "完成", "merge" | Finishing: 完成开发流程 |

## 工作流程决策树

```
接收任务
    ↓
复杂? → Task Planning → 拆分、四象限评估
    ↓
需要设计? → Brainstorming → 获得用户批准
    ↓
有书面计划? → 选择执行模式
    ├── 复杂/有依赖 → same-session
    └── 简单/独立 → parallel-session
    ↓
完成? → Finishing → 4个选项
```

---

## 快速启动

## 快速启动

### 接收新任务时

```
任务复杂? → 自动触发任务规划 → 拆分、优先级评估
    ↓
需要设计? → brainstorming → 获得用户批准
    ↓
有书面计划? → 执行计划
    ├── 复杂/有依赖 → same-session 模式
    └── 简单/独立 → parallel-session 模式
```

## 核心流程

### 1. 任务规划 (Task Planning)

**触发条件：**
- 多步骤或子任务需求
- 多文件/多模块开发
- 需要设计或方案选择

**四象限优先级评估：**
```
        重要
          │
    P0    │    P1
  (紧急)  │  (不紧急)
──────────┼──────────
    P2    │    P3
  (紧急)  │  (不紧急)
          │
        不重要
```

**执行前必问：**
1. 是否有更好的解决方案？
2. 是否有拓展空间？
3. 是否有理解不确定的地方？
4. 是否有多种实现路径需要确认？

### 2. 设计探索 (Brainstorming)

**硬性规则：** 未经设计批准，不得开始编码

**流程：**
1. 探索项目上下文
2. 一次一个问题澄清
3. 提出 2-3 种方案
4. 分阶段呈现设计
5. 保存到 `docs/plans/YYYY-MM-DD-<topic>-design.md`
6. 调用 writing-plans

### 3. 计划编写 (Writing Plans)

**计划头部模板：**
```markdown
# [Feature Name] Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans

**Goal:** [一句话描述]

**Architecture:** [2-3句方法描述]

**Tech Stack:** [关键技术/库]

---
```

**任务结构：**
- 精确的文件的绝对路径
- 完整的代码示例
- 确切的命令和预期输出
- DRY、YAGNI、TDD、频繁提交

### 4. 计划执行 (Plan Execution)

**Same-Session 模式（精细）：**
- 每个任务后两阶段审查（spec + quality）
- 发现问题立即修复
- 适合复杂、有依赖的任务

**Parallel-Session 模式（高效）：**
- 批量执行（默认3个任务）
- 检查点报告进度
- 适合独立任务

### 5. 完成开发 (Finishing)

**4个选项：**
1. 本地合并 → 清理worktree
2. 创建PR → 保持worktree
3. 保持现状 → 保持worktree
4. 丢弃 → 需要输入"discard"确认 → 清理worktree

### 6. Git Worktrees

**目录选择优先级：**
1. `.worktrees/`（如果存在）
2. `worktrees/`（如果存在）
3. CLAUDE.md 中的偏好
4. 询问用户

**安全验证：**
```bash
git check-ignore -q .worktrees  # 必须已忽略
```

## 检查点规则

### 每个Task后
- [ ] 实现完成
- [ ] 测试通过
- [ ] 代码审查通过
- [ ] 提交完成
- [ ] TodoWrite 更新

### 每个批次后
- [ ] 显示实现内容
- [ ] 显示验证输出
- [ ] 说 "Ready for feedback"
- [ ] 等待用户反馈

### 完成前
- [ ] 完整测试套件通过
- [ ] 最终代码审查
- [ ] 验证无敏感信息
- [ ] 提交信息规范
