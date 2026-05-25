# 执行反馈机制

## 目的

记录任务执行情况，用于改进评估器准确度。

## 反馈记录

```yaml
feedback_record:
  task_id: unique_id
  timestamp: ISO8601

  # 评估信息
  assessment:
    initial_mode: quick | normal | deep
    confidence: 0.0-1.0
    factors:
      keyword_score: 0.0-1.0
      file_complexity: 0.0-1.0
      historical: 0.0-1.0

  # 实际执行
  execution:
    actual_mode: quick | normal | deep
    final_mode: quick | normal | deep  # 如果有切换
    files_affected: number
    lines_changed: number
    time_minutes: number
    experts_involved: [list]

  # 准确度评估
  accuracy:
    mode_correct: boolean  # 初始模式是否正确
    escalation_needed: boolean
    de_escalation_needed: boolean

  # 学习数据
  learning:
    # 哪些信号被低估了
    underestimated_signals: [keywords, file_types]
    # 哪些信号被高估了
    overestimated_signals: [keywords, file_types]
```

## 反馈收集时机

1. **任务完成时** - 记录实际vs评估
2. **模式切换时** - 记录切换原因
3. **用户纠正时** - 用户说"这个太复杂了"

## 应用到评估器

```python
# 伪代码
def calculate_confidence(request):
    base_score = keyword_analysis(request)

    # 应用历史学习
    similar_tasks = find_similar_historical_tasks(request)
    for task in similar_tasks:
        if task.accuracy.mode_correct:
            base_score *= 1.1  # 更信任
        else:
            base_score *= 0.9  # 降低权重

    return normalize(base_score)
```

## 定期优化

每月运行一次分析：

```bash
# 生成准确度报告
$ skills-admin analyze-accuracy

# 输出示例
Quick mode accuracy: 92%
Normal mode accuracy: 78%
Deep mode accuracy: 85%

Recommendations:
- Lower threshold for Normal → Deep
- "refactor" keyword weight: 0.6 → 0.75
```
