---
name: standard-workflow
description: Standard workflow for moderate complexity tasks (Level 2-3). Use this for feature development that spans multiple components but doesn't require full architecture redesign. Involves 3-4 roles: typically PM for requirements, one or two developers for implementation, and QA for testing. Perfect for tasks that take half a day to 2 days.
triggers:
  complexity: moderate-to-complex
  auto_trigger: true
---

# Standard Workflow

> 🎯 **标准工作流** - 适用于中等复杂度任务，3-4个角色协作

## 适用场景

- 新功能开发
- 多组件协调
- 小型项目
- 模块重构

## 角色组合

固定包含：PM + Developer(s) + QA

| 任务类型 | 角色组合 |
|----------|----------|
| 前端功能 | PM + Frontend + Designer + QA |
| 后端功能 | PM + Backend + Architect + QA |
| 全栈功能 | PM + Frontend + Backend + QA |
| 设计系统 | PM + Designer + Frontend + QA |

## 工作流程

```
用户: "开发一个用户资料管理功能"
    ↓
Phase 1: 需求澄清 (PM, 5分钟)
    - 快速确认需求
    - 确定范围边界
    - 输出: 简要需求清单
    ↓
Phase 2: 设计 (Developer + Designer, 15分钟)
    - 界面设计 (如需要)
    - API设计
    - 数据模型
    ↓
Phase 3: 开发 (Frontend + Backend, 2-4小时)
    - 并行开发
    - TDD模式
    - 持续集成
    ↓
Phase 4: 质量保证 (QA, 30分钟)
    - code-review --mode standard
    - 功能测试
    - 集成测试
    ↓
✅ 完成
```

## 输出物

- ✅ 简要需求文档 (1页)
- ✅ API/接口定义
- ✅ 代码实现
- ✅ 测试用例
- ✅ 审查报告
- ⚠️ 可选: 设计稿
- ❌ 无完整架构文档

## 时间预算

| 阶段 | 时间 |
|------|------|
| 需求 | 5-10分钟 |
| 设计 | 15-30分钟 |
| 开发 | 2-8小时 |
| 测试 | 30-60分钟 |
| **总计** | **4小时-2天** |

## 与Simple的区别

| 维度 | Simple | Standard |
|------|--------|----------|
| 角色数 | 1-2 | 3-4 |
| PM参与 | 否 | 是 |
| 设计阶段 | 无 | 有 |
| 文档 | 无 | 简要 |
| 审查 | Quick | Standard |
| 时间 | 1-2小时 | 半天-2天 |
