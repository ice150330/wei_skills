# 遗留技能 (Legacy Skills)

## 说明

此目录包含旧版技能，保持兼容性。新架构将逐步取代这些技能。

## 技能列表

| 旧技能 | 新替代 | 状态 |
|--------|--------|------|
| `core-workflow` | `standard-workflow` / `full-workflow` | 可用，建议迁移 |
| `code-quality` | 整合进各角色工作流程 | 可用，建议迁移 |
| `safe-operations` | 整合进 DevOps/QA 角色 | 可用，建议迁移 |
| `ui-ux-design` | `designer` 角色 | 可用，建议迁移 |
| `project-dev-workflow` | `full-workflow` | 可用，建议迁移 |

## 迁移指南

### 旧用法
```
/use skill project-dev-workflow
```

### 新用法
```
# 让系统自动选择
"开发一个电商平台"
→ 自动选择 full-workflow

# 或手动指定
/use skill full-workflow
```

## 兼容性保证

- ✅ 旧技能仍然可用
- ✅ 现有触发器继续工作
- ⚠️ 新功能优先在新架构实现
- 📅 旧技能将在 v3.0 后逐步淘汰

## 建议

新项目建议使用新架构：
- `_core/complexity-assessor` - 复杂度评估
- `_workflows/simple|standard|full` - 分层工作流
- `_roles/*` - 独立角色
