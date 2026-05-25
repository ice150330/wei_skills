---
name: code-quality
description: 代码质量保证技能 - TDD、系统化调试、代码审查和完成前验证，确保高质量代码交付
triggers:
  keywords:
    - "bug"
    - "fix"
    - "debug"
    - "错误"
    - "修复"
    - "调试"
    - "test"
    - "测试"
    - "TDD"
    - "review"
    - "审查"
    - "完成了"
    - "做好了"
    - "done"
    - "test fail"
    - "测试失败"
  file_extensions:
    - ".test.js"
    - ".test.ts"
    - ".test.py"
    - ".spec.js"
    - ".spec.ts"
    - ".spec.py"
  priority: high
auto_trigger: true
---

# Code Quality

> 🔧 **自动触发提示**: 当检测到调试、测试、Bug修复或完成声明时，此技能会自动应用。

## 自动触发场景

| 触发词 | 应用原则 |
|--------|----------|
| "fix bug", "修复bug", "debug" | Systematic Debugging: 先找根因再修复 |
| "test", "测试", ".test.js" | TDD: 红-绿-重构循环 |
| "review", "审查" | Code Review: 三模式审查 |
| "完成了", "done", "测试通过" | Verification: 验证门函数 |

## 三大铁律

## 三大铁律

```
┌─────────────────────────────────────────────────────────┐
│  NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST        │
├─────────────────────────────────────────────────────────┤
│  NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST        │
├─────────────────────────────────────────────────────────┤
│  NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION        │
└─────────────────────────────────────────────────────────┘
```

## 1. Test-Driven Development (TDD)

### 红-绿-重构循环

```
RED → Verify RED → GREEN → Verify GREEN → REFACTOR → Next
 │        │           │           │            │
写失败测试  观看失败    最小实现     确认通过      清理代码
(强制)              (强制)
```

### RED 阶段要求
- 一个行为
- 清晰的测试名
- 真实代码（非mock，除非不可避免）

### 红旗（立即停止，删除代码，重新开始）
- 测试在实现后立即通过
- "先实现再补测试"
- "保持代码作为参考"
- "这次特殊情况"

## 2. Systematic Debugging

### 四阶段流程

**Phase 1: 根本原因调查**
- 阅读错误信息
- 稳定复现
- 检查最近变更
- 多组件系统：每层添加诊断
- 追踪数据流到源头

**Phase 2: 模式分析**
- 找到工作示例
- 对比参考实现
- 识别差异

**Phase 3: 假设与测试**
- 形成单一假设
- 最小化测试
- 验证后再继续

**Phase 4: 实现**
- 创建失败测试用例
- 单一修复
- 验证修复

⚠️ **3+ 修复失败 = 停止，质疑架构**

## 3. Code Review

### 三种模式

| 模式 | 代理数 | 耗时 | 适用场景 |
|------|--------|------|----------|
| quick | 1 | 10-30s | 小改动（<20行） |
| standard | 2 | 30-60s | 常规功能开发 |
| deep | 4 | 60-120s | 关键模块、安全敏感 |

### 置信度评分

| 分数 | 含义 | 处理 |
|------|------|------|
| 90-100 | 必须修复 | 立即修复 |
| 80-89 | 强烈建议修复 | 优先修复 |
| 60-79 | 值得考虑 | 可选修复 |
| <80 | 已过滤 | 忽略 |

### 与开发流程集成

```
[完成Task N]
    ↓
[运行 /review --diff]
    ↓
[有任何 Critical/Important 问题?]
    ├─ 是 → [修复] → [重新审查] → [验证通过]
    ↓
[继续 Task N+1]
```

## 4. Verification Before Completion

### 验证门函数

```
1. IDENTIFY: 什么命令能证明这个声明?
2. RUN: 执行完整命令（全新、完整）
3. READ: 完整输出，检查退出码，统计失败数
4. VERIFY: 输出是否确认声明?
5. ONLY THEN: 做出声明（带证据）
```

### 常见声明的验证要求

| 声明 | 需要 |
|------|------|
| 测试通过 | 测试命令输出：0 failures |
| Linter干净 | Linter输出：0 errors |
| 构建成功 | 构建命令：exit 0 |
| Bug已修复 | 测试原始症状：passes |

### 红旗（立即停止）
- 使用 "should", "probably", "seems to"
- 在验证前表达满意（"Great!", "Done!"）
- 未验证就提交/推送/PR
- 信任代理成功报告
