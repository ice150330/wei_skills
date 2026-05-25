# Archived Skills

These skills were removed during v3.0 simplification.

## Removed Skills

| Skill | Reason | Replacement |
|-------|--------|-------------|
| `project-dev-workflow` | Redundant with deep mode | `modes/deep/` |
| `_core/complexity-assessor` | Renamed/updated | `assessor/` |
| `_workflows/simple` | Renamed | `modes/quick/` |
| `_workflows/standard` | Renamed | `modes/normal/` |
| `_workflows/full` | Renamed | `modes/deep/` |
| `_roles/frontend` | Merged | `experts/dev/` |
| `_roles/backend` | Merged | `experts/dev/` |
| `_roles/*` | Renamed | `experts/*` |
| `core-workflow` | Deprecated | Use modes |
| `code-quality` | Merged | `experts/qa/` |
| `safe-operations` | Merged | `experts/devops/` |
| `ui-ux-design` | Merged | `experts/designer/` |

## Why These Were Removed

1. **Too many layers** - 4 layers (_core → _workflows → _roles → plugins) simplified to 3 (assessor → modes → experts)
2. **Overlapping functionality** - project-dev-workflow duplicated modes/deep
3. **Unclear boundaries** - Frontend/Backend split unnecessary, merged to Dev
4. **Naming inconsistency** - Removed `_prefixes`, standardized names
5. **Documentation bloat** - Merged QUICK-START into README

## Migration

If you need any of these old skills, they're preserved here for reference.
Active development should use the new v3.0 structure.
