---
description: Recommend the top three Skills for the current task from this repository's first-party and recorded third-party Skills.
argument-hint: <describe your task, context, constraints, and desired output>
---

Use the `skill-recommender` Skill to recommend the top three Skills for this scenario:

$ARGUMENTS

When producing the recommendation, consider:

1. First-party Skills recorded in `skills.json` and `skills/*/SKILL.md`.
2. Third-party Skills recorded in `third-party-skills.json` and `third-party-skills/`.
3. The user's current goal, available inputs, risk level, constraints, and desired output.

Return exactly three recommendations when enough candidates exist, sorted by priority. For each recommendation, use this fixed format: Skill 名称, 具体作用, 推荐理由. If fewer than three relevant candidates exist, say why instead of forcing weak matches. Include a copyable next-step prompt or command.
