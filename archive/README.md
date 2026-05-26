# 归档技能

这些技能是在 v3.0 简化过程中移出活跃路由的旧版内容，仅作为历史参考保留。

## 3.2 路由说明

`archive/` 下的内容不参与当前 `3.2` 技能路由。当前活跃架构以 `registry.yaml` 为准：

```
root-directives → assessor → modes → experts
```

如需恢复旧技能，必须先迁移到当前目录结构并更新 `registry.yaml`。

## 已移除技能

| 旧技能 | 移除原因 | 当前替代 |
|--------|----------|----------|
| `project-dev-workflow` | 与 Deep Mode 重复 | `modes/deep/` |
| `_core/complexity-assessor` | 已重命名并升级 | `assessor/` |
| `_workflows/simple` | 已重命名 | `modes/quick/` |
| `_workflows/standard` | 已重命名 | `modes/normal/` |
| `_workflows/full` | 已重命名 | `modes/deep/` |
| `_roles/frontend` | 已合并 | `experts/dev/` |
| `_roles/backend` | 已合并 | `experts/dev/` |
| `_roles/*` | 已重命名 | `experts/*` |
| `core-workflow` | 已废弃 | 使用 `modes/` |
| `code-quality` | 已合并 | `experts/qa/` |
| `safe-operations` | 已合并 | `experts/devops/` |
| `ui-ux-design` | 已合并 | `experts/designer/` |

## 移除原因

1. 层级过多：旧架构层级复杂，当前架构简化为 `root-directives → assessor → modes → experts`。
2. 功能重叠：`project-dev-workflow` 与 `modes/deep` 重复。
3. 边界不清：Frontend/Backend 拆分对当前工作流不是必需，已合并到 Dev。
4. 命名不一致：移除 `_prefix` 风格，统一目录名。
5. 文档膨胀：把快速入口合并到主 README。

## 迁移原则

如果需要引用旧技能，请只把必要规则迁移到当前活跃技能中，不要直接把归档目录重新加入路由。
