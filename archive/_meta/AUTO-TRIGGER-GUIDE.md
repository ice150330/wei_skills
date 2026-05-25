# 技能自动触发器使用指南

## 概述

Claude 现在配备了智能技能触发器系统，能够根据你的输入、当前文件和项目上下文自动识别并应用合适的技能。

## 触发器工作原理

```
你的输入 / 操作
    ↓
[触发器引擎] 分析上下文
    ├── 关键词匹配
    ├── 文件类型检测
    ├── Git状态分析
    └── 意图识别
    ↓
[技能选择器] 选择合适技能
    ├── 按优先级排序
    ├── 去重处理
    └── 组合优化
    ↓
[技能应用] 自动应用原则
    ↓
继续正常响应
```

## 触发器响应格式

当技能被自动触发时，你会看到：

```
🎯 自动触发 <skill-name> 技能

原因: <触发原因>
将应用的原则:
- <原则1>
- <原则2>
...
---
```

## 各技能触发场景

### 1. code-quality（代码质量）

**自动触发场景:**

| 场景 | 触发词示例 | 应用原则 |
|------|------------|----------|
| 🐛 Bug修复 | "fix bug", "修复bug", "debug", "错误" | Systematic Debugging: 四阶段调试流程 |
| 🧪 测试开发 | "test", "测试", ".test.js" | TDD: 红-绿-重构循环 |
| 🔍 代码审查 | "review", "审查", "优化代码" | Code Review: 三模式审查 |
| ✅ 完成声明 | "完成了", "done", "测试通过" | Verification: 验证门函数 |

**示例:**
```
你: 修复这个登录bug

🐛 自动触发 code-quality 技能

原因: 检测到 "fix bug" 关键词
将应用的原则:
- 先进行根本原因调查，再尝试修复
- 遵循四阶段调试流程
- 编写失败测试用例验证修复
---

Claude: 我将使用系统化调试流程来修复这个bug...
```

---

### 2. safe-operations（安全操作）

**自动触发场景:**

| 场景 | 触发词示例 | 应用原则 |
|------|------------|----------|
| ⚠️ 删除操作 | "delete", "删除", "rm -rf", "remove" | Safe Delete: 安全检查清单 |
| 📦 Git提交 | "commit", "提交", "push", "git add" | Git Commit Check: 8步检查流程 |
| 🌲 Worktree | "worktree", "工作树", "隔离工作区" | Worktree Safety: 验证.gitignore |

**示例:**
```
你: 删除这个旧目录

⚠️ 自动触发 safe-operations 技能

原因: 检测到删除操作
将应用的原则:
- 执行安全检查清单
- 确认路径和内容
- 验证备份和恢复选项
---

Claude: 在执行删除前，让我进行安全检查...
```

---

### 3. core-workflow（核心工作流程）

**自动触发场景:**

| 场景 | 触发词示例 | 应用原则 |
|------|------------|----------|
| 📋 任务规划 | "plan", "计划", "project", "项目" | Task Planning: 四象限优先级 |
| 🎨 设计阶段 | "design", "设计", "架构", "方案" | Brainstorming: 设计探索流程 |
| ⚙️ 执行开发 | "execute", "执行", "开始实现" | Plan Execution: 模式选择 |
| 🏁 完成工作 | "finish", "完成", "merge", "PR" | Finishing: 完成开发流程 |

**示例:**
```
你: 帮我计划一个新功能开发

📋 自动触发 core-workflow 技能

原因: 检测到 "plan" + "新功能" 关键词
将应用的原则:
- 任务拆分与四象限优先级评估
- 设计探索与方案选择
- 详细的实施计划编写
---

Claude: 我将使用核心工作流程来规划这个新功能...
```

---

### 4. ui-ux-design（UI/UX设计）

**自动触发场景:**

| 场景 | 触发词/文件 | 应用原则 |
|------|-------------|----------|
| 🎨 设计任务 | "UI", "界面", "design", "设计" | Design System: 生成设计系统 |
| 💻 前端文件 | ".jsx", ".tsx", ".vue", ".css" | Frontend Stack: 技术栈指南 |
| 🧩 组件开发 | "component", "组件", "page" | UI Components: 组件规范 |
| 📱 移动适配 | "mobile", "app", "响应式" | Responsive Design: 响应式原则 |

**示例:**
```
你: 创建一个登录页面组件

🎨 自动触发 ui-ux-design 技能

原因: 检测到 "创建" + "组件" + "页面"
将应用的原则:
- 生成设计系统（配色、字体、间距）
- 遵循组件设计规范
- 应用交付前检查清单
---

Claude: 我将使用UI/UX设计技能来创建这个组件...
```

---

## 复合触发场景

某些场景会触发多个技能的组合：

### 🔧 Bug修复工作流
```
触发词: "fix bug", "修复bug"

触发的技能组合:
1. code-quality → Systematic Debugging
2. code-quality → TDD
3. safe-operations → Git Commit Check
```

### 🚀 新功能开发
```
触发词: "new feature", "新功能"

触发的技能组合:
1. core-workflow → Task Planning
2. code-quality → TDD
3. safe-operations → Worktree Safety
```

### 🎨 UI开发
```
触发词: "build UI", "创建组件"

触发的技能组合:
1. ui-ux-design → Design System
2. code-quality → TDD
3. code-quality → Code Review
```

---

## 用户控制

### 查看当前激活的技能

```
/active-skills
```

### 手动触发技能

```
/use skill <skill-name>

例如:
/use skill code-quality
/use skill safe-operations
/use skill core-workflow
/use skill ui-ux-design
```

### 临时禁用自动触发

```
/disable-auto-trigger <skill-name>
/disable-auto-trigger code-quality
```

### 重新启用自动触发

```
/enable-auto-trigger <skill-name>
/enable-auto-trigger code-quality
```

### 查看触发器配置

```
/trigger-config
```

---

## 触发器优先级

| 优先级 | 技能 | 场景 |
|--------|------|------|
| 🔴 Critical | safe-operations | 删除操作、危险命令 |
| 🟠 High | code-quality | Bug修复、代码审查 |
| 🟡 High | core-workflow | 复杂任务、项目规划 |
| 🟢 Medium | ui-ux-design | UI开发、设计任务 |

---

## 自适应学习

系统会学习你的工作习惯：

- **经常使用的技能**: 提高触发优先级
- **经常跳过的技能**: 降低触发频率
- **自定义模式**: 识别你的工作模式并优化

---

## 最佳实践

### ✅ 推荐的交互方式

```
# 清晰的意图表达
"修复登录页面的bug"
"创建一个新的用户管理功能"
"设计一个数据分析仪表盘"
"帮我审查这段代码"

# 系统会自动:
# 1. 识别你的意图
# 2. 触发合适的技能
# 3. 应用相应的原则
```

### ❌ 避免的模糊表达

```
"弄一下这个"
"改改这里"
"看看这个"

# 模糊的表达可能导致:
# 1. 无法准确识别意图
# 2. 错过最佳技能匹配
# 3. 需要额外澄清
```

---

## 故障排除

### 技能没有触发?

1. 检查关键词是否匹配
2. 使用 `/use skill <name>` 手动触发
3. 检查触发器是否被禁用

### 技能触发太频繁?

1. 使用 `/disable-auto-trigger <skill>` 临时禁用
2. 系统会学习并自动调整触发阈值

### 想要跳过当前触发的技能?

直接说: "跳过这个技能" 或 "不需要应用这些原则"

---

## 配置文件

触发器配置位于:
```
~/.claude/skills/triggers.yaml
```

你可以编辑此文件来自定义触发规则。

---

## 更新日志

- **v1.0** (2026-04-10)
  - 初始版本发布
  - 4个核心技能自动触发
  - 复合场景支持
  - 用户控制命令
