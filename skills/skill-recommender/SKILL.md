---
name: skill-recommender
description: >-
  Use this skill when the user is unsure which Skill to use. It recommends the
  top three matching options from this repository's first-party Skills and recorded
  third-party Skills based on the user's current task, constraints, and desired
  outcome. It is designed to be invoked directly or through the /recommend slash
  command.
---

# Skill Recommender

## Purpose

这个 Skill 用来回答：

> 我现在这个场景，该用哪个 Skill 最合适？

它会从两个来源中做选择：

1. 本仓库维护的自研 Skills：以根目录 `skills.json` 和 `skills/*/SKILL.md` 为准。
2. 本仓库记录的第三方 Skills：以根目录 `third-party-skills.json` 和 `third-party-skills/` 中的说明为准。

推荐目标不是列出所有可能选项，而是根据当前场景给出最适合的 3 个推荐方案。每个推荐必须使用固定格式：Skill 名称、具体作用、推荐理由。

## Trigger examples

Use this skill when the user says things like:

- “我该用哪个 skill？”
- “帮我从这些 skills 里选一个”
- “这个场景适合哪个 skill？”
- “我有点犹豫该选哪个”
- “/recommend 我想 review 一段已经能跑的代码，但担心未来有坑”

也可以通过 slash command 触发：

```text
/recommend <描述你的任务、场景、约束或目标>
```

## Do not use this skill for

Do not use this skill when:

- 用户已经明确点名要使用某个 Skill。
- 用户要你直接完成任务，而不是先选择 Skill。
- 任务明显不需要 Skill，直接回答更高效。
- 用户只是在询问某个具体 Skill 的安装或用法。

如果用户明确要求直接执行任务，可以在必要时简短说明“我会使用 X Skill”，然后直接执行，不要把推荐流程变成额外阻塞。

## Inputs to collect

优先从用户当前消息中提取，不要过度追问。推荐所需信息包括：

1. 任务目标：用户想完成什么？
2. 当前阶段：探索、实现、review、排障、写作、决策、发布等。
3. 输入材料：是否有 diff、代码、日志、PR、需求、设计稿、上下文文档等。
4. 风险偏好：速度优先、质量优先、保守稳妥、创意发散等。
5. 输出期望：清单、结论、代码修改、分析报告、命令、安装建议等。
6. 约束：时间、环境、工具、不能联网、不能改代码、必须引用来源等。

只有当缺少信息会显著影响推荐时，才问 1-3 个澄清问题。否则直接给出“基于当前信息”的推荐。

## Workflow

### Step 1: Build the candidate set

读取或依据上下文识别候选 Skill：

- First-party candidates come from `skills.json` and `skills/*/SKILL.md`.
- Third-party candidates come from `third-party-skills.json` and notes under `third-party-skills/`.

如果无法读取索引，则基于当前已知列表继续，但要说明“候选集可能不完整”。

### Step 2: Extract the user's scenario

把用户场景整理成 3-6 个判断维度：

- 主要任务类型
- 当前材料
- 成功标准
- 主要风险
- 需要的输出格式
- 是否需要安装或调用外部第三方 Skill

### Step 3: Score candidates

对每个明显相关候选按 0-3 分粗略评估：

- 3：高度匹配，可直接使用
- 2：部分匹配，需要补充约束或配合其他 Skill
- 1：弱匹配，只适合作为参考
- 0：不匹配

评分维度：

1. Trigger match：是否符合触发场景。
2. Input fit：用户现有材料是否满足该 Skill 的输入要求。
3. Output fit：该 Skill 的输出是否接近用户想要的结果。
4. Risk fit：该 Skill 是否覆盖当前最大风险。
5. Cost fit：使用成本是否符合用户当前时间和复杂度。

### Step 4: Recommend three Skills

默认推荐 3 个 Skill，并按推荐优先级排序。

每个推荐必须包含：

- Skill 名称：使用准确的 Skill 名称；如果是第三方 Skill，尽量附来源或记录位置。
- 具体作用：说明它能在当前场景中具体帮用户做什么。
- 推荐理由：解释为什么它适合当前任务、材料、风险或输出期望。

如果候选不足 3 个，可以少于 3 个，但必须明确说明“当前候选不足 3 个”以及缺少的原因。不要为了凑数推荐明显不匹配的 Skill。

### Step 5: Provide an invocation prompt

给出可直接复制的调用方式。若通过 `/recommend` 触发，也要给出下一步实际使用推荐 Skill 的 prompt。

## Output format

Use this format by default:

````markdown
## 推荐结论

### 1. `skill-name`

- Skill 名称：`skill-name`
- 具体作用：...
- 推荐理由：...

### 2. `skill-name`

- Skill 名称：`skill-name`
- 具体作用：...
- 推荐理由：...

### 3. `skill-name`

- Skill 名称：`skill-name`
- 具体作用：...
- 推荐理由：...

如果当前候选不足 3 个，写明：当前候选不足 3 个，原因是 ...

## 判断依据

- 当前任务：...
- 现有材料：...
- 最大风险/目标：...
- 排序逻辑：...

## 建议用法

```text
<可复制的下一步 prompt 或安装/调用命令>
```

## 还需要确认吗？

如果不需要，写：不需要，可以直接使用上述推荐。
如果需要，列出最多 3 个具体问题。
````

## Quality bar

A good recommendation:

- 明确给出 3 个按优先级排序的推荐，而不是让用户继续纠结。
- 每个推荐都包含固定格式：Skill 名称、具体作用、推荐理由。
- 能解释为什么这些 Skill 适合当前场景，并说明排序逻辑。
- 给出下一步可复制的 prompt 或安装命令。
- 候选不足时会承认不确定性。

A bad recommendation:

- 只是重复所有 Skill 列表。
- 不结合用户场景。
- 推荐多个选项但不排序。
- 没有按“Skill 名称 / 具体作用 / 推荐理由”的格式输出。
- 忽略第三方 Skills 记录。
- 没有下一步可执行动作。
