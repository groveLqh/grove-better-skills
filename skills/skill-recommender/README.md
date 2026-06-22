# Skill Recommender

用于在你犹豫该选哪个 Skill 时，根据当前任务场景，从本仓库自研 Skills 和记录的第三方 Skills 中推荐最合适的 3 个。

## 推荐调用方式

```text
/recommend 我想 review 当前 diff，功能已经跑通，但担心以后有隐藏风险
```

也可以直接要求 Agent 使用 `skill-recommender`：

```text
请使用 skill-recommender，帮我判断这个场景该用哪个 Skill：<描述你的任务>
```

## 安装

```bash
npx skills@latest add grove94/grove-better-skills skill-recommender
```

或在仓库根目录执行：

```bash
./install.sh skill-recommender
```

## 它会做什么

- 读取/参考本仓库 `skills.json` 中的自研 Skills。
- 读取/参考 `third-party-skills.json` 和 `third-party-skills/` 中记录的第三方 Skills。
- 结合你的任务目标、已有材料、风险和输出期望，推荐 3 个按优先级排序的 Skill。
- 每个推荐都使用固定格式：Skill 名称、具体作用、推荐理由。
- 给出可复制的下一步 prompt 或安装/调用方式。
