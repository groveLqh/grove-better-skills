# uzi-skill

来源：<https://github.com/wbh604/UZI-Skill>

## 适用场景

用于 A 股、港股、美股的个股深度分析、快速扫描、估值建模、投资者评审团、龙虎榜/游资分析、杀猪盘风险检测、IC memo 和 Bloomberg 风格 HTML 报告生成。

适合问题包括：

- 想对一只股票做系统化深度研究，而不是只看单一指标或单篇研报
- 需要把个股分析拆成数据抓取、估值建模、投资者评审、定性判断和最终报告
- 需要 DCF、Comps、LBO、3-Stmt、IC Memo、Porter、单位经济等多种分析方法辅助判断
- 需要用多位投资者/流派视角做评审团式打分和分歧呈现
- 需要分析 A 股龙虎榜、游资席位、机构与游资博弈、同板块辨识度
- 需要检查“朋友推荐、群里老师、内幕消息、必涨翻倍”等场景下是否存在杀猪盘/异常推广风险

## 为什么值得记录

`UZI-Skill` 的价值不是单个 prompt，而是一套比较完整的股票研究工作流：它把个股研究拆成多个可审计阶段，并结合脚本、缓存数据、评分规则、评审团、估值模型、报告模板和风险检测。对于“需要 AI 帮忙看盘/做个股研究，但又怕输出空泛观点”的场景，它提供了一个相对完整的流程参考。

另外，它对 Agent 的约束写得比较明确：要求按任务顺序执行、不能编造数字、要暴露估值和评审分歧、要在关键阶段做自查 gate。这些设计也可以作为后续自研投资研究类 Skill 的参考。

## 主要模块

- `SKILL.md`：根入口，根据任务类型路由到最窄匹配的子 workflow。
- `skills/deep-analysis/SKILL.md`：个股深度分析主流程，覆盖数据抓取、估值建模、投资者评审、定性判断和 HTML 报告。
- `skills/investor-panel/SKILL.md`：投资者评审团，根据不同投资风格/流派输出信号、置信度、分数和理由。
- `skills/lhb-analyzer/SKILL.md`：龙虎榜与游资席位分析，识别机构 vs 游资博弈和板块辨识度。
- `skills/trap-detector/SKILL.md`：杀猪盘/异常推广风险检测，根据“老师带、群里推荐、内幕消息、必涨翻倍”等信号做风险评级。
- `commands/`：命令入口，例如深度分析、快速扫描、DCF、IC memo、投资者面板、陷阱检测等。
- `scripts/`：数据抓取、建模、评分、报告生成和测试相关脚本。

## 与本仓库自研 Skills 的关系

- 与 `skill-recommender` 互补：当用户任务是股票研究、估值分析、投资者视角评审、龙虎榜分析或杀猪盘风险检测时，可作为第三方候选推荐。
- 不替代 `risk-oriented-code-review`：`UZI-Skill` 是金融/股票研究 workflow，不是代码 review 工具。
- 可作为未来“行业/投资研究类 Skill”设计参考，尤其是多阶段 gate、定量结果和定性判断结合、报告产物结构化输出这些部分。

## 安装方式

Claude Code：

```text
/plugin marketplace add wbh604/UZI-Skill
/plugin install stock-deep-analyzer@uzi-skill
```

Codex / OpenAI CLI：

```text
按 https://raw.githubusercontent.com/wbh604/UZI-Skill/main/.codex/INSTALL.md 装 UZI-Skill，分析 600519
```

Gemini CLI：

```bash
gemini extensions install https://github.com/wbh604/UZI-Skill
```

CLI 直用：

```bash
git clone https://github.com/wbh604/UZI-Skill.git
cd UZI-Skill
pip install -r requirements.txt
python run.py 贵州茅台
```

## 使用示例

```text
/stock-deep-analyzer:analyze-stock 贵州茅台
/stock-deep-analyzer:quick-scan 002217
/stock-deep-analyzer:scan-trap 002217
/stock-deep-analyzer:dcf 600519
```

## 注意事项

- 这是投资研究辅助工具，不是直接买卖建议。
- 上游 README 中说明部分命令在不同 Agent 环境下需要带完整命名空间前缀：`/stock-deep-analyzer:<cmd>`。
- 深度分析依赖脚本、缓存、公开数据源和本地 Python 环境；如果只通过 marketplace 安装 skill 文件，仍需确认脚本依赖是否完整。
- 对真实投资决策，仍需要人工复核数据来源、财务指标、估值假设、市场风险和个人风险承受能力。

## 记录状态

- `installable: true`
- 已确认来源仓库根目录包含 `SKILL.md`
- 已确认仓库包含 `skills/deep-analysis`、`skills/investor-panel`、`skills/lhb-analyzer`、`skills/trap-detector` 等子技能
- 已确认上游提供 Claude Code、Codex、Gemini CLI 和 CLI 直用安装方式
- 适合作为第三方推荐候选，不放入本仓库 `skills/` 目录
