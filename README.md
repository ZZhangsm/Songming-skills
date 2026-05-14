# Songming-skills

一个适用于 Claude Code / Codex 的技能集合，用来存放个人积累的 AI Agent 技能。每个技能独立目录，包含 `SKILL.md` 入口及可选的 `references/`、`scripts/`、`assets/` 子目录。

A personal collection of Claude Code / Codex skills. Each skill lives in its own directory with a `SKILL.md` entry point and optional `references/`, `scripts/`, `assets/` subdirectories.

## 目录 / Table of Contents

- [这个仓库是做什么的 / What This Is](#toc-what)
- [技能列表 / Skills](#toc-skills)
  - [model-training-explainer](#toc-skill-mte)
- [安装与接入 / Installation](#toc-installation)
- [新增一个技能 / Adding a New Skill](#toc-new-skill)
- [文档结构 / Documentation Map](#toc-docs)
- [依赖要求 / Requirements](#toc-requirements)

<a id="toc-what"></a>
## 这个仓库是做什么的 / What This Is

本人日常工作中积累的 AI Agent 技能集合。每个技能封装一类特定任务的工作流——从读取仓库结构、阅读论文、到生成交付物——让 Claude Code / Codex 在收到相关指令时能以一致且可预期的方式执行。技能独立于任何具体代码库，可在多个项目中复用，Claude Code 和 Codex 均可使用。

This repo collects AI agent skills I've built through daily work. Each skill encapsulates a specific task workflow — reading a repo structure, parsing a paper, or generating a deliverable — so Claude Code / Codex executes consistently and predictably when triggered. Skills are decoupled from any specific project and reusable across repos.

<a id="toc-skills"></a>
## 技能列表 / Skills

<a id="toc-skill-mte"></a>
### model-training-explainer

**领域 Domain**: code-to-doc · paper-to-HTML · 模型架构解读 · 训练流程可视化

给定一个代码仓库和一篇论文（arXiv URL 或 PDF），生成单文件暗色主题的 HTML，逐一讲解模型及其训练流程：架构总览、数据流水线、训练策略、损失函数、评估，将论文中的每项 claim 映射到具体代码行，并用代表性数据集展示真实张量形状。

Given a code repository and a paper (arXiv URL or PDF), produce a single-file dark-theme HTML that walks through the model and its training pipeline — architecture overview, data pipeline, training strategy, loss functions, evaluation — mapping each paper claim to concrete code line references with real tensor dimensions from a representative dataset.

| 文件 File | 作用 Purpose |
|---|---|
| `model-training-explainer/SKILL.md` | 技能定义与执行策略 / Skill definition and workflow |
| `model-training-explainer/references/template.css` | 暗色主题样式（架构图、流程图、代码块、表格、响应式布局） / Dark-theme CSS for arch diagrams, flow charts, code blocks, tables, responsive layout |
| `model-training-explainer/references/template.js` | IntersectionObserver 滚动导航高亮 / Scroll-spy nav highlighter |

<a id="toc-installation"></a>
## 安装与接入 / Installation

```bash
# Claude Code
cp -r ./Songming-skills ~/.claude/skills/

# Codex
cp -r ./Songming-skills ~/.codex/skills/
```

或 symlink 到项目本地 / Or symlink into a project:

```bash
ln -s /path/to/Songming-skills/model-training-explainer /path/to/your-project/skills/
```

<a id="toc-new-skill"></a>
## 新增一个技能 / Adding a New Skill

在仓库根目录创建新目录，补充 `SKILL.md`：

Create a new directory with a `SKILL.md` at the repo root:

```bash
mkdir <skill-name>
```

`SKILL.md` 采用以下 frontmatter 格式 / Use this frontmatter format:

```markdown
---
name: <skill-name>
description: 一行描述，用于路由匹配 / One-line description for routing.
---

# <Skill Name>

**领域 / Domain:** <逗号分隔的领域标签 / comma-separated domain tags>

**概要 / Summary.** <2-3 句说明 / description of what this skill does>

**执行策略 / Strategy:**
1. ...
2. ...
3. ...
```

可选子目录 / Optional subdirectories:

- `references/` — 参考文件（CSS、JS 模板等） / reference files (CSS, JS templates, etc.)
- `scripts/` — 辅助脚本（抽取、构建等） / helper scripts (extraction, build, etc.)
- `assets/` — 静态资源 / static assets

新增完成后，更新 README 的技能列表段落。/ After adding, update the Skills section of this README.

<a id="toc-docs"></a>
## 文档结构 / Documentation Map

| 文件 File | 作用 Purpose |
|---|---|
| `README.md` | 仓库介绍 / Repo introduction |
| `<skill-name>/SKILL.md` | 技能定义与执行策略 / Skill definition and workflow |
| `<skill-name>/references/` | 技能配套模板与参考 / Templates and references |
| `<skill-name>/scripts/` | 技能辅助脚本 / Helper scripts |
| `<skill-name>/assets/` | 静态资源 / Static assets |

<a id="toc-requirements"></a>
## 依赖要求 / Requirements

- Claude Code 或 OpenAI Codex，支持从本地目录加载 skill / Claude Code or OpenAI Codex, with skill loading from local directories
- 各技能可能有额外依赖，见对应 `SKILL.md` / Individual skills may have additional dependencies — see their `SKILL.md`
