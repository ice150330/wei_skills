---
name: full-workflow
description: Complete 7-role workflow for complex projects (Level 3 complexity). Use this for new product development, large-scale refactoring, or multi-module systems. Involves all roles: PM, Architect, Designer, Frontend, Backend, QA, and DevOps. Perfect for projects that take multiple days to weeks.
triggers:
  complexity: complex
  auto_trigger: true
---

# Full Workflow (7-Role)

> 🏗️ **完整工作流** - 适用于复杂项目，全部7个角色协作

## 适用场景

- 全新项目开发
- 大型系统重构
- 多模块协调
- 架构级别变更
- 需要完整规划的项目

## 完整角色团队

```
┌─────────────────────────────────────────────┐
│              Full Development Team           │
├──────────┬──────────┬──────────┬────────────┤
│ 🎯 PM    │ 🏗️ Arch  │ 🎨 Design│ ⚡ Frontend│
├──────────┼──────────┼──────────┼────────────┤
│ 🔧 Backend│ 🧪 QA    │ 🚀 DevOps│            │
└──────────┴──────────┴──────────┴────────────┘
```

## 四阶段流程

### Phase 1: 规划 (Planning)

**参与**: PM → Architect → Designer

**时长**: 2-4小时

**输出**:
- PRD文档
- 架构设计文档
- API规范
- 设计系统

**调用技能**:
- core-workflow (规划)
- ui-ux-design (设计系统)

### Phase 2: 开发 (Development)

**参与**: Frontend + Backend (并行) + QA (并行测试)

**时长**: 1-5天

**输出**:
- 前端代码
- 后端代码
- 单元测试
- 集成测试

**调用技能**:
- frontend-design (前端实现)
- code-quality (TDD)
- code-simplifier (优化)

### Phase 3: 质量保证 (Quality)

**参与**: QA主导，所有开发者配合

**时长**: 4-8小时

**输出**:
- QA报告
- 修复记录
- 性能报告

**调用技能**:
- code-review --mode deep
- code-quality (调试)
- safe-operations (安全检查)

### Phase 4: 部署 (Deployment)

**参与**: DevOps + 全员配合

**时长**: 2-4小时

**输出**:
- CI/CD配置
- 部署文档
- 运维手册

**调用技能**:
- safe-operations (部署安全)
- core-workflow (完成流程)

## 完整流程图

```
Day 1: Planning
├── AM: PM - 需求分析
├── PM: Architect - 架构设计
└── EOD: Designer - 设计系统

Day 2-3: Development
├── Frontend - 界面实现
├── Backend - API开发
└── QA - 并行测试

Day 4: Quality
├── code-review (deep mode)
├── 性能测试
├── 安全扫描
└── Bug修复

Day 5: Deployment
├── CI/CD配置
├── 生产部署
├── 监控配置
└── 项目交付
```

## 输出物清单

### 文档
- ✅ PRD文档
- ✅ 架构设计文档
- ✅ API规范
- ✅ 设计系统文档
- ✅ 部署文档
- ✅ 运维手册

### 代码
- ✅ 前端源码
- ✅ 后端源码
- ✅ 测试代码 (单元+集成+E2E)
- ✅ 基础设施代码

### 报告
- ✅ QA质量报告
- ✅ 性能测试报告
- ✅ 安全扫描报告
- ✅ 代码审查报告

## 时间预算

| 阶段 | 时间 |
|------|------|
| 规划 | 0.5-1天 |
| 开发 | 1-5天 |
| 质量保证 | 0.5-1天 |
| 部署 | 0.5天 |
| **总计** | **3-7天** |

## 使用条件

必须满足以下任一条件才使用Full Workflow：

- [ ] 全新项目启动
- [ ] 涉及5+个模块
- [ ] 架构级别变更
- [ ] 需要完整设计系统
- [ ] 多技术栈协调
- [ ] 预计工期 > 3天
