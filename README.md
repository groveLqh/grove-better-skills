# grove-better-skills

个人沉淀的好用 skills 仓库。

这里主要收集一些可以反复复用的 Agent / Codex / ChatGPT 工作流。每个 skill 尽量不只是一段 prompt，而是包含触发场景、输入要求、执行流程、检查清单、输出格式和质量标准，方便在真实工作里稳定复用。

## Skills

### 1. Risk-Oriented Code Review

路径：[`skills/risk-oriented-code-review`](skills/risk-oriented-code-review)

用途：专门做“现在能跑，但以后可能会坑你”的第二层代码 review。

适合场景：

- 功能已经跑通
- happy path 看起来正确
- 普通 review 没发现明显 bug
- 但你担心隐藏副作用、兼容性、边界情况、性能、安全、测试和维护成本

推荐输入：

```text
请 review 当前 diff。
不要只看语法和明显 bug，请重点检查：隐藏副作用、破坏兼容性、边界情况、性能风险、安全风险、命名误导、测试不足和未来维护成本。
最后按严重程度排序。
```

它会重点检查：

- 隐藏副作用
- 破坏兼容性
- 边界情况
- 性能风险
- 安全风险
- 命名误导
- 测试不足
- 未来维护成本

输出会按严重程度排序：

- P0 / Blocker：合并前必须修
- P1 / High：建议合并前修
- P2 / Medium：可接受但需要 follow-up
- P3 / Low：轻量优化、命名、文档或测试补充

## 推荐目录结构

```text
skills/
└── skill-name/
    ├── SKILL.md
    └── README.md
```

## Skill 编写原则

一个好的 skill 不应该只是 prompt 片段，而应该尽量包含：

1. 它解决什么问题
2. 什么场景应该触发
3. 什么场景不应该触发
4. 需要收集哪些输入
5. 执行时的思考方式和工作流
6. 检查清单或判断维度
7. 输出格式
8. 好结果和坏结果的判断标准
9. 约束条件，避免 Agent 过度发挥

## 当前状态

- 已添加：`risk-oriented-code-review`
- 后续可以继续沉淀更多日常高频工作流，例如 PR 评论处理、CI 失败排查、产品方案 review、技术方案 review 等。
