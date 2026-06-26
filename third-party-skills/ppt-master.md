# ppt-master

来源：<https://github.com/hugohe3/ppt-master>

## 适用场景

用于从文档、网页、Markdown、已有 PPTX、文本说明或主题需求生成真正可编辑的 PowerPoint 文件。它不是把页面截图塞进 PPT，而是通过 SVG 页面生成、质量检查、后处理和 PPTX 导出，生成可在 PowerPoint 中逐元素编辑的 `.pptx`。

适合问题包括：

- 从 PDF、DOCX、网页、Markdown、Excel、已有 PPTX 或文本材料生成演示文稿
- 想要真实可编辑的 PowerPoint，而不是每页一张图片
- 需要套用现有 PPTX 模板，把新内容填回原生版式
- 需要美化或重新排版已有 PPT，同时尽量保持文字和页序约束
- 需要生成 speaker notes、旁白音频、动画配置或在线预览
- 需要在 Agent 环境中把「资料处理 -> 设计策略 -> SVG 页面 -> 质量检查 -> PPTX 导出」串成严格流程

## 为什么值得记录

`ppt-master` 把生成 PPT 这类容易失控的任务拆成严格串行 pipeline，并提供大量脚本、模板、格式规范和独立 workflow。它的关键价值是输出原生可编辑 PPTX，适合需要后续人工继续修改、复用模板或交付正式演示文稿的场景。

## 主要模块

- `skills/ppt-master/SKILL.md`：主 workflow 和执行规则。
- `skills/ppt-master/scripts/`：文档转 Markdown、项目管理、图片分析、SVG 检查、SVG 后处理、PPTX 导出等脚本。
- `skills/ppt-master/templates/`：布局、品牌、图表、图标等模板资源。
- `skills/ppt-master/workflows/template-fill-pptx.md`：使用已有 PPTX 模板填充新内容。
- `skills/ppt-master/workflows/beautify-pptx.md`：对已有 PPTX 做 1:1 美化重排。
- `skills/ppt-master/workflows/topic-research.md`：只有主题、没有材料时先做资料收集。
- `skills/ppt-master/workflows/live-preview.md`：生成过程中的浏览器预览。
- `skills/ppt-master/workflows/customize-animations.md`：按需调整对象级动画。

## 与本仓库自研 Skills 的关系

- 与 `skill-recommender` 互补：当用户任务是生成、改写、美化、套模板或导出演示文稿时，可作为第三方候选推荐。
- 不替代 `risk-oriented-code-review`：`ppt-master` 是演示文稿生成 workflow，不是代码 review 工具。

## 安装方式

完整仓库方式：

```bash
git clone https://github.com/hugohe3/ppt-master.git
cd ppt-master
pip install -r requirements.txt
```

上游也提供 skill marketplace 安装方式：

```bash
npx skills add hugohe3/ppt-master
```

或在 Claude Code 内：

```text
/plugin marketplace add hugohe3/ppt-master
/plugin install ppt-master@ppt-master
```

注意：上游说明中 marketplace 安装只拉取 skill 文件，后处理脚本仍需要在安装目录执行 `pip install -r requirements.txt`。

## 记录状态

- `installable: true`
- 已确认来源仓库包含 `skills/ppt-master/SKILL.md`
- 已确认仓库包含脚本、模板、独立 workflow 和示例项目
- 适合作为第三方推荐候选，不放入本仓库 `skills/` 目录
