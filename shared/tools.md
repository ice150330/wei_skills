# 共享工具

所有技能都可以复用的通用工具能力。

## 文件操作

- `read_file(path)`：读取文件并保留行号。
- `write_file(path, content)`：原子写入文件。
- `edit_file(path, old, new)`：精确替换内容。
- `find_files(pattern)`：按 glob 模式查找文件。
- `search_content(pattern)`：按内容搜索。

## 代码操作

- `parse_ast(code)`：按语言解析语法树。
- `format_code(code)`：自动格式化代码。
- `lint_check(code)`：运行静态检查。

## Git 操作

- `git_status()`：查看当前工作区状态。
- `git_diff()`：查看改动差异。
- `git_log(n)`：查看最近提交。

## 沟通操作

- `ask_user(questions)`：向用户询问澄清问题。
- `notify(message)`：向用户报告进展。
- `confirm(action)`：在高风险操作前确认。

## 结构审阅

- `check_project_structure()`：检查 `docs/plans`、`docs/reports`、`config`、`scripts`、`tests` 和入口说明文件是否符合当前任务需要。
- `choose_file_location(type)`：根据文件类型选择正确目录，避免堆到根目录。
