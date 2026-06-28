# Econ Writing Agents

A [Claude Code plugin](https://docs.anthropic.com/en/docs/claude-code/plugins) that brings multi-agent review to **empirical-economics writing** — the same "multiple expert reviewers" model that makes peer review work, built into your drafting, results, and revision process. Adapted from [`andrehuang/academic-writing-agents`](https://github.com/andrehuang/academic-writing-agents) and re-targeted at causal-inference / panel / DID / IV / event-study papers (trade, political economy, applied micro).

## Why

In empirical economics, the gap between a clean identification strategy and a paper that survives a top-journal referee is large. Coefficients get narrated inconsistently with the table, causal claims outrun what the identification supports, pre-trend evidence is asserted without showing the individual years, and table notes omit the clustering level. Most authors catch these with one or two co-authors, late in the process.

This plugin gives you a team of **14 specialist agents** — each focused on a different dimension of an empirical paper — working in parallel, at any point in the writing process.

## Design Philosophy

Informed by Michael Black's "Writing a Good Scientific Paper", real empirical-paper supervision, and top-journal referee norms:

- **Parallel expert review.** Multiple specialized agents review simultaneously — an identification reviewer, a regression-table auditor, a technical reviewer, a writing reviewer, and a bibliography auditor all reading at once.
- **Review-then-act.** Always diagnose before fixing. The reviewer identifies issues; the polisher implements fixes. Never blindly edit.
- **43 codified principles** in 8 categories: Structure & Narrative, Prose & Style, Econometric Equations, Tables & Figures, Citations & Bibliography, Process & Meta, Empirical Identification & Regression, and **Paragraph-Level Flow & Self-Audit**.
- **Empirics are verifiable.** When an agent makes a claim about a coefficient, a p-value, or a sample size, the orchestrator checks it against the table / `.do` output before relaying it. Two agents never disagree about a number.
- **Human-in-the-loop.** Agents propose; the author decides. The plugin presents a prioritized plan and you choose what to act on. The mechanics (Stata, Python, LaTeX) run themselves.
- **Project CLAUDE.md is the source of truth.** General principles are defaults; your project's `.claude/CLAUDE.md` (FE structures, coefficient-direction constraints, binning rules) overrides them for this paper.

## How It Works

1. **Auto-triggers** when Claude detects empirical-economics context — `.tex` manuscripts with regression tables, `.do`/`.ipynb` estimation pipelines, identification or results sections, event-study figures.
2. The `econ` skill reads project conventions and **regression rules** from your `.claude/CLAUDE.md`.
3. Deploys the right specialist agents in parallel.
4. Synthesizes findings into a prioritized report (Critical / Important / Minor).
5. Offers to fix issues via action agents, direct edits, or re-running a `.do`/`.ipynb` when a result must be re-estimated.
6. Iterates with you until you are satisfied.

You can also invoke it manually: `/econ audit Table 8`.

## What's Included

### Skill

| Skill | Command | Description |
|-------|---------|-------------|
| **Econ** | `/econ <task>` | Orchestrates specialist agents for empirical-economics writing tasks |

### Agents (14 total)

**Empirical Review Agents** (read-only — economics-specific):

| Agent | Focus |
|-------|-------|
| `identification-reviewer` | DID parallel trends, IV relevance/exclusion, FE structure, control-group choice, calibrated causal language |
| `regression-table-auditor` | Coefficient sign/significance vs narrative, FE & cluster-SE annotation, N/clusters, star legend, table–text consistency |

**Review Agents** (read-only analysis):

| Agent | Focus |
|-------|-------|
| `consistency-checker` | Terminology, cross-refs, table/figure–text–note alignment, structural coherence |
| `logic-reviewer` | Identification narrative arc, transitions, argument gaps |
| `technical-reviewer` | Econometric specification, notation, identification soundness, robustness, citations |
| `writing-reviewer` | Prose clarity, conciseness, calibrated confidence over regression results |
| `latex-layout-auditor` | PDF layout audit — table column alignment, float placement, sizing |

**Audit Agents** (read + verify):

| Agent | Focus |
|-------|-------|
| `bibliography-auditor` | Bib completeness, working-paper→published updates (NBER/SSRN), title capitalization, journal-name consistency |

**Research Agents** (read + web):

| Agent | Focus |
|-------|-------|
| `research-analyst` | Related empirical literature, identification-strategy positioning, gap analysis |
| `brainstormer` | Alternative identification strategies, mechanisms, heterogeneity, research directions |

**Survey Agents** (read + web + write):

| Agent | Focus |
|-------|-------|
| `paper-crawler` | Collects papers from RePEc, NBER, OpenAlex, Crossref; deduplicates; classifies |

**Action Agents** (read + write):

| Agent | Focus |
|-------|-------|
| `prose-polisher` | Rewrites for clarity, conciseness, and calibrated causal language (edits, not just reports) |
| `section-drafter` | Drafts identification strategy, results discussion, robustness, captions, abstracts |
| `latex-figure-specialist` | Creates/adjusts regression tables (booktabs/threeparttable/esttab), event-study & coefficient plots |

### 43 Principles

Organized into 8 categories:

**A. Structure & Narrative** — A1 Recursive Consistency, A2 Logical Chaining, A3 Definition Order, A4 Paragraph Closers, A5 Claim-First, A6 GPS Rhythm, A7 The Nugget

**B. Prose & Style** — B1 Enumerations, B2 Negation-Contrast, B3 Colloquial Terms, B4 Author Voice, B5 One Idea/Sentence, B6 Calibrated Confidence, B7 Ruthless Conciseness, B8 AI-Tell Detection

**C. Econometric Equations** — C1 Equations for Clarity, C2 Text–Equation–Table Triple, C3 Equation–Code Correspondence

**D. Tables & Figures** — D1 Active Use, D2 Cross-Reference Floats, D3 Table/Figure–Text–Note Consistency, D4 One Message, D5 Interpret Don't Just Reference, D6 Layout & Alignment, D7 Note Self-Sufficiency

**E. Citations & Bibliography** — E1 Cite Named Datasets/Methods, E2 Citation Completeness, E3 Bibliography Hygiene

**F. Process & Meta** — F1 Strategic Limitations, F2 Negation-Contrast Audit

**G. Empirical Identification & Regression** — G1 Identification Strategy First, G2 Parallel Trends & Pre-trends, G3 Calibrated Causal Language, G4 Regression Table Completeness, G5 Coefficient–Narrative Consistency

**H. Paragraph-Level Flow & Self-Audit** — H1 One Message/Paragraph, H2 Topic-Sentence-First, H3 Self-Contained Terminology, H4 Reverse Outlining, H5 Reader-Perspective, H6 Transition Lexicon, H7 Claim–Evidence Mapping, H8 Adversarial Self-Review

## Usage

The plugin **auto-triggers** on empirical-economics context. Describe what you need in natural language:

```
Audit Table 8 (tab:tradewar_core_results) — coefficient directions, FE, cluster SE, star legend

Check the identification section — is the parallel-trend claim supported by individual pre-period coefficients?

Review the results discussion for consistency between prose and the table

Polish the results section, and fix any causal language that outruns the identification

Audit the bibliography — flag NBER/SSRN working papers that now have published versions

How does our BRI identification compare to recent trade-shock papers?

Survey recent work on trade war and supply-chain reallocation, 2018–2025

Re-estimate column (2), then update the results discussion to match the new numbers

Prepare this paper for submission — full review pipeline
```

You can also invoke the skill explicitly with `/econ <task>` if auto-triggering does not activate.

## Submission Readiness Pipeline（投稿准备工作流）

**`prepare for submission` 不是 agent，而是一个由 `/econ` 编排的投稿前总审工作流**（Submission Readiness Pipeline）——把"多专家并行审查 + 修复 + 验证 + 就绪清单"一次跑完。对应 `/econ prepare this paper for submission`。

### 三阶段

**Stage 1 — 并行审查**（7 个 agent 同时）：

| Agent | 审查重点 |
|---|---|
| `identification-reviewer` | 识别策略、平行趋势、IV 排他性、因果语言 |
| `regression-table-auditor` | 系数方向/显著性 vs 叙事、FE/cluster/N/星号、表-文一致 |
| `technical-reviewer` | 计量设定、稳健性、引用 |
| `consistency-checker` | 术语、交叉引用、表-文-注一致 |
| `writing-reviewer` | 文字清晰度、因果语言校准 |
| `bibliography-auditor` | `.bib` 完整性、working-paper→published |
| `latex-layout-auditor` | PDF 排版、表列对齐 |

**Stage 2 — 修复**：`prose-polisher`（文字/因果语言）+ `section-drafter`（结构补段）+ `latex-figure-specialist`（表/图）；必要时 orchestrator 用 Bash 重跑 `.do`/`.ipynb` 重估，并据新数字更新表与正文。

**Stage 3 — 验证**：`consistency-checker` + `regression-table-auditor` 复查改动，跑投稿就绪清单。

### 投稿就绪清单

- [ ] 每张表注含 FE、聚类层面、N、星号图例（D7, G4）
- [ ] 核心系数方向/显著性与项目铁律一致（G5）
- [ ] 设计禁用的 pre-treatment 单年无显著（G2）
- [ ] 因果语言与识别强度匹配（G3）
- [ ] 文献无 working-paper-only（已有发表版）（E3）
- [ ] AI 写作痕迹审计通过（B8, F2）
- [ ] 摘要点明核心发现 + 主效应量级（A7）
- [ ] 命名数据集/方法已引用（E1, E2）

### 用法

```
/econ prepare this paper for submission
```
或自然语言"准备投稿，跑完整审查流水线"。orchestrator 按 SKILL.md playbook 识别并部署三阶段。

---

## Workflow: Python + Stata + LaTeX

This plugin assumes the standard empirical-economics division of labor:

- **Python (notebook)** constructs variables and saves the analysis panel.
- **Stata (`.do`)** reads the Python output and runs the regressions, producing the estimates behind each table.
- **LaTeX (`.tex`)** renders the manuscript and tables.

When a result must change, the orchestrator re-runs the notebook then the `.do` via Bash (using your project's Stata and Python paths from `.claude/CLAUDE.md`), re-audits the regenerated table, and updates the prose to match the new numbers. Execution is not handed back to you — it runs inline.

## Installation

This is a local adaptation. Install it as a local plugin directory:

```bash
# Point Claude Code at this directory as a plugin:
claude --plugin-dir /mnt/c/Users/WINDOWS/.claude/plugins/econ-writing-agents
```

Or symlink / copy it into your Claude Code plugins location and enable it through `/plugin`.

To iterate during development, edit the files in place and reload.

## Review Persistence & Coordination

The orchestrator **persists review findings** and supports **incremental review**:

- **Review results saved to `.review/`**: After synthesis, aggregated findings (Critical/Important/Minor) are written to `<project>/.review/YYYY-MM-DD-<scope>.md`. Review results survive across sessions.
- **Incremental review**: Before deploying reviewers, the orchestrator checks whether the target files changed since the last review. Unchanged → present prior findings; changed → review only the changed files.
- **Cross-agent findings sharing**: Action agents (prose-polisher, section-drafter) receive the specific reviewer findings in scope, so fixes address flagged issues rather than applying generic improvements.

## Customization

### Project-level agents

Add domain-specific agents to your project's `.claude/agents/` directory. The orchestrator auto-discovers them and includes them in deployment plans.

### Project-level conventions (essential for this plugin)

Add a `.claude/CLAUDE.md` to your project with:
- Manuscript structure (`.tex` files, table `\label{}`s, build command)
- **Regression rules** — FE structures per dependent variable, coefficient-direction constraints, pre-trend / binning rules, the specific tables and figures they apply to
- LaTeX conventions (citation style `\cite`/`\citet`/`\citep`, cross-ref style, table packages)
- Stata and Python paths and the notebook→`.do`→table workflow

The identification-reviewer and regression-table-auditor read these rules and check the manuscript against them. Category G principles are the general default; the project CLAUDE.md is the source of truth for this specific paper.

### Extending the agent roster

Add new agents to `~/.claude/agents/` (global) or `<project>/.claude/agents/` (project-level). Each is a Markdown file with YAML frontmatter (name, description, tools, model). The orchestrator picks them up automatically.

## Acknowledgments

Built on [`andrehuang/academic-writing-agents`](https://github.com/andrehuang/academic-writing-agents) by Haiwen Huang, whose multi-agent architecture, review-then-act workflow, and writing principles this plugin inherits. The original draws on Michael Black's "Writing a Good Scientific Paper". This adaptation re-targets the agents, principles, literature sources, and examples at empirical-economics / causal-inference writing.

## License

MIT
