# Songming-skills

个人 Claude Code / Codex 技能集合，遵循 `anywhere-agents` 技能格式。每个技能独立目录，包含 `SKILL.md` 入口及可选的 `references/`、`scripts/`、`assets/` 子目录。

A personal collection of Claude Code / Codex skills following the `anywhere-agents` skill format. Each skill lives in its own directory with a `SKILL.md` entry point and optional `references/`, `scripts/`, `assets/` subdirectories.

## 目录 · Table of Contents

- [这个仓库是做什么的 · What This Is](#toc-what)
- [技能列表 · Skills](#toc-skills)
  - [model-training-explainer](#toc-skill-mte)
- [安装与接入 · Installation](#toc-installation)
- [新增一个技能 · Adding a New Skill](#toc-new-skill)
- [文档结构 · Documentation Map](#toc-docs)
- [依赖要求 · Requirements](#toc-requirements)

<a id="toc-what"></a>
## 这个仓库是做什么的 / What This Is

本人日常工作中积累的 AI Agent 技能集合。每个技能封装一类特定任务的工作流——从读取仓库结构、阅读论文、到生成交付物——让 Claude Code / Codex 在收到相关指令时能以一致且可预期的方式执行。

This repo collects AI agent skills I've built through daily work. Each skill encapsulates a specific task workflow — from reading repo structure and papers to generating deliverables — so Claude Code / Codex executes consistently and predictably when triggered.

### 为什么单独建一个仓库 / Why a standalone repo

- 与项目解耦：技能独立于任何具体代码库，可在多个项目中复用
- 版本管理：技能的演进有 git 历史可追溯
- 共享方便：clone 或 symlink 即可接入
- 标准化格式：遵循 `anywhere-agents` 惯例，Claude Code 和 Codex 均可用

- Decoupled from projects: skills are reusable across multiple repos
- Version controlled: full git history for each skill's evolution
- Easy to share: clone or symlink to use anywhere
- Standard format: follows `anywhere-agents` conventions, works with both Claude Code and Codex

<a id="toc-skills"></a>
## 技能列表 / Skills

<a id="toc-skill-mte"></a>
### model-training-explainer

**领域 / Domain:** code-to-doc · paper-to-HTML · 模型架构解读 · 训练流程可视化

给定一个代码仓库和一篇论文（arXiv URL 或 PDF），生成单文件暗色主题的 HTML，逐一讲解模型及其训练流程：架构总览、数据流水线、训练策略、损失函数、评估，将论文中的每项 claim 映射到具体代码行，并用代表性数据集展示真实张量形状。

Given a code repository and a paper (arXiv URL or PDF), produce a single-file dark-theme HTML that walks through the model and its training pipeline — architecture, data pipeline, training strategy, loss functions, evaluation — mapping each paper claim to concrete code line references with real tensor dimensions from a representative dataset.

**配套文件 / Supporting files:**

| 文件 / File | 作用 / Purpose |
|---|---|
| `model-training-explainer/SKILL.md` | 技能定义与执行策略 / Skill definition and workflow |
| `model-training-explainer/references/template.css` | 暗色主题样式（架构图、流程图、代码块、表格、响应式布局）/ Dark-theme CSS for arch diagrams, flow charts, code blocks, tables, responsive layout |
| `model-training-explainer/references/template.js` | IntersectionObserver 滚动导航高亮 / Scroll-spy nav highlighter |

<a id="toc-installation"></a>
## 安装与接入 / Installation

### 方式一：Agent Config（anywhere-agents 用户）

把以下配置加入 `agent-config.local.yaml`：

Add this to your `agent-config.local.yaml`:

```yaml
skill_sources:
  - name: songming
    url: https://github.com/<your>/Songming-skills
    ref: main
```

然后执行：

```bash
anywhere-agents pack verify --fix
```

### 方式二：Symlink 到项目本地

Symlink the skill directory into your project:

```bash
ln -s /path/to/Songming-skills/model-training-explainer /path/to/your-project/skills/
```

### 方式三：直接复制到全局技能目录

Copy to the global skills directory:

**Claude Code**

```bash
cp -r ./Songming-skills ~/.claude/skills/
```

**Codex**

```bash
cp -r ./Songming-skills ~/.codex/skills/
```

<a id="toc-new-skill"></a>
## 新增一个技能 / Adding a New Skill

在仓库根目录创建新目录并补充 `SKILL.md`：

Create a new directory with a `SKILL.md` at the repo root:

```bash
mkdir <skill-name>
```

`<skill-name>/SKILL.md` 采用以下 frontmatter 格式：

`<skill-name>/SKILL.md` uses this frontmatter format:

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

如需配套文件，在技能目录下创建子目录：

For supporting files, create subdirectories:

- `references/` — 参考文件（CSS、JS 模板等）/ reference files (CSS, JS templates, etc.)
- `scripts/` — 辅助脚本（抽取、构建等）/ helper scripts (extraction, build, etc.)
- `assets/` — 静态资源 / static assets

新增完成后，更新本 README 的[技能列表](#toc-skills)段落，加入新技能条目。

After adding, update the [Skills](#toc-skills) section of this README with the new entry.

<a id="toc-docs"></a>
## 文档结构 / Documentation Map

| 文件 / File | 作用 / Purpose |
|---|---|
| `README.md` | 仓库介绍 / Repo introduction |
| `<skill-name>/SKILL.md` | 技能定义与执行策略 / Skill definition and workflow |
| `<skill-name>/references/` | 技能配套模板与参考 / Templates and references |
| `<skill-name>/scripts/` | 技能辅助脚本 / Helper scripts |
| `<skill-name>/assets/` | 静态资源 / Static assets |

<a id="toc-requirements"></a>
## 依赖要求 / Requirements

- [Claude Code](https://claude.ai/claude-code) 或 [OpenAI Codex](https://codex.ai)，支持从本地目录加载 skill
- 各技能可能有额外依赖，见对应 `SKILL.md`
- [Claude Code](https://claude.ai/claude-code) or [OpenAI Codex](https://codex.ai), with skill loading from local directories
- Individual skills may have additional dependencies — see their `SKILL.md`
