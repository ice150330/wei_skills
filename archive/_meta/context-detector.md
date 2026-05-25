# 智能上下文检测器

## 概述

上下文检测器分析当前项目状态、文件内容、用户历史等，为触发器提供精准的上下文信息。

## 检测维度

### 1. 项目类型检测

```python
def detect_project_type():
    """基于文件检测项目类型"""

    indicators = {
        'nodejs': ['package.json', 'node_modules'],
        'python': ['requirements.txt', 'pyproject.toml', 'setup.py', 'Pipfile'],
        'rust': ['Cargo.toml', 'Cargo.lock'],
        'go': ['go.mod', 'go.sum'],
        'java': ['pom.xml', 'build.gradle'],
        'dotnet': ['*.csproj', '*.sln'],
        'ruby': ['Gemfile', '*.gemspec'],
        'php': ['composer.json'],
    }

    # 返回检测到的项目类型列表
    return detected_types
```

### 2. 当前文件上下文

```python
def analyze_current_file():
    """分析当前活动文件"""

    context = {
        'extension': get_file_extension(),
        'type': classify_file_type(),  # code, test, config, doc
        'language': detect_language(),
        'is_test_file': is_test_file(),
        'is_config': is_config_file(),
        'lines': count_lines(),
        'has_errors': check_syntax_errors(),
    }

    return context
```

### 3. Git 状态检测

```python
def analyze_git_status():
    """分析Git仓库状态"""

    status = {
        'is_git_repo': check_git_repo(),
        'branch': get_current_branch(),
        'has_changes': has_uncommitted_changes(),
        'changed_files': get_changed_files(),
        'has_conflicts': has_merge_conflicts(),
        'ahead_behind': get_ahead_behind(),
        'last_commit_time': get_last_commit(),
    }

    return status
```

### 4. 开发阶段检测

```python
def detect_dev_phase():
    """检测当前开发阶段"""

    # 基于最近操作和文件状态判断
    phases = {
        'planning': ['创建计划文件', '编写设计文档'],
        'development': ['修改代码', '添加功能'],
        'testing': ['运行测试', '修复bug'],
        'review': ['代码审查', 'PR创建'],
        'deployment': ['合并分支', '推送代码'],
    }

    return current_phase
```

## 上下文映射到技能

### 上下文 → 技能映射表

| 上下文 | 推荐技能 | 触发概率 |
|--------|----------|----------|
| 修改 .test.js 文件 | code-quality (TDD) | 100% |
| 运行测试失败 | code-quality (Debugging) | 100% |
| 删除操作 | safe-operations | 100% |
| git commit | safe-operations | 100% |
| 新建项目 | core-workflow | 90% |
| 修改 .jsx/.tsx | ui-ux-design | 80% |
| 创建组件 | ui-ux-design | 90% |
| Bug报告 | code-quality | 90% |
| 代码完成声明 | code-quality | 90% |
| 复杂任务描述 | core-workflow | 80% |

### 智能组合触发

```python
def smart_skill_combination():
    """基于上下文组合技能"""

    context = gather_context()

    # Bug修复场景
    if context['intent'] == 'bug_fix':
        return [
            ('code-quality', 'systematic_debugging'),
            ('code-quality', 'tdd'),
            ('safe-operations', 'git_commit_check'),
        ]

    # 新功能开发
    if context['intent'] == 'new_feature':
        return [
            ('core-workflow', 'planning'),
            ('code-quality', 'tdd'),
            ('safe-operations', 'worktree_safety'),
        ]

    # UI开发
    if context['intent'] == 'ui_development':
        return [
            ('ui-ux-design', 'design_system'),
            ('code-quality', 'code_review'),
        ]

    # 代码重构
    if context['intent'] == 'refactoring':
        return [
            ('code-quality', 'code_review'),
            ('code-quality', 'tdd'),
            ('safe-operations', 'git_commit_check'),
        ]
```

## 意图识别

### 基于NLP的意图分类

```python
class IntentClassifier:
    """用户意图分类器"""

    intents = {
        'bug_fix': {
            'keywords': ['fix', 'bug', 'error', 'crash', '修复', '错误'],
            'patterns': [r'fix\s+\w+', r'修复\w+', r'解决\w+问题'],
        },
        'new_feature': {
            'keywords': ['add', 'new', 'feature', 'implement', '添加', '实现', '新功能'],
            'patterns': [r'add\s+\w+', r'实现\w+', r'新功能'],
        },
        'ui_development': {
            'keywords': ['UI', 'design', 'component', 'page', '界面', '设计', '组件'],
            'patterns': [r'create\s+\w+\s+component', r'设计\w+页面'],
        },
        'refactoring': {
            'keywords': ['refactor', 'clean up', 'improve', '重构', '优化'],
            'patterns': [r'refactor\s+\w+', r'重构\w+'],
        },
        'testing': {
            'keywords': ['test', 'testing', 'spec', '测试', '用例'],
            'patterns': [r'add\s+test', r'测试\w+'],
        },
        'deployment': {
            'keywords': ['deploy', 'push', 'commit', '发布', '提交', '推送'],
            'patterns': [r'git\s+push', r'提交代码'],
        },
    }

    def classify(self, user_input):
        """分类用户输入意图"""
        # 返回最匹配的意图和置信度
        return intent, confidence
```

## 历史学习

### 用户偏好学习

```python
def learn_user_preferences():
    """学习用户偏好"""

    preferences = {
        'preferred_workflow': detect_preferred_workflow(),
        'skipped_triggers': get_skipped_triggers(),
        'custom_patterns': detect_custom_patterns(),
        'trigger_threshold': calculate_optimal_threshold(),
    }

    return preferences
```

### 自适应调整

```python
def adapt_triggers():
    """基于历史调整触发器"""

    # 如果用户经常跳过某个触发器，降低其优先级
    for trigger in triggers:
        skip_rate = calculate_skip_rate(trigger)
        if skip_rate > 0.7:
            lower_priority(trigger)

    # 如果用户经常使用某个技能，提高其优先级
    for skill in skills:
        usage_rate = calculate_usage_rate(skill)
        if usage_rate > 0.8:
            raise_priority(skill)
```

## 上下文缓存

### 会话上下文

```python
session_context = {
    'started_at': timestamp,
    'project_type': detected_type,
    'active_skills': [],
    'recent_files': [],
    'recent_operations': [],
    'user_preferences': {},
}
```

### 上下文更新策略

```python
def update_context(event):
    """根据事件更新上下文"""

    if event.type == 'file_change':
        session_context['recent_files'].append(event.file)
        session_context['recent_files'] = keep_last_n(10)

    if event.type == 'skill_trigger':
        session_context['active_skills'].append(event.skill)
        session_context['recent_operations'].append({
            'skill': event.skill,
            'timestamp': now(),
            'success': event.success,
        })
```

## 使用示例

### 场景1: 用户说 "修复登录bug"

```python
context = {
    'intent': 'bug_fix',
    'confidence': 0.95,
    'git_status': {'has_changes': True},
    'current_file': 'auth.js',
}

# 触发的技能组合
triggered = [
    ('code-quality', 'systematic_debugging'),
    ('code-quality', 'tdd'),
]
```

### 场景2: 用户修改 .test.js 文件

```python
context = {
    'file_type': 'test',
    'extension': '.test.js',
    'project_type': 'nodejs',
}

# 触发的技能
triggered = [
    ('code-quality', 'tdd'),
]
```

### 场景3: 用户执行 `rm -rf`

```python
context = {
    'operation': 'delete',
    'risk_level': 'critical',
    'path': 'node_modules',
}

# 立即触发安全技能
triggered = [
    ('safe-operations', 'safe_delete'),
]
```
