# claude code Skills v3.2

> 根本指令驱动架构：**root-directives → assessor → mode → experts**

## 核心变更 (v3.1 → v3.2)

1. **统一中文化** — 活跃技能文件的标题、说明、流程、模板统一使用中文
2. **新增目录审阅检查** — 新建项目或改造工作流前先检查必备目录和入口文件
3. **补齐必备结构** — skills 工作流增加 docs、config、scripts、tests 等标准目录
4. **强化工作流校验** — 明确版本一致性、路由路径、目录结构和文档格式检查

## 历史变更 (v3.0 → v3.1)

1. **新增 root-directives** — 每次对话优先加载，确保中文优先、项目结构规范、技能智能路由
2. **增强 assessor** — 增加中文关键词匹配
3. **registry 增加中文关键词** — 支持中英文双向触发

## 三大根本指令

| 指令 | 内容 | 优先级 |
|------|------|--------|
| 🌐 语言规则 | 全程中文（对话、注释、报告、终端输出） | 绝对 |
| 📁 项目结构 | 文件归入对应目录，不放根目录 | 高 |
| 🧠 技能路由 | 每次对话评估并选择合适技能 | 高 |

## 架构

```
skills/
├── root-directives/       # 🔴 根本指令（每次对话加载）
│   └── SKILL.md          # 中文优先、项目结构、技能路由
├── assessor/              # 📊 复杂度评估（每次对话加载）
│   └── SKILL.md
├── modes/
│   ├── quick/            # ⚡ 简单模式（<10分钟）
│   ├── normal/           # 📋 标准模式（10分钟-4小时）
│   └── deep/             # 🏗️ 深度模式（4小时+）
├── experts/
│   ├── pm/               # 🎯 产品经理
│   ├── architect/        # 🏗️ 系统架构师
│   ├── designer/         # 🎨 UI/UX 设计师
│   ├── dev/              # ⚡ 开发专家
│   ├── qa/               # 🧪 质量保证
│   └── devops/           # 🚀 运维专家
├── coordinator/           # 🔄 多专家协调器
├── shared/               # 共享工具和模式
└── archive/               # 旧版归档
```

## 执行流程

```
用户请求
    ↓
🔴 root-directives（确保中文、项目结构、技能匹配）
    ↓
📊 assessor（评估复杂度：简单/中等/复杂）
    ↓
┌────────┼────────┐
⚡ quick  📋 normal  🏗️ deep
(直接)   (1-2专家)  (全专家+规划)
    ↓        ↓          ↓
   ✅ 完成  ✅ 完成    ✅ 完成
```

## 技能匹配快速参考

| 用户说... | 触发技能 |
|-----------|----------|
| 任何请求 | root-directives + assessor |
| 需求/规划 | task-planner, pm-expert |
| 设计/架构 | architect-expert, brainstorming |
| 写代码 | dev-expert, plan-execution |
| 调试/Bug | systematic-debugging |
| 代码审查 | code-quality |
| 测试 | test-driven-development |
| UI/界面 | designer-expert, ui-ux-pro-max |
| 部署 | devops-expert |
| 提交代码 | git-commit-check |
| 删除文件 | safe-delete |

## 中文关键词支持

所有技能触发支持中英文关键词：
- 需求/requirement → pm-expert
- 架构/architecture → architect-expert
- 实现/implement → dev-expert
- 测试/test → qa-expert
- 部署/deploy → devops-expert

---

*Version: 3.2 | 架构: 根本指令驱动 | 更新: 2026-05-26*