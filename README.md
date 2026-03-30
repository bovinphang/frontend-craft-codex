# frontend-craft-codex

[![Stars](https://img.shields.io/github/stars/bovinphang/frontend-craft-codex?style=flat)](https://github.com/bovinphang/frontend-craft-codex/stargazers)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![TypeScript](https://img.shields.io/badge/-TypeScript-3178C6?logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/-React-61DAFB?logo=react&logoColor=black)
![Vue](https://img.shields.io/badge/-Vue-4FC08D?logo=vue.js&logoColor=white)
![Figma](https://img.shields.io/badge/-Figma-F24E1E?logo=figma&logoColor=white)
![Node](https://img.shields.io/badge/-Node.js-339933?logo=node.js&logoColor=white)

---

<div align="center">

**🌐 Language / 语言 / 語言 / 言語 / 한국어**

[**English**](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](docs/zh-TW/README.md) | [日本語](docs/ja-JP/README.md) | [한국어](docs/ko-KR/README.md)

</div>

---

**A Codex plugin for enterprise frontend teams.**

Integrates code review, security review, design-to-code (Figma/Sketch/MasterGo/Pixso/墨刀/摹客), accessibility checks, automated quality assurance, and project templates. All review, analysis, and evaluation reports are automatically saved as Markdown files to the project `reports/` directory for archiving, traceability, and team sharing.

---

## 🚀 Quick Start

### Step 1: Install the plugin

**Option A: Project-level (recommended)**

```bash
# Add as submodule in project root
git submodule add https://github.com/bovinphang/frontend-craft-codex.git .frontend-craft

# Copy skills and agents to project
cp -r .frontend-craft/.agents .frontend-craft/.codex .
```

**Option B: User-level**

```bash
git clone https://github.com/bovinphang/frontend-craft-codex.git .frontend-craft

# Copy to Codex user directory
cp -r .frontend-craft/.agents/skills/* ~/.agents/skills/
cp -r .frontend-craft/.codex/agents/* ~/.codex/agents/
```

### Step 2: Initialize project config (recommended)

Invoke the `$frontend-craft-init` skill or ask Codex:

```
Please use the frontend-craft-init skill to initialize project templates to .codex/
```

After initialization, customize for your project:

1. `AGENTS.md` — Update project info, package manager, common commands
2. `.codex/rules/` — Remove inapplicable rules (e.g. delete `vue.md` for React-only projects)
3. `.codex/config.toml` — Configure MCP design tools as needed

### Step 3: Start using

```
# Code review (outputs to reports/code-review-*.md)
Use frontend-craft-review or frontend-code-review skill

# Create page/feature/component
Use frontend-craft-scaffold skill - create UserDetail page, create DataTable component

# Invoke subagents explicitly
Use frontend-architect to analyze component architecture
Use performance-optimizer for performance analysis
```

✨ **Done!** You now have access to 5 custom agents, 16 skills.

---

## 🌐 Multi-agent skills (Skills CLI)

If your team uses **Claude Code**, **OpenAI Codex**, **Cursor**, **OpenCode**, **Gemini CLI**, **OpenClaw**, **Continue**, **CodeBuddy**, **Trae**, **Kimi Code CLI**, or other AI coding agents, you can install the **workflow skills** from the canonical [`bovinphang/frontend-craft`](https://github.com/bovinphang/frontend-craft) repository into each tool’s skills directory using the [Skills CLI](https://skills.sh/docs/cli) (`npx skills`). The CLI supports dozens of agents; the exact list appears in interactive prompts or in the upstream documentation.

**Skills CLI vs. this Codex repo**

- **Skills CLI** — Installs skill packages from `bovinphang/frontend-craft` into the paths your chosen agents expect. Use this when you want the same review and frontend standards across multiple tools.
- **This repository** — Provides the **Codex** layout ([`.agents/skills/`](.agents/skills/), [`.codex/agents/`](.codex/agents/), Codex-specific init/review/scaffold skills, etc.) via the **Quick Start** steps above (submodule or copy).

**Requirements:** Node.js ≥ 18.

**Install skills**

```bash
npx skills add bovinphang/frontend-craft
```

Follow the prompts for project vs. global install (`-g`), symlink vs. copy (`--copy`), and which agents to enable. To list skills in the repo without installing, run `npx skills add bovinphang/frontend-craft -l`. For specific skills or agents, use `--skill` / `--agent` (see `npx skills --help`).

**Update skills**

From the project where skills were installed (or after a global install, use the matching scope):

```bash
npx skills update
```

This updates all installed skills to their latest versions. You can run `npx skills check` first to see what would change.

**Telemetry:** The CLI may collect anonymous telemetry by default. To disable it, set `DISABLE_TELEMETRY=1`. Details: [skills.sh CLI docs](https://skills.sh/docs/cli).

---

## 📦 What's inside

```
frontend-craft-codex/
├── .agents/skills/          # Codex Skills (16 total)
│   ├── frontend-code-review/     # Architecture, types, rendering, styles, a11y
│   ├── frontend-craft-init/      # Initialize project templates
│   ├── frontend-craft-review/    # Review with Git scope
│   ├── frontend-craft-scaffold/  # Create page/feature/component
│   ├── security-review/         # XSS, CSRF, sensitive data, input validation
│   ├── accessibility-check/     # WCAG 2.1 AA accessibility
│   ├── implement-from-design/   # Implement UI from design files
│   ├── test-and-fix/            # lint, type-check, test, build and fix
│   ├── react-project-standard/  # React + TypeScript standards
│   ├── vue3-project-standard/   # Vue 3 + TypeScript standards
│   ├── legacy-web-standard/     # JS + jQuery + HTML legacy projects
│   ├── legacy-to-modern-migration/
│   ├── e2e-testing/             # Playwright/Cypress E2E
│   ├── nextjs-project-standard/ # Next.js 14+ App Router
│   ├── nuxt-project-standard/   # Nuxt 3 SSR/SSG
│   └── monorepo-project-standard/
│
├── .codex/agents/           # Custom subagents (5 total)
│   ├── frontend-architect.toml   # Page splitting, component architecture
│   ├── performance-optimizer.toml # Performance bottleneck analysis
│   ├── ui-checker.toml           # UI visual issues, design fidelity
│   ├── figma-implementer.toml    # Precise UI implementation from design
│   └── design-token-mapper.toml  # Map design variables to Tokens
│
└── scripts/                 # Optional: manual integration
    ├── security-check.mjs   # Block dangerous commands
    ├── format-changed-file.mjs
    ├── run-tests.mjs
    ├── session-start.mjs
    └── notify.mjs
```

---

## 📋 Feature overview

### Skills

| Skill | Purpose | Report output |
|-------|---------|---------------|
| `frontend-code-review` | Review code on architecture, types, rendering, styles, a11y | `code-review-*.md` |
| `frontend-craft-review` | Review specified files or recent Git changes | `code-review-*.md` |
| `frontend-craft-init` | Initialize project templates to `.codex/` | — |
| `frontend-craft-scaffold` | Create page / feature / component by convention | — |
| `security-review` | XSS, CSRF, sensitive data, input validation | `security-review-*.md` |
| `accessibility-check` | WCAG 2.1 AA accessibility | `accessibility-review-*.md` |
| `implement-from-design` | Implement UI from Figma/Sketch/MasterGo/Pixso/墨刀/摹客 | `design-plan-*.md` |
| `test-and-fix` | Run lint, type-check, test, build and fix | `test-fix-*.md` |
| `react-project-standard` | React + TypeScript project standards | — |
| `vue3-project-standard` | Vue 3 + TypeScript project standards | — |
| `legacy-web-standard` | JS + jQuery + HTML legacy projects | — |
| `legacy-to-modern-migration` | jQuery/MPA → React/Vue 3 migration strategy | `migration-plan-*.md` |
| `e2e-testing` | Playwright/Cypress E2E standards | — |
| `nextjs-project-standard` | Next.js 14+ App Router standards | — |
| `nuxt-project-standard` | Nuxt 3 SSR/SSG standards | — |
| `monorepo-project-standard` | pnpm workspace, Turborepo, Nx | — |

### Custom agents (subagents)

| Agent | Purpose | Report output |
|-------|---------|---------------|
| `frontend-architect` | Page splitting, component architecture, state flow, directory planning | `architecture-proposal-*.md` |
| `performance-optimizer` | Analyze performance bottlenecks, output optimization plan | `performance-review-*.md` |
| `ui-checker` | UI visual issues, design fidelity evaluation | `ui-fidelity-review-*.md` |
| `figma-implementer` | Precise UI implementation from design files | `design-implementation-*.md` |
| `design-token-mapper` | Map design variables to project Design Tokens | `token-mapping-*.md` |

Invoke subagents explicitly in your prompt, e.g.:

```
Use frontend-architect to analyze the component architecture for this page
```

### Project templates (via `$frontend-craft-init`)

| File | Purpose |
|------|---------|
| `AGENTS.md` | Project description, common commands, working principles |
| `.codex/config.toml` | MCP server config for design tools |
| `.codex/rules/vue.md` | Vue 3 component standards |
| `.codex/rules/react.md` | React component standards |
| `.codex/rules/design-system.md` | Design system, Token, accessibility |
| `.codex/rules/testing.md` | Testing and validation |
| `.codex/rules/git-conventions.md` | Conventional Commits |
| `.codex/rules/i18n.md` | Internationalization |
| `.codex/rules/performance.md` | Performance optimization |
| `.codex/rules/api-layer.md` | API layer, error handling |
| `.codex/rules/state-management.md` | State management |
| `.codex/rules/error-handling.md` | Error handling |
| `.codex/rules/naming-conventions.md` | Naming conventions |
| `.codex/rules/code-comments.md` | Frontend code comment guidelines |
| `.codex/rules/ci-cd.md` | CI/CD pipeline |
| `.codex/rules/refactoring.md` | Refactoring constraints |

---

## ⚙️ Configuration

### Prerequisites

- [Codex](https://developers.openai.com/codex/) (CLI, IDE extension, or App)
- Node.js >= 18
- npm, pnpm, or yarn

### MCP design tools

Configure in `.codex/config.toml` or `~/.codex/config.toml`. Set environment variables:

| Variable | Tool | How to get |
|----------|------|------------|
| `FIGMA_API_KEY` | Figma / Figma Desktop | Figma account settings > Personal Access Tokens |
| `SKETCH_API_KEY` | Sketch | Sketch developer settings |
| `MG_MCP_TOKEN` | MasterGo | MasterGo account settings > Security > Generate Token |
| `MODAO_TOKEN` | 墨刀 | 墨刀 AI feature page for access token |

> Pixso uses local MCP; enable in Pixso client. No extra env vars.
> 摹客 has no MCP; works via user screenshots/annotations.

**macOS / Linux:**

```bash
export FIGMA_API_KEY="your-figma-api-key"
export SKETCH_API_KEY="your-sketch-api-key"
export MG_MCP_TOKEN="your-mastergo-token"
export MODAO_TOKEN="your-modao-token"
```

**Windows (PowerShell):**

```powershell
$env:FIGMA_API_KEY = "your-figma-api-key"
$env:SKETCH_API_KEY = "your-sketch-api-key"
$env:MG_MCP_TOKEN = "your-mastergo-token"
$env:MODAO_TOKEN = "your-modao-token"
```

---

## 📄 Report output

All reports are saved to the project `reports/` directory:

| Report type | Filename pattern | Source |
|-------------|------------------|--------|
| Code review | `code-review-YYYY-MM-DD-HHmmss.md` | `frontend-craft-review`, `frontend-code-review` |
| Security review | `security-review-YYYY-MM-DD-HHmmss.md` | `security-review` |
| Accessibility | `accessibility-review-YYYY-MM-DD-HHmmss.md` | `accessibility-check` |
| Performance | `performance-review-YYYY-MM-DD-HHmmss.md` | `performance-optimizer` |
| Architecture | `architecture-proposal-YYYY-MM-DD-HHmmss.md` | `frontend-architect` |
| Design fidelity | `ui-fidelity-review-YYYY-MM-DD-HHmmss.md` | `ui-checker` |
| Design implementation | `design-implementation-YYYY-MM-DD-HHmmss.md` | `figma-implementer` |
| Token mapping | `token-mapping-YYYY-MM-DD-HHmmss.md` | `design-token-mapper` |
| Design plan | `design-plan-YYYY-MM-DD-HHmmss.md` | `implement-from-design` |
| Test fix | `test-fix-YYYY-MM-DD-HHmmss.md` | `test-and-fix` |
| Migration plan | `migration-plan-YYYY-MM-DD-HHmmss.md` | `legacy-to-modern-migration` |

> **Tip:** Add `reports/` to `.gitignore` to avoid committing auto-generated reports.

---

## 📥 Update

For Git submodule installs:

```bash
git submodule update --remote .frontend-craft
cp -r .frontend-craft/.agents .frontend-craft/.codex .
```

For user-level installs, re-copy the updated skills and agents.

---

## 🎯 Key concepts

### Skills

Codex skills are workflow definitions with `name` and `description` in `SKILL.md`. Codex can invoke them implicitly when your task matches the description, or explicitly via `$skill-name` or by mentioning the skill in your prompt.

### Custom agents (subagents)

Custom agents are defined in `.codex/agents/*.toml`. Each file specifies `name`, `description`, and `developer_instructions`. Invoke them explicitly in your prompt when you need specialized analysis (e.g. architecture, performance, design fidelity).

### Scripts (optional)

Codex does not support hooks. The `scripts/` directory contains utilities you can integrate manually into pre-commit hooks, CI pipelines, or reference in `AGENTS.md` for Codex to run when appropriate.

---

## 📄 License

MIT — Use freely, modify as needed, contribute back if you can.

---

**If this repo helps you, give it a Star. Build something great.**
