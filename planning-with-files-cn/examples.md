# Examples: Planning with Files in Action (示例: 基于文件的规划实践)

## Example 1: Research Task (示例 1: 研究任务)

**User Request:** "Research the benefits of morning exercise and write a summary"
**用户请求:** "研究晨练的好处并写一份总结"

### Loop 1: Create Plan (循环 1: 创建计划)
```bash
Write task_plan.md
```

```markdown
# Task Plan: Morning Exercise Benefits Research (晨练好处研究)

## Goal (目标)
Create a research summary on the benefits of morning exercise.
创建一份关于晨练好处的研究总结。

## Phases (阶段)
- [ ] Phase 1: Create this plan ✓ (创建此计划)
- [ ] Phase 2: Search and gather sources (搜索和收集来源)
- [ ] Phase 3: Synthesize findings (综合发现)
- [ ] Phase 4: Deliver summary (交付总结)

## Key Questions (关键问题)
1. What are the physical health benefits? (身体健康好处有哪些?)
2. What are the mental health benefits? (心理健康好处有哪些?)
3. What scientific studies support this? (有哪些科学研究支持?)

## Status (状态)
**Currently in Phase 1** - Creating plan (当前在第 1 阶段 - 创建计划)
```

### Loop 2: Research (循环 2: 研究)
```bash
Read task_plan.md           # Refresh goals (刷新目标)
WebSearch "morning exercise benefits"
Write notes.md              # Store findings (存储发现)
Edit task_plan.md           # Mark Phase 2 complete (标记第 2 阶段完成)
```

### Loop 3: Synthesize (循环 3: 综合)
```bash
Read task_plan.md           # Refresh goals (刷新目标)
Read notes.md               # Get findings (获取发现)
Write morning_exercise_summary.md
Edit task_plan.md           # Mark Phase 3 complete (标记第 3 阶段完成)
```

### Loop 4: Deliver (循环 4: 交付)
```bash
Read task_plan.md           # Verify complete (验证完成)
Deliver morning_exercise_summary.md
```

---

## Example 2: Bug Fix Task (示例 2: Bug 修复任务)

**User Request:** "Fix the login bug in the authentication module"
**用户请求:** "修复认证模块中的登录 bug"

### task_plan.md
```markdown
# Task Plan: Fix Login Bug (修复登录 Bug)

## Goal (目标)
Identify and fix the bug preventing successful login.
识别并修复阻止成功登录的 bug。

## Phases (阶段)
- [x] Phase 1: Understand the bug report ✓ (理解 bug 报告)
- [x] Phase 2: Locate relevant code ✓ (定位相关代码)
- [ ] Phase 3: Identify root cause (CURRENT) (识别根本原因 - 当前)
- [ ] Phase 4: Implement fix (实施修复)
- [ ] Phase 5: Test and verify (测试和验证)

## Key Questions (关键问题)
1. What error message appears? (出现什么错误消息?)
2. Which file handles authentication? (哪个文件处理认证?)
3. What changed recently? (最近有什么变化?)

## Decisions Made (已做的决策)
- Auth handler is in src/auth/login.ts (认证处理器在 src/auth/login.ts)
- Error occurs in validateToken() function (错误发生在 validateToken() 函数)

## Errors Encountered (遇到的错误)
- [Initial] TypeError: Cannot read property 'token' of undefined
  → Root cause: user object not awaited properly
  (根本原因: user 对象未正确等待)

## Status (状态)
**Currently in Phase 3** - Found root cause, preparing fix
(当前在第 3 阶段 - 找到根本原因,准备修复)
```

---

## Example 3: Feature Development (示例 3: 功能开发)

**User Request:** "Add a dark mode toggle to the settings page"
**用户请求:** "在设置页面添加深色模式切换"

### The 3-File Pattern in Action (三文件模式实践)

**task_plan.md:**
```markdown
# Task Plan: Dark Mode Toggle (深色模式切换)

## Goal (目标)
Add functional dark mode toggle to settings.
添加功能性的深色模式切换到设置。

## Phases (阶段)
- [x] Phase 1: Research existing theme system ✓ (研究现有主题系统)
- [x] Phase 2: Design implementation approach ✓ (设计实施方案)
- [ ] Phase 3: Implement toggle component (CURRENT) (实施切换组件 - 当前)
- [ ] Phase 4: Add theme switching logic (添加主题切换逻辑)
- [ ] Phase 5: Test and polish (测试和完善)

## Decisions Made (已做的决策)
- Using CSS custom properties for theme (使用 CSS 自定义属性实现主题)
- Storing preference in localStorage (将偏好存储在 localStorage)
- Toggle component in SettingsPage.tsx (切换组件在 SettingsPage.tsx)

## Status (状态)
**Currently in Phase 3** - Building toggle component
(当前在第 3 阶段 - 构建切换组件)
```

**notes.md:**
```markdown
# Notes: Dark Mode Implementation (深色模式实施)

## Existing Theme System (现有主题系统)
- Located in: src/styles/theme.ts (位于)
- Uses: CSS custom properties (使用)
- Current themes: light only (当前主题: 仅浅色)

## Files to Modify (要修改的文件)
1. src/styles/theme.ts - Add dark theme colors (添加深色主题颜色)
2. src/components/SettingsPage.tsx - Add toggle (添加切换)
3. src/hooks/useTheme.ts - Create new hook (创建新钩子)
4. src/App.tsx - Wrap with ThemeProvider (用 ThemeProvider 包装)

## Color Decisions (颜色决策)
- Dark background: #1a1a2e (深色背景)
- Dark surface: #16213e (深色表面)
- Dark text: #eaeaea (深色文本)
```

**dark_mode_implementation.md:** (deliverable) (交付物)
```markdown
# Dark Mode Implementation (深色模式实施)

## Changes Made (所做的更改)

### 1. Added dark theme colors (添加深色主题颜色)
File: src/styles/theme.ts
...

### 2. Created useTheme hook (创建 useTheme 钩子)
File: src/hooks/useTheme.ts
...
```

---

## Pattern: Error Recovery (模式: 错误恢复)

When something fails, DON'T hide it:
当某些事情失败时,不要隐藏它:

### Before (Wrong) (之前 - 错误)
```
Action: Read config.json
Error: File not found
Action: Read config.json  # Silent retry (静默重试)
Action: Read config.json  # Another retry (又一次重试)
```

### After (Correct) (之后 - 正确)
```
Action: Read config.json
Error: File not found

# Update task_plan.md: (更新 task_plan.md)
## Errors Encountered (遇到的错误)
- config.json not found → Will create default config
  (config.json 未找到 → 将创建默认配置)

Action: Write config.json (default config) (写入默认配置)
Action: Read config.json
Success!
```

---

## Pattern: The Read-Before-Decide (模式: 决策前读取)

**Always read your plan before major decisions:**
**始终在重大决策前读取你的计划:**

```
[Many tool calls have happened...] ([发生了许多工具调用...])
[Context is getting long...] ([上下文正在变长...])
[Original goal might be forgotten...] ([原始目标可能已被遗忘...])

→ Read task_plan.md          # This brings goals back into attention!
                              (这将目标带回注意力!)
→ Now make the decision       # Goals are fresh in context
                              (现在做出决策 - 目标在上下文中是新鲜的)
```

This is why Manus can handle ~50 tool calls without losing track. The plan file acts as a "goal refresh" mechanism.
这就是为什么 Manus 可以处理约 50 次工具调用而不会迷失方向。计划文件充当"目标刷新"机制。
