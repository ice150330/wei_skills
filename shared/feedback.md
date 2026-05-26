# 执行反馈机制

## 目的

记录任务执行情况，用于改进评估器准确度。

## 反馈记录

```yaml
feedback_record:
  task_id: unique_id
  timestamp: ISO8601

  assessment:
    initial_mode: quick | normal | deep
    confidence: 0.0-1.0
    factors:
      keyword_score: 0.0-1.0
      file_complexity: 0.0-1.0
      historical: 0.0-1.0

  execution:
    actual_mode: quick | normal | deep
    final_mode: quick | normal | deep
    files_affected: number
    lines_changed: number
    time_minutes: number
    experts_involved: [list]

  accuracy:
    mode_correct: boolean
    escalation_needed: boolean
    de_escalation_needed: boolean

  learning:
    underestimated_signals: [keywords, file_types]
    overestimated_signals: [keywords, file_types]
```

## 反馈收集时机

1. **任务完成时**：记录实际复杂度和初始评估的差异。
2. **模式切换时**：记录升级或降级原因。
3. **用户纠正时**：记录用户指出的复杂度判断偏差。

## 应用到评估器

```python
# 伪代码
def calculate_confidence(request):
    base_score = keyword_analysis(request)

    similar_tasks = find_similar_historical_tasks(request)
    for task in similar_tasks:
        if task.accuracy.mode_correct:
            base_score *= 1.1
        else:
            base_score *= 0.9

    return normalize(base_score)
```

## 定期优化

每月运行一次分析：

```bash
skills-admin analyze-accuracy
```

输出示例：

```text
Quick mode accuracy: 92%
Normal mode accuracy: 78%
Deep mode accuracy: 85%

Recommendations:
- Lower threshold for Normal → Deep
- "refactor" keyword weight: 0.6 → 0.75
```
