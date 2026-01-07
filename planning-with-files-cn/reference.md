# Reference: Manus Context Engineering Principles (参考: Manus 上下文工程原则)

本 Skill 基于 Manus 的上下文工程原则,Manus 是一家 AI 代理公司,于 2024 年 12 月被 Meta 以 20 亿美元收购。

## Quick Reference (快速参考)

| Principle (原则) | Core Action (核心行动) | When to Use (适用场景) |
|---------|---------------|----------------|
| 1. Filesystem as External Memory (文件系统即外存) | 用 Write/Read 存储大内容,context 只保留路径 | 内容超过 500 tokens |
| 2. Attention Manipulation (注意力操控) | 每次决策前 Read task_plan.md | 超过 10 个 tool calls |
| 3. Keep Failure Traces (保留失败轨迹) | 在 task_plan.md 记录所有错误 | 遇到任何失败 |
| 4. Avoid Few-Shot Overfitting (避免少样本过拟合) | 变换措辞,不要机械复制 | 重复性任务 |
| 5. Stable Prefixes for Cache (稳定前缀优化缓存) | 静态内容放前面 | 所有任务 |
| 6. Append-Only Context (仅追加上下文) | 永远不修改历史消息 | 所有任务 |

---

## The 6 Manus Principles (6 大 Manus 原则)

### 1. Filesystem as External Memory (文件系统即外存)

> "Markdown is my 'working memory' on disk."
> "Markdown 是我在磁盘上的'工作记忆'。"

**Problem (问题):** Context windows have limits. Stuffing everything in context degrades performance and increases costs.
上下文窗口有限制。将所有内容塞入 context 会降低性能并增加成本。

**Solution (解决方案):** Treat the filesystem as unlimited memory:
将文件系统视为无限记忆:
- Store large content in files (将大内容存储到文件)
- Keep only paths in context (在上下文中只保留路径)
- Agent can "look up" information when needed (代理可以"查找"需要的信息)
- Compression must be REVERSIBLE (压缩必须是可逆的)

### 2. Attention Manipulation Through Repetition (通过重复操控注意力)

**Problem (问题):** After ~50 tool calls, models forget original goals ("lost in the middle" effect).
大约 50 次工具调用后,模型会忘记原始目标("中间迷失"效应)。

**Solution (解决方案):** Keep a `task_plan.md` file that gets RE-READ throughout execution:
保持一个 `task_plan.md` 文件,在整个执行过程中重复读取:
```
Start of context: [Original goal - far away, forgotten]
(上下文开始: [原始目标 - 遥远,已遗忘])
...many tool calls...
(...许多工具调用...)
End of context: [Recently read task_plan.md - gets ATTENTION!]
(上下文结束: [最近读取的 task_plan.md - 获得注意力!])
```

By reading the plan file before each decision, goals appear in the attention window.
通过在每次决策前读取计划文件,目标会出现在注意力窗口中。

### 3. Keep Failure Traces (保留失败轨迹)

> "Error recovery is one of the clearest signals of TRUE agentic behavior."
> "错误恢复是真实代理行为的最明显信号之一。"

**Problem (问题):** Instinct says hide errors, retry silently. This wastes tokens and loses learning.
本能说隐藏错误,静默重试。这会浪费 token 并失去学习机会。

**Solution (解决方案):** KEEP failed actions in the plan file:
在计划文件中保留失败的操作:
```markdown
## Errors Encountered (遇到的错误)
- [2025-01-03] FileNotFoundError: config.json not found → Created default config
- [2025-01-03] API timeout → Retried with exponential backoff, succeeded
```

The model updates its internal understanding when seeing failures.
模型在看到失败时会更新其内部理解。

### 4. Avoid Few-Shot Overfitting (避免少样本过拟合)

> "Uniformity breeds fragility."
> "一致性导致脆弱性。"

**Problem (问题):** Repetitive action-observation pairs cause drift and hallucination.
重复的行动-观察对会导致漂移和幻觉。

**Solution (解决方案):** Introduce controlled variation:
引入受控的变化:
- Vary phrasings slightly (稍微变化措辞)
- Don't copy-paste patterns blindly (不要盲目复制粘贴模式)
- Recalibrate on repetitive tasks (在重复性任务中重新校准)

### 5. Stable Prefixes for Cache Optimization (稳定前缀优化缓存)

**Problem (问题):** Agents are input-heavy (100:1 ratio). Every token costs money.
代理是输入密集型的 (100:1 比例)。每个 token 都要花钱。

**Solution (解决方案):** Structure for cache hits:
为缓存命中构建结构:
- Put static content FIRST (将静态内容放在前面)
- Append-only context (never modify history) (仅追加上下文,永不修改历史)
- Consistent serialization (一致的序列化)

### 6. Append-Only Context (仅追加上下文)

**Problem (问题):** Modifying previous messages invalidates KV-cache.
修改之前的消息会使 KV 缓存失效。

**Solution (解决方案):** NEVER modify previous messages. Always append new information.
永远不要修改之前的消息。始终追加新信息。

## The Agent Loop (代理循环)

Manus operates in a continuous loop:
Manus 在一个连续循环中运行:

```
1. Analyze (分析) → 2. Think (思考) → 3. Select Tool (选择工具) → 4. Execute (执行) → 5. Observe (观察) → 6. Iterate (迭代) → 7. Deliver (交付)
```

### File Operations in the Loop: (循环中的文件操作)

| Operation (操作) | When to Use (何时使用) |
|-----------|-------------|
| `write` (写入) | New files or complete rewrites (新文件或完全重写) |
| `append` (追加) | Adding sections incrementally (增量添加章节) |
| `edit` (编辑) | Updating specific parts (checkboxes, status) (更新特定部分:复选框、状态) |
| `read` (读取) | Reviewing before decisions (决策前审查) |

## Manus Statistics (Manus 统计数据)

| Metric (指标) | Value (值) |
|--------|-------|
| Average tool calls per task (平均每个任务的工具调用数) | ~50 |
| Input-to-output ratio (输入输出比) | 100:1 |
| Acquisition price (收购价格) | $2 billion (20 亿美元) |
| Time to $100M revenue (达到 1 亿美元收入的时间) | 8 months (8 个月) |

## Key Quotes (关键引言)

> "If the model improvement is the rising tide, we want Manus to be the boat, not the piling stuck on the seafloor."
> "如果模型改进是涨潮,我们希望 Manus 是船,而不是卡在海床上的桩。"

> "For complex tasks, I save notes, code, and findings to files so I can reference them as I work."
> "对于复杂任务,我将笔记、代码和发现保存到文件中,以便在工作中参考。"

> "I used file.edit to update checkboxes in my plan as I progressed, rather than rewriting the whole file."
> "我使用 file.edit 更新计划中的复选框,而不是重写整个文件。"

## Source (来源)

Based on Manus's official context engineering documentation:
基于 Manus 的官方上下文工程文档:
https://manus.im/de/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus
