# 技能自动触发器引擎

## 概述

触发器引擎根据用户输入、文件类型、操作上下文自动识别并触发合适的技能。

## 触发器类型

### 1. 关键词触发器 (Keyword Trigger)

基于用户消息中的关键词匹配。

**匹配模式：**
- 精确匹配
- 前缀匹配
- 包含匹配
- 正则表达式

**示例：**
```yaml
- type: keyword
  patterns:
    - "bug"
    - "fix"
    - "debug"
  action: apply_systematic_debugging
```

### 2. 文件类型触发器 (File Extension Trigger)

基于文件扩展名匹配。

**示例：**
```yaml
- type: file_extension
  extensions: [".test.js", ".test.ts"]
  action: apply_tdd
```

### 3. 复合触发器 (Composite Trigger)

多个条件组合触发，执行多个技能。

**示例：**
```yaml
- type: composite
  conditions:
    - type: keyword
      patterns: ["fix bug"]
  actions:
    - skill: code-quality
      action: apply_systematic_debugging
    - skill: safe-operations
      action: apply_git_commit_check
```

## 触发器执行流程

```
接收用户输入
    ↓
解析上下文（当前文件、项目类型、历史操作）
    ↓
匹配触发器规则
    ↓
按优先级排序
    ↓
去重处理
    ↓
执行触发的技能
    ↓
应用技能指导原则
    ↓
继续正常响应
```

## 优先级系统

| 优先级 | 说明 | 示例场景 |
|--------|------|----------|
| critical | 关键安全操作 | 删除文件、危险命令 |
| high | 重要质量保障 | Bug修复、代码审查 |
| medium | 一般开发辅助 | UI设计、工作流程 |
| low | 可选建议 | 优化建议、最佳实践 |

## 上下文感知

### 检测的上下文信息

1. **当前文件类型**
   - 代码文件 (.js, .ts, .py, etc.)
   - 测试文件 (.test.js, .spec.ts, etc.)
   - 配置文件 (.json, .yaml, .toml, etc.)
   - 文档文件 (.md, .txt, etc.)

2. **项目类型**
   - Node.js (package.json)
   - Python (requirements.txt, pyproject.toml)
   - Rust (Cargo.toml)
   - Go (go.mod)

3. **当前Git状态**
   - 是否有未提交的更改
   - 当前分支
   - 是否有冲突

4. **历史操作**
   - 最近执行的任务
   - 最近使用的技能
   - 用户的偏好设置

## 触发器响应模板

### 自动触发提示

当技能被自动触发时，使用以下格式：

```
[技能图标] 自动触发 <skill-name> 技能

原因: <触发原因>
将应用的原则:
- <原则1>
- <原则2>
...

---
```

### 示例

**Bug修复触发：**
```
🐛 自动触发 code-quality 技能

原因: 检测到 "fix bug" 关键词
将应用的原则:
- 先进行根本原因调查，再尝试修复
- 编写失败测试用例（TDD）
- 验证修复后才声明完成

---
```

**删除操作触发：**
```
⚠️ 自动触发 safe-operations 技能

原因: 检测到删除操作
将应用的原则:
- 执行安全检查清单
- 确认路径和内容
- 验证备份和恢复选项

---
```

## 用户控制

### 禁用自动触发

用户可以通过以下方式禁用自动触发：

```
/disable-auto-trigger <skill-name>
/disable-all-triggers
```

### 手动触发

用户可以随时手动触发技能：

```
/use skill <skill-name>
```

### 触发器建议

当系统认为某个技能可能有帮助但未达到自动触发阈值时：

```
💡 建议使用 <skill-name> 技能
原因: <原因>
是否应用? [是/否]
```

## 触发器优化

### 学习机制

系统会记录：
- 哪些触发器被频繁使用
- 哪些触发器被用户跳过
- 用户对触发器的反馈

### 自适应调整

根据使用模式调整：
- 触发阈值
- 优先级
- 响应方式

## 实现注意事项

1. **性能考虑**
   - 触发器匹配应该快速
   - 避免复杂的正则表达式
   - 使用缓存避免重复解析

2. **准确性**
   - 避免误触发
   - 提供明确的触发原因
   - 允许用户覆盖

3. **透明度**
   - 始终告知用户触发了什么技能
   - 解释为什么触发
   - 显示将应用什么原则
