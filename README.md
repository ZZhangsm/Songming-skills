# Songming-skills

个人 Claude Code / Codex 技能集合，遵循 `anywhere-agents` 技能格式。每个技能独立目录，包含 `SKILL.md` 入口及可选的 `references/`、`scripts/`、`assets/` 子目录。

---

## 目录

- [这个仓库是做什么的](#what)
- [技能列表](#skills)
  - [model-training-explainer](#model-training-explainer)
- [安装与接入](#installation)
- [新增一个技能](#new-skill)
- [文档结构](#docs)
- [依赖要求](#requirements)

---

<a id="what"></a>
## 这个仓库是做什么的

本人日常工作中积累的 AI Agent 技能集合。每个技能封装一类特定任务的工作流——从读取仓库结构、阅读论文、到生成交付物——让 Claude Code / Codex 在收到相关指令时能以一致且可预期的方式执行。

为什么单独建一个仓库：

- 与项目解耦：技能独立于任何具体代码库，可在多个项目中复用
- 版本管理：技能的演进有 git 历史可追溯
- 共享方便：clone 或 symlink 即可接入
- 标准化格式：遵循 `anywhere-agents` 惯例，Claude Code 和 Codex 均可用

---

> **English** — A personal collection of AI agent skills following the `anywhere-agents` skill format. Each skill encapsulates a specific task workflow and lives in its own directory with a `SKILL.md` entry point and optional `references/`, `scripts/`, `assets/` subdirectories.
>
> Why a standalone repo:
> - Decoupled from projects: skills are reusable across multiple repos
> - Version controlled: full git history for each skill's evolution
> - Easy to share: clone or symlink to use anywhere
> - Standard format: follows `anywhere-agents` conventions, works with both Claude Code and Codex

---

<a id="skills"></a>
## 技能列表

<a id="model-training-explainer"></a>
### model-training-explainer

**领域：** code-to-doc · paper-to-HTML · 模型架构解读 · 训练流程可视化

给定一个代码仓库和一篇论文（arXiv URL 或 PDF），生成单文件暗色主题的 HTML，逐一讲解模型及其训练流程：架构总览、数据流水线、训练策略、损失函数、评估，将论文中的每项 claim 映射到具体代码行，并用代表性数据集展示真实张量形状。

**配套文件：**

| 文件 | 作用 |
|---|---|
| `model-training-explainer/SKILL.md` | 技能定义与执行策略 |
| `model-training-explainer/references/template.css` | 暗色主题样式（架构图、流程图、代码块、表格、响应式布局） |
| `model-training-explainer/references/template.js` | IntersectionObserver 滚动导航高亮 |

---

> **English — model-training-explainer**
>
> **Domain:** code-to-doc, paper-to-HTML, model architecture explanation, training pipeline visualization
>
> Given a code repository and a paper (arXiv URL or PDF), produce a single-file dark-theme HTML that walks through the model and its training pipeline — architecture, data pipeline, training strategy, loss functions, evaluation — mapping each paper claim to concrete code line references with real tensor dimensions from a representative dataset.
>
> **Supporting files:**
>
> | File | Purpose |
> |---|---|
> | `model-training-explainer/SKILL.md` | Skill definition and workflow |
> | `model-training-explainer/references/template.css` | Dark-theme CSS (arch diagrams, flow charts, code blocks, tables, responsive layout) |
> | `model-training-explainer/references/template.js` | IntersectionObserver scroll-spy nav highlighter |

---

<a id="installation"></a>
## 安装与接入

### 方式一：Agent Config（anywhere-agents 用户）

把以下配置加入 `agent-config.local.yaml`：

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

```bash
ln -s /path/to/Songming-skills/model-training-explainer /path/to/your-project/skills/
```

### 方式三：直接复制到全局技能目录

**Claude Code**

```bash
cp -r ./Songming-skills ~/.claude/skills/
```

**Codex**

```bash
cp -r ./Songming-skills ~/.codex/skills/
```

---

> **English — Installation**
>
> **Option A: Agent Config (anywhere-agents users)**
>
> Add to `agent-config.local.yaml`:
> ```yaml
> skill_sources:
>   - name: songming
>     url: https://github.com/<your>/Songming-skills
>     ref: main
> ```
> Then run: `anywhere-agents pack verify --fix`
>
> **Option B: Symlink into a project**
> ```bash
> ln -s /path/to/Songming-skills/model-training-explainer /path/to/your-project/skills/
> ```
>
> **Option C: Copy to global skills directory**
> - Claude Code: `cp -r ./Songming-skills ~/.claude/skills/`
> - Codex: `cp -r ./Songming-skills ~/.codex/skills/`

---

<a id="new-skill"></a>
## 新增一个技能

在仓库根目录创建新目录并补充 `SKILL.md`：

```bash
mkdir <skill-name>
```

`<skill-name>/SKILL.md` 采用以下 frontmatter 格式：

```markdown
---
name: <skill-name>
description: 一行描述，用于路由匹配
---

# <Skill Name>

**领域：** <逗号分隔的领域标签>

**概要：** <2-3 句说明>

**执行策略：**
1. ...
2. ...
```

如需配套文件，在技能目录下创建子目录：

- `references/` — 参考文件（CSS、JS 模板等）
- `scripts/` — 辅助脚本（抽取、构建等）
- `assets/` — 静态资源

新增完成后，更新本 README 的技能列表段落，加入新技能条目。

---

> **English — Adding a New Skill**
>
> Create a directory with a `SKILL.md` at the repo root:
> ```bash
> mkdir <skill-name>
> ```
>
> Frontmatter format for `<skill-name>/SKILL.md`:
> ```markdown
> ---
> name: <skill-name>
> description: One-line description for routing.
> ---
>
> # <Skill Name>
>
> **Domain:** <comma-separated domain tags>
>
> **Summary:** <2-3 sentence description>
>
> **Strategy:**
> 1. ...
> 2. ...
> ```
>
> Optional subdirectories:
> - `references/` — templates (CSS, JS, etc.)
> - `scripts/` — helper scripts (extraction, build, etc.)
> - `assets/` — static assets
>
> After adding, update the Skills section of this README.

---

<a id="docs"></a>
## 文档结构

| 文件 | 作用 |
|---|---|
| `README.md` | 仓库介绍 |
| `<skill-name>/SKILL.md` | 技能定义与执行策略 |
| `<skill-name>/references/` | 技能配套模板与参考 |
| `<skill-name>/scripts/` | 技能辅助脚本 |
| `<skill-name>/assets/` | 静态资源 |

> **English — Documentation Map**
>
> | File | Purpose |
> |---|---|
> | `README.md` | Repo introduction |
> | `<skill-name>/SKILL.md` | Skill definition and workflow |
> | `<skill-name>/references/` | Templates and references |
> | `<skill-name>/scripts/` | Helper scripts |
> | `<skill-name>/assets/` | Static assets |

---

<a id="requirements"></a>
## 依赖要求

- Claude Code 或 OpenAI Codex，支持从本地目录加载 skill
- 各技能可能有额外依赖，见对应 `SKILL.md`

> **English — Requirements**
>
> - Claude Code or OpenAI Codex, with skill loading from local directories
> - Individual skills may have additional dependencies — see their `SKILL.md`
