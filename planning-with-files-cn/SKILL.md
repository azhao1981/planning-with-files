---
name: planning-with-files-cn
description: 使用 Manus 风格的持久化 Markdown 文件进行规划、进度跟踪和知识管理。适用于复杂任务、多步骤项目、研究任务,或当用户提到 planning(规划)、organizing work(组织工作)、tracking progress(跟踪进度)、structured output(结构化输出)、file-based planning(基于文件的规划)、制定计划、项目管理、任务组织时触发。
---

# 基于文件的规划

像 Manus 一样工作: 使用持久化 Markdown 文件作为"磁盘上的工作记忆"。

## Quick Start (快速开始)

在任何复杂任务之前:

1. **Create `task_plan.md`** 在工作目录中创建计划文件
2. **Define phases** 定义阶段并使用复选框
3. **Update after each phase** 每个阶段后标记 [x] 并更新状态
4. **Read before deciding** 决策前读取以刷新目标到注意力窗口

## The 3-File Pattern (三文件模式)

对于任何非平凡任务,创建三个文件:

| File (文件) | Purpose (用途) | When to Update (更新时机) |
|------|---------|----------------|
| `task_plan.md` | 跟踪阶段和进度 | 每个阶段完成后 |
| `notes.md` | 存储发现和研究 | 研究过程中 |
| `[deliverable].md` | 最终输出 | 完成时 |

## Core Workflow (核心工作流)

```
Loop 1: Create task_plan.md with goal and phases
Loop 2: Research → save to notes.md → update task_plan.md
Loop 3: Read notes.md → create deliverable → update task_plan.md
Loop 4: Deliver final output
```

### The Loop in Detail (循环详解)

**Before each major action:** (每次重大行动前)
```bash
Read task_plan.md  # Refresh goals in attention window (刷新目标到注意力窗口)
```

**After each phase:** (每个阶段后)
```bash
Edit task_plan.md  # Mark [x], update status (标记完成,更新状态)
```

**When storing information:** (存储信息时)
```bash
Write notes.md     # Don't stuff context, store in file (不要塞满上下文,存储到文件)
```

## task_plan.md Template (任务计划模板)

对于任何复杂任务,首先创建此文件:

```markdown
# Task Plan: [Brief Description] (简短描述)

## Goal (目标)
[One sentence describing the end state] (一句话描述最终状态)

## Phases (阶段)
- [ ] Phase 1: Plan and setup (规划和设置)
- [ ] Phase 2: Research/gather information (研究/收集信息)
- [ ] Phase 3: Execute/build (执行/构建)
- [ ] Phase 4: Review and deliver (审查和交付)

## Key Questions (关键问题)
1. [Question to answer] (要回答的问题)
2. [Question to answer] (要回答的问题)

## Decisions Made (已做的决策)
- [Decision]: [Rationale] ([决策]: [理由])

## Errors Encountered (遇到的错误)
- [Error]: [Resolution] ([错误]: [解决方案])

## Status (状态)
**Currently in Phase X** - [What I'm doing now] (当前在第 X 阶段 - [正在做什么])
```

## notes.md Template (笔记模板)

用于研究和发现:

```markdown
# Notes: [Topic] (主题)

## Sources (来源)

### Source 1: [Name] (名称)
- URL: [link] (链接)
- Key points: (关键点)
  - [Finding] (发现)
  - [Finding] (发现)

## Synthesized Findings (综合发现)

### [Category] (类别)
- [Finding] (发现)
- [Finding] (发现)
```

## Critical Rules (关键规则)

### 1. ALWAYS Create Plan First (始终先创建计划)
永远不要在没有 `task_plan.md` 的情况下开始复杂任务。这是不可协商的。

### 2. Read Before Decide (决策前先读取)
在任何重大决策之前,读取计划文件。这能将目标保持在你的注意力窗口中。

### 3. Update After Act (行动后更新)
完成任何阶段后,立即更新计划文件:
- 用 [x] 标记完成的阶段
- 更新状态部分
- 记录遇到的任何错误

### 4. Store, Don't Stuff (存储,不要塞满)
大内容放入文件,而不是上下文。只在工作记忆中保留路径。

### 5. Log All Errors (记录所有错误)
每个错误都放入"遇到的错误"部分。这能为未来的任务积累知识。

## When to Use This Pattern (何时使用此模式)

**Use 3-file pattern for:** (对以下情况使用三文件模式)
- Multi-step tasks (3+ steps) (多步骤任务)
- Research tasks (研究任务)
- Building/creating something (构建/创建某物)
- Tasks spanning multiple tool calls (跨越多次工具调用的任务)
- Anything requiring organization (任何需要组织的工作)

**Skip for:** (以下情况跳过)
- Simple questions (简单问题)
- Single-file edits (单文件编辑)
- Quick lookups (快速查询)

## Anti-Patterns to Avoid (避免的反模式)

| Don't (不要) | Do Instead (而是) |
|-------|------------|
| Use TodoWrite for persistence (用 TodoWrite 持久化) | Create `task_plan.md` file (创建计划文件) |
| State goals once and forget (陈述一次目标后就忘) | Re-read plan before each decision (每次决策前重读计划) |
| Hide errors and retry (隐藏错误并重试) | Log errors to plan file (记录错误到计划文件) |
| Stuff everything in context (把所有内容塞入上下文) | Store large content in files (将大内容存储到文件) |
| Start executing immediately (立即开始执行) | Create plan file FIRST (首先创建计划文件) |

## Advanced Patterns (高级模式)

See [reference.md](reference.md) for: (参见 reference.md 了解)
- Attention manipulation techniques (注意力操控技巧)
- Error recovery patterns (错误恢复模式)
- Context optimization from Manus (Manus 的上下文优化)

See [examples.md](examples.md) for: (参见 examples.md 了解)
- Real task examples (真实任务示例)
- Complex workflow patterns (复杂工作流模式)
