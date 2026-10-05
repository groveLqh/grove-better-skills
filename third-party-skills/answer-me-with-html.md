# answer-me-with-html

来源：<https://github.com/QingYunA/answer-me-with-html>

## 适用场景

把 Agent 的结构化回答做成可离线阅读的 HTML 页面。模型编写简短 Markdown 草稿，随 Skill 提供的 CLI 负责排版、主题和图表布局。

适合问题包括：

- 用时序图、状态流程图解释 TCP 握手等技术概念
- 梳理代码仓库的模块、目录和调用关系
- 对比多个技术方案，并给出表格和结论
- 把时间线、多步骤流程或较长总结整理成易读页面
- 按需生成带分步动画和旁白的讲解视频

## 为什么值得记录

将内容生成与页面渲染分开，减少模型逐行编写 CSS、HTML 和 SVG 坐标的工作。生成页面是自包含 HTML，无需 CDN 或网络字体，支持主题、明暗模式和复制内嵌 Markdown 源稿，适合技术学习与结果分享。

## 主要模块

- `skills/answer-me-with-html/SKILL.md`：触发场景、草稿格式和使用流程。
- `skills/answer-me-with-html/scripts/am.mjs`：随 Skill 打包的 CLI。
- 图表与内容组件：流程图、时序图、树、时间线、对比表和提示块等。
- `blueprint`、`shadcn`、`paper`：面向图解、卡片和长文的主题。
- `am video`：按需把草稿和旁白转换为讲解播放器页面，可进一步导出 MP4。

## 与本仓库自研 Skills 的关系

- 与 `skill-recommender` 配合：当任务是技术解释、架构梳理、方案对比或 HTML 图解交付时，可作为第三方候选推荐。
- 可用于呈现 `debugging-webpage-anomalies` 或 `risk-oriented-code-review` 的结论；诊断与证据核验仍由原工作流完成。
- 与 `clone-website` 的定位不同：本 Skill 侧重把回答转成图解页面，后者侧重研究并复刻已有网站。

## 安装方式

上游 README 给出的通用安装命令：

```bash
npx skills add QingYunA/answer-me-with-html
```

需要 Node.js 20 或更高版本；CLI 已打包在 Skill 内，上游说明无需额外执行 `npm install`。安装器会询问目标 Agent。

Claude Code 也可使用上游插件方式：

```text
/plugin marketplace add QingYunA/answer-me-with-html
/plugin install answer-me-with-html@answer-me-with-html
```

## 注意事项

- 默认根据问题复杂度决定是否生成页面；简单问题仍可直接回答。每轮都生成页面的 always-on 模式是可选配置。
- 页面默认保存在 `~/.answer-me-with-html/pages/`；分享前应检查内容及内嵌源稿中是否有私密信息。
- MP4 导出另需 Chrome、ffmpeg 和 Node.js 22+。ElevenLabs 旁白是可选能力，使用时会涉及外部服务。
- 上游性能与成本数字属于其基准结果，实际收益受模型、上下文和任务影响。

## 记录状态

- `installable: true`
- 已核对上游 README、Skill 入口和打包 CLI 路径
- 本次仅收录与核对文档，未安装或运行
- 收录核对日期：2026-10-05
