# 遗留技能说明

## 说明

此目录包含旧版技能，仅用于历史参考和迁移对照。自 `3.2` 起，归档内容不参与当前技能路由。

## 当前活跃架构

```
root-directives → assessor → modes → experts
```

活跃技能以 `C:\Users\39574\.claude\skills\registry.yaml` 为准。

## 技能列表

| 旧技能 | 新替代 | 状态 |
|--------|--------|------|
| `core-workflow` | `modes/normal` 或 `modes/deep` | 归档，仅参考 |
| `code-quality` | `experts/qa` | 归档，仅参考 |
| `safe-operations` | `experts/devops` | 归档，仅参考 |
| `ui-ux-design` | `experts/designer` | 归档，仅参考 |
| `project-dev-workflow` | `modes/deep` | 归档，仅参考 |

## 迁移指南

### 旧用法

```
/use skill project-dev-workflow
```

### 当前用法

```
开发一个电商平台
→ root-directives → assessor → deep-mode → experts
```

## 兼容性说明

- 归档文件保留历史内容，便于查阅。
- 新功能只在当前活跃架构中实现。
- 不应把 `archive/` 作为 3.2 路由来源。
- 若确需恢复旧能力，先迁移到 `modes/` 或 `experts/`，再更新 `registry.yaml`。

## 建议

新任务统一使用当前架构：
- `root-directives`：中文优先、目录审阅、技能路由。
- `assessor`：复杂度评估。
- `modes/quick|normal|deep`：执行模式。
- `experts/*`：按需启用专家角色。
