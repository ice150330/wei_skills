---
name: safe-operations
description: 安全操作技能 - 安全删除、Git提交检查和Worktree使用规范，防止数据丢失和安全事故
triggers:
  keywords:
    - "delete"
    - "删除"
    - "remove"
    - "移除"
    - "rm -rf"
    - "del"
    - "rmdir"
    - "Remove-Item"
    - "commit"
    - "提交"
    - "git add"
    - "push"
    - "worktree"
    - "工作树"
  priority: critical
auto_trigger: true
---

# Safe Operations

> ⚠️ **自动触发提示**: 当检测到删除操作、Git提交或Worktree操作时，此技能会自动应用安全规范。

## 自动触发场景

| 触发词 | 应用原则 |
|--------|----------|
| "delete", "删除", "rm -rf" | Safe Delete: 安全检查清单 |
| "commit", "提交", "push" | Git Commit Check: 8步检查流程 |
| "worktree", "工作树" | Worktree Safety: 验证.gitignore |

## 安全红线

**🔴 极高风险（禁止自动执行）:**
- `robocopy /mir` 删除文件
- `rm -rf /` 或 `C:\`
- `Remove-Item -Recurse -Force`

**删除前必须:**
- [ ] 确认路径正确
- [ ] 确认不是当前目录
- [ ] 确认不包含.git
- [ ] 确认已备份/推送

---

## 1. Safe Delete

## 1. Safe Delete

### 🔴 极高风险（禁止自动执行）

```bash
# 绝对禁止
robocopy <source> <dest> /mir           # 镜像同步删除
rm -rf /                                # 删除根目录
rm -rf C:\                             # 删除C盘
del /f /s /q C:\                        # Windows强制删除
Remove-Item -Recurse -Force <path>      # PowerShell强制删除
```

### 强制检查清单

删除前必须确认：
- [ ] 确认目标路径是否正确
- [ ] 确认是否为当前工作目录
- [ ] 确认路径是否包含重要目录（.git等）
- [ ] 确认是否已备份或可恢复
- [ ] 对于Git仓库，确认已推送所有更改

### 特殊文件名

Windows 系统保留设备名，**绝对不能**删除：
```
CON, PRN, AUX, NUL, COM1-9, LPT1-9
```

### Git 仓库特殊保护

```bash
# 1. 检查仓库状态
git status

# 2. 确认所有更改已提交
git add .
git commit -m "备份当前工作"
git push

# 3. 确认远程是最新的
git diff origin/main

# 4. 然后才能安全删除
```

## 2. Git Commit Check

### 提交前8步检查

- [ ] 确认当前所在分支
- [ ] 检查未暂存的更改（git status）
- [ ] 检查更改内容（git diff）
- [ ] 确认只提交了预期的文件
- [ ] 验证没有提交敏感信息
- [ ] 确认提交信息清晰明确
- [ ] 测试更改是否正常工作
- [ ] 确认可以推送到远程仓库

### 绝对不能提交

```
.env, .env.local, .env.production
node_modules/, venv/, __pycache__/
dist/, build/, target/
*.log, logs/
.DS_Store, Thumbs.db
```

### 提交信息规范（Conventional Commits）

```
<type>(<scope>): <subject>

type: feat, fix, docs, style, refactor, test, chore
```

## 3. Git Worktrees

### 目录选择优先级

1. `.worktrees/`（如果存在）
2. `worktrees/`（如果存在）
3. CLAUDE.md 中的偏好
4. 询问用户

### 安全验证（强制）

项目本地目录必须验证已被忽略：

```bash
git check-ignore -q .worktrees  # 检查是否被忽略

# 如未忽略，立即修复
echo ".worktrees/" >> .gitignore
git add .gitignore && git commit -m "chore: ignore worktrees"
```

### 创建流程

```
1. 检测项目名称
2. 确定完整路径
3. 创建worktree
4. 运行项目设置（npm install等）
5. 验证干净基线（运行测试）
6. 报告位置
```

## 安全红线

### 绝对禁止
- [ ] 执行 `robocopy /mir` 删除文件
- [ ] 删除根目录 `/` 或 `C:\`
- [ ] 使用通配符删除 `rm -rf *`
- [ ] 提交敏感信息到Git
- [ ] 提交 `.env` 文件
- [ ] 提交 `node_modules/`
- [ ] 创建worktree前不验证.gitignore

### 必须始终执行
- [ ] 删除前检查路径和内容
- [ ] 提交前检查敏感信息
- [ ] 项目本地worktree验证被忽略
- [ ] 创建worktree后验证测试基线
