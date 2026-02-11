---
name: skill-value-assessor
description: Evaluate whether a task is worth converting into an AI Skill using a three-dimensional assessment model (Cognitive Friction, Process Structure, Reuse Value). Use when the user wants to decide if a workflow should be automated as a Skill, asks questions like "Should I make this a Skill?", "Is this worth automating?", or explicitly invokes with /assess-skill or /skill-eval. Provides guided questioning, automatic scoring, and concrete recommendations.
---

# Skill Value Assessor

## Core Purpose

Help users make informed decisions about whether a manual workflow should be converted into an AI Skill by applying a structured three-dimensional assessment model.

## When This Skill Is Used

This skill triggers when users:
- Ask if a task should be made into a Skill
- Want to evaluate automation value before investing time
- Need guidance on prioritizing Skill development
- Use commands like `/assess-skill` or `/skill-eval`

## Assessment Workflow

### Phase 1: Task Understanding

First, clearly identify the task being evaluated:

1. **Extract the task description** from user input
2. **Clarify the workflow** if unclear:
   - "Can you describe the steps you currently take manually?"
   - "What makes this task difficult or time-consuming?"

### Phase 2: Guided Three-Dimensional Assessment

Evaluate the task across three dimensions using guided questioning. Present one dimension at a time to avoid overwhelming the user.

#### Dimension A: Cognitive Friction (认知摩擦力)
*"How mentally draining is this task?"*

Present the scoring scale:
```
【维度 1/3：认知摩擦力】— 人脑有多抗拒这个任务？

1分 🟢 顺手就做，不费脑子
      示例：回复"收到"，简单的复制粘贴

2分 🟢 略微繁琐，但还好
      示例：发送常规邮件

3分 🟡 需要停下来想一想，或查资料
      示例：写复杂SQL，查API文档

4分 🟠 很烦，总想拖延，容易遗漏
      示例：代码审查，写技术文档

5分 🔴 极度消耗脑力，让人心累
      示例：全景盲点扫描，多语言翻译保持格式

基于你的描述 [复述任务]，我初步判断可能是 [X] 分。
你同意吗？或者请告诉我你的实际感受：
```

**Scoring logic**:
- If user provides a number (1-5), use it directly
- If user describes feelings, map to appropriate score:
  - "easy", "simple", "quick" → 1-2
  - "annoying", "tedious", "need to think" → 3
  - "hate doing this", "always procrastinate" → 4
  - "exhausting", "error-prone", "overwhelming" → 5

#### Dimension B: Process Structure (结构化程度)
*"How clear and repeatable is the workflow?"*

Present the scoring scale:
```
【维度 2/3：结构化程度】— 这个流程有多清晰？

1分 🔴 完全依赖灵感，每次都不一样
      示例：写诗，画抽象画，创意设计

2分 🟠 有大致框架，但中间步骤模糊
      示例：写读后感，整理书签（无固定分类标准）

3分 🟡 有框架，部分步骤需要判断
      示例：写项目总结，代码重构

4分 🟢 步骤比较清晰，有明确的检查点
      示例：根据模板写文档，格式化数据

5分 🟢 完全标准化，有明确的 if-then 逻辑
      示例：提取摘要，格式化JSON，5W1H检查清单

关键问题：你能用"如果...那么..."的规则描述这个流程吗？
如果流程每次都差不多，且步骤明确 → 分数高
如果需要大量创意或每次都不同 → 分数低

基于 [任务描述]，我认为结构化程度是 [X] 分。
你同意吗？或者描述一下你的流程：
```

**Scoring logic**:
- Ask: "Can you describe the process as a series of if-then rules?"
- If workflow varies significantly each time → 1-2
- If there's a rough template but needs judgment → 3
- If steps are mostly clear with minor variations → 4
- If fully deterministic and can be written as checklist → 5

**Critical check**: If score is ≤2, proactively suggest:
```
⚠️ 注意：你的流程结构化程度较低（[X]分）。

这可能意味着：
- 每次执行流程都需要创意或大量判断
- 难以用明确的步骤描述

建议：
• 如果可以先优化流程（建立标准化步骤），结构化程度可能提升到4-5分
• 如果流程本质上依赖创意，可能不适合做成Skill

是否需要我帮你分析如何优化流程？[Y/N]
```

#### Dimension C: Reuse Value (复用价值)
*"How often will this be used, and what's the cost of errors?"*

Present the scoring scale:
```
【维度 3/3：复用价值】— 值得折腾吗？

1分 🔴 低频低值：一年做一次，做错了也无所谓
      示例：年终总结的开头寒暄

2分 🟠 低频中值：偶尔需要，但不太重要
      示例：清理临时文件

3分 🟡 高频低值：每天都做，但很简单
      示例：整理桌面文件

4分 🟢 低频高值：不常做，但出错代价很大
      示例：服务器部署配置，合同审核

5分 🟢 高频高值：每天都做，且直接影响产出质量
      示例：代码提交规范检查，每日复盘，需求分析

请回答：
1. 这个任务多久做一次？（每天/每周/每月/偶尔）
2. 如果做错了，会有什么后果？（无所谓/有点麻烦/可能导致严重问题）

基于你的回答，我判断复用价值是 [X] 分。
```

**Scoring logic**:
- Daily + high impact → 5
- Daily + low impact → 3
- Rare + high impact → 4
- Rare + low impact → 1-2

### Phase 3: Calculation & Recommendation

After collecting all three scores:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 评估结果汇总

任务：[任务名称]

维度评分：
  A. 认知摩擦力：[X]/5 分
  B. 结构化程度：[X]/5 分
  C. 复用价值：  [X]/5 分

总分：[XX]/15 分
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Apply decision thresholds**:

#### Score 12-15: 立即封装 (Must Have) ✅
```
🎯 判定：立即封装 (Must Have)

这是 AI Skill 的甜蜜区！
• 既能极大减轻你的负担
• AI 又能执行得很好
• 投资回报率高

💡 行动建议：
1. 马上创建 Skill（使用 /skill-creator）
2. 这将成为你的核心生产力工具
3. 建议在3个月后复盘：实际使用频率是否符合预期

📚 相似案例：
[匹配相似的高分案例]
```

#### Score 8-11: 优化后封装 (Should Have) ⚠️
```
⚠️ 判定：优化后封装 (Should Have)

当前得分：[XX]/15

瓶颈分析：
[识别最低分的维度]

• 如果 B (结构化程度) 低：
  → 先优化流程，建立清晰的SOP
  → 手工执行2-3次验证步骤
  → 然后再考虑自动化

• 如果 C (复用价值) 低：
  → 观察1-2周，记录实际使用频率
  → 如果频率上升，重新评估

• 如果 A (认知摩擦力) 低：
  → 手动执行可能更快
  → 除非未来频率提高

💡 建议的优化路径：
[具体的优化建议]

优化后预计得分：[估算]
```

#### Score 0-7: 保持人工 (Won't Do) ❌
```
❌ 判定：保持人工 (Won't Do)

原因分析：
[说明为什么不适合自动化]

• 如果任务太简单（A=1-2, C=1-2）
  → 手动更快，自动化是杀鸡用牛刀

• 如果流程不清晰（B=1-2）
  → AI无法处理高度依赖创意/直觉的任务
  → 除非能先标准化流程

• 如果频率太低（C=1-2）
  → 维护Skill的成本 > 节省的时间

💡 替代方案：
[建议其他工具或方法]
```

### Phase 4: Case Matching (Optional Enhancement)

Load `references/case_library.md` to find similar cases:

```
📚 相似案例参考：

你的任务与以下案例相似：

案例：[案例名称]
评分：[X+X+X = XX分]
判定：[结果]
关键学习：[一句话总结]

查看详情 → [[references/case_library.md#案例名称]]
```

### Phase 5: Save Assessment (Optional)

Ask user if they want to save this assessment:

```
💾 是否保存此次评估记录？

保存后可以：
• 季度复盘时查看决策模式
• 追踪哪些高分Skill实际有用
• 避免重复评估相似任务

[Y] 保存到评估历史
[N] 不保存

如果选择 Y，将记录保存到评估历史文件。
```

If user confirms, use the template from `references/assessment_template.md` to create/append to the assessment history file.

## Key Principles

1. **One dimension at a time** - Don't overwhelm with all three dimensions at once
2. **Proactive suggestions** - If you notice red flags (e.g., low structure score), suggest optimizations
3. **Concrete examples** - Use examples from case library to help calibration
4. **Clear thresholds** - Apply the 12/8/7 scoring thresholds consistently
5. **Context-aware** - If the task description is vague, ask clarifying questions before scoring

## Reference Materials

- **Detailed evaluation model** → `references/evaluation_model.md`
- **Case library** → `references/case_library.md`
- **Assessment template** → `references/assessment_template.md`

Load these references as needed during the assessment process.

## Anti-Patterns to Avoid

❌ Don't ask all three dimensions simultaneously
❌ Don't give scores without explanation
❌ Don't skip the recommendation phase
❌ Don't ignore low structure scores (proactively suggest optimization)
❌ Don't force users to use exact numbers (accept descriptions)
