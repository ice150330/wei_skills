---
name: simple-workflow
description: Lightweight workflow for simple tasks (Level 2 complexity). Use this for single-module changes, small features, or minor improvements. Involves 1-2 roles and skips heavy planning. Perfect for tasks that take 1-2 hours and affect 2-5 files.
triggers:
  complexity: moderate
  auto_trigger: true
---

# Simple Workflow

> ⚡ **轻量级工作流** - 适用于简单任务，1-2个角色，快速执行

## 适用场景

- 单一功能开发
- 2-5个文件修改
- 现有模块扩展
- 小型优化任务

## 角色组合

根据任务类型，自动选择1-2个角色：

| 任务类型 | 角色组合 |
|----------|----------|
| 前端组件 | Frontend + Designer |
| API开发 | Backend + QA |
| Bug修复 | QA + (Frontend/Backend) |
| 代码重构 | QA + (相关开发者) |
| 设计优化 | Designer + Frontend |

## 工作流程

```
用户: "给登录页面添加验证码"
    ↓
[自动识别] 前端任务 → Frontend + QA
    ↓
Frontend: 实现验证码组件
    ├── 调用 frontend-design 技能
    ├── 调用 code-quality (TDD)
    └── 输出: 组件代码
    ↓
QA: 快速审查
    ├── 调用 code-review --mode quick
    └── 输出: 审查意见
    ↓
✅ 完成
```

## 执行步骤

### 1. 快速分析 (1-2分钟)
```
- 理解需求
- 识别涉及文件
- 确定技术方案
- 无需详细文档
```

### 2. 实现 (主要时间)
```
- 编写代码
- 单元测试 (TDD)
- 简单注释
```

### 3. 快速审查 (2-3分钟)
```
- code-review --mode quick
- 检查明显问题
- 安全合规检查
```

### 4. 完成
```
- 简要总结
- 提交代码
- 标记完成
```

## 输出物

- ✅ 代码实现
- ✅ 单元测试
- ✅ 简要审查报告
- ❌ 无详细设计文档
- ❌ 无架构文档
- ❌ 无完整计划

## 时间预算

| 阶段 | 时间 |
|------|------|
| 分析 | 1-2分钟 |
| 实现 | 30-60分钟 |
| 审查 | 2-3分钟 |
| **总计** | **1-2小时** |

## 示例

### 示例1: 添加表单验证
```
用户: "给注册表单添加邮箱格式验证"

分析: 前端单文件修改
角色: Frontend + QA

Frontend:
  - 添加验证函数
  - 更新表单组件
  - 编写测试

QA:
  - code-review --mode quick
  - 边界条件检查

✅ 完成
```

### 示例2: 优化查询
```
用户: "优化这个慢查询"

分析: 后端单点优化
角色: Backend + QA

Backend:
  - 分析查询
  - 添加索引
  - 优化SQL

QA:
  - 性能测试
  - 回归测试

✅ 完成
```
