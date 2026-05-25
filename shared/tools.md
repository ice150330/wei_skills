# Shared Tools

Common utilities used across all skills.

## File Operations

- `read_file(path)` - Read with line numbers
- `write_file(path, content)` - Atomic write
- `edit_file(path, old, new)` - Precise replacement
- `find_files(pattern)` - Glob search
- `search_content(pattern)` - Grep search

## Code Operations

- `parse_ast(code)` - Language-aware parsing
- `format_code(code)` - Auto-formatting
- `lint_check(code)` - Static analysis

## Git Operations

- `git_status()` - Current state
- `git_diff()` - Changes
- `git_log(n)` - Recent commits

## Communication

- `ask_user(questions)` - Get clarification
- `notify(message)` - Inform user
- `confirm(action)` - Safe confirmation
