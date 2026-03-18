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

**🌐 语言 / Language / 語言 / 言語 / 한국어**

[**English**](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](docs/zh-TW/README.md) | [日本語](docs/ja-JP/README.md) | [한국어](docs/ko-KR/README.md)

</div>

---

**面向企业前端团队的 Codex 插件。**

集成代码评审、安全审查、设计稿转代码（Figma/Sketch/MasterGo/Pixso/墨刀/摹客）、无障碍检查、自动化质量保障和项目模板。所有评审、分析和评估报告自动保存为 Markdown 文件到项目 `reports/` 目录，便于归档、追溯和团队共享。

---

## 🚀 快速开始

### 第一步：安装插件

**方式一：项目级安装（推荐）**

```bash
# 在项目根目录添加为子模块
git submodule add https://github.com/bovinphang/frontend-craft-codex.git .frontend-craft

# 复制 skills 和 agents 到项目
cp -r .frontend-craft/.agents .frontend-craft/.codex .
```

**方式二：用户级安装**

```bash
git clone https://github.com/bovinphang/frontend-craft-codex.git .frontend-craft

# 复制到 Codex 用户目录
cp -r .frontend-craft/.agents/skills/* ~/.agents/skills/
cp -r .frontend-craft/.codex/agents/* ~/.codex/agents/
```

### 第二步：初始化项目配置（推荐）

调用 `$frontend-craft-init` skill 或直接询问 Codex：

```
请使用 frontend-craft-init skill 将项目模板初始化到 .codex/
```

初始化后根据项目实际情况修改：

1. `AGENTS.md` — 项目信息、包管理器、常用命令
2. `.codex/rules/` — 删除不适用的规则（如纯 React 项目删除 vue.md）
3. `.codex/config.toml` — 按需配置 MCP 设计工具

### 第三步：开始使用

```
# 代码评审（输出到 reports/code-review-*.md）
使用 frontend-craft-review 或 frontend-code-review skill

# 创建页面/功能/组件
使用 frontend-craft-scaffold skill - 创建 UserDetail 页面、创建 DataTable 组件

# 显式调用子代理
使用 frontend-architect 分析组件架构
使用 performance-optimizer 进行性能分析
```

✨ **完成！** 你现在可以使用 5 个自定义子代理、16 个 skills。

---

## 📦 目录结构

```
frontend-craft-codex/
├── .agents/skills/          # Codex Skills（16 个）
│   ├── frontend-code-review/     # 架构、类型、渲染、样式、可访问性
│   ├── frontend-craft-init/      # 初始化项目模板
│   ├── frontend-craft-review/   # 支持 Git 范围的评审
│   ├── frontend-craft-scaffold/  # 创建 page/feature/component
│   ├── security-review/         # XSS、CSRF、敏感数据、输入校验
│   ├── accessibility-check/     # WCAG 2.1 AA 无障碍
│   ├── implement-from-design/   # 设计稿实现
│   ├── test-and-fix/            # 校验与修复
│   ├── react-project-standard/  # React + TypeScript 规范
│   ├── vue3-project-standard/   # Vue 3 + TypeScript 规范
│   ├── legacy-web-standard/     # 遗留项目规范
│   ├── legacy-to-modern-migration/
│   ├── e2e-testing/             # Playwright/Cypress E2E
│   ├── nextjs-project-standard/ # Next.js 14+ App Router
│   ├── nuxt-project-standard/   # Nuxt 3 SSR/SSG
│   └── monorepo-project-standard/
│
├── .codex/agents/           # 自定义子代理（5 个）
│   ├── frontend-architect.toml   # 架构设计
│   ├── performance-optimizer.toml # 性能优化
│   ├── ui-checker.toml           # UI 还原度检查
│   ├── figma-implementer.toml    # 设计稿实现
│   └── design-token-mapper.toml  # Token 映射
│
└── scripts/                 # 可选：手动集成
    ├── security-check.mjs   # 危险命令检查
    ├── format-changed-file.mjs
    ├── run-tests.mjs
    ├── session-start.mjs
    └── notify.mjs
```

---

## 📋 功能概览

### Skills

| Skill | 用途 | 报告输出 |
|-------|------|----------|
| `frontend-code-review` | 架构、类型、渲染、样式、可访问性评审 | `code-review-*.md` |
| `frontend-craft-review` | 评审指定文件或最近 Git 变更 | `code-review-*.md` |
| `frontend-craft-init` | 初始化项目模板到 `.codex/` | — |
| `frontend-craft-scaffold` | 创建 page/feature/component | — |
| `security-review` | XSS、CSRF、敏感数据、输入校验 | `security-review-*.md` |
| `accessibility-check` | WCAG 2.1 AA 无障碍 | `accessibility-review-*.md` |
| `implement-from-design` | Figma/Sketch/MasterGo/Pixso/墨刀/摹客 实现 | `design-plan-*.md` |
| `test-and-fix` | lint、type-check、test、build 与修复 | `test-fix-*.md` |
| `react-project-standard` | React + TypeScript 规范 | — |
| `vue3-project-standard` | Vue 3 + TypeScript 规范 | — |
| `legacy-web-standard` | JS + jQuery 遗留项目 | — |
| `legacy-to-modern-migration` | jQuery/MPA → React/Vue 3 迁移 | `migration-plan-*.md` |
| `e2e-testing` | Playwright/Cypress E2E | — |
| `nextjs-project-standard` | Next.js 14+ App Router | — |
| `nuxt-project-standard` | Nuxt 3 SSR/SSG | — |
| `monorepo-project-standard` | pnpm workspace、Turborepo、Nx | — |

### 自定义子代理

| Agent | 用途 | 报告输出 |
|-------|------|----------|
| `frontend-architect` | 页面拆分、组件架构、状态流、目录规划 | `architecture-proposal-*.md` |
| `performance-optimizer` | 性能瓶颈分析、优化方案 | `performance-review-*.md` |
| `ui-checker` | UI 视觉问题、设计还原度评估 | `ui-fidelity-review-*.md` |
| `figma-implementer` | 设计稿精确实现 | `design-implementation-*.md` |
| `design-token-mapper` | 设计变量映射到 Token | `token-mapping-*.md` |

在提示词中显式调用子代理，例如：

```
请使用 frontend-architect 分析该页面的组件架构
```

### 项目模板（通过 `$frontend-craft-init`）

| 文件 | 用途 |
|------|------|
| `AGENTS.md` | 项目说明、常用命令、工作原则 |
| `.codex/config.toml` | MCP 设计工具配置 |
| `.codex/rules/vue.md` | Vue 3 组件规范 |
| `.codex/rules/react.md` | React 组件规范 |
| `.codex/rules/design-system.md` | 设计系统、Token、可访问性 |
| `.codex/rules/testing.md` | 测试与校验 |
| `.codex/rules/git-conventions.md` | Conventional Commits |
| `.codex/rules/i18n.md` | 国际化 |
| `.codex/rules/performance.md` | 性能优化 |
| `.codex/rules/api-layer.md` | API 层、错误处理 |
| `.codex/rules/state-management.md` | 状态管理 |
| `.codex/rules/error-handling.md` | 错误处理 |
| `.codex/rules/naming-conventions.md` | 命名规范 |
| `.codex/rules/ci-cd.md` | CI/CD 流水线 |
| `.codex/rules/refactoring.md` | 重构约束 |

---

## ⚙️ 配置

### 前置依赖

- [Codex](https://developers.openai.com/codex/)（CLI、IDE 扩展或 App）
- Node.js >= 18
- npm、pnpm 或 yarn

### MCP 设计工具

在 `.codex/config.toml` 或 `~/.codex/config.toml` 中配置。需设置环境变量：

| 变量 | 工具 | 获取方式 |
|------|------|----------|
| `FIGMA_API_KEY` | Figma / Figma Desktop | Figma 账户设置 > Personal Access Tokens |
| `SKETCH_API_KEY` | Sketch | Sketch 开发者设置 |
| `MG_MCP_TOKEN` | MasterGo | MasterGo 账户设置 > 安全 > 生成 Token |
| `MODAO_TOKEN` | 墨刀 | 墨刀 AI 功能页获取 |

> Pixso 使用本地 MCP，在 Pixso 客户端启用即可。摹客无 MCP，通过截图/标注配合使用。

**macOS / Linux：**

```bash
export FIGMA_API_KEY="your-figma-api-key"
export SKETCH_API_KEY="your-sketch-api-key"
export MG_MCP_TOKEN="your-mastergo-token"
export MODAO_TOKEN="your-modao-token"
```

**Windows (PowerShell)：**

```powershell
$env:FIGMA_API_KEY = "your-figma-api-key"
$env:SKETCH_API_KEY = "your-sketch-api-key"
$env:MG_MCP_TOKEN = "your-mastergo-token"
$env:MODAO_TOKEN = "your-modao-token"
```

---

## 📄 报告输出

所有报告保存到项目 `reports/` 目录：

| 报告类型 | 文件名模式 | 来源 |
|----------|------------|------|
| 代码评审 | `code-review-YYYY-MM-DD-HHmmss.md` | `frontend-craft-review`、`frontend-code-review` |
| 安全审查 | `security-review-YYYY-MM-DD-HHmmss.md` | `security-review` |
| 无障碍 | `accessibility-review-YYYY-MM-DD-HHmmss.md` | `accessibility-check` |
| 性能 | `performance-review-YYYY-MM-DD-HHmmss.md` | `performance-optimizer` |
| 架构 | `architecture-proposal-YYYY-MM-DD-HHmmss.md` | `frontend-architect` |
| 设计还原度 | `ui-fidelity-review-YYYY-MM-DD-HHmmss.md` | `ui-checker` |
| 设计实现 | `design-implementation-YYYY-MM-DD-HHmmss.md` | `figma-implementer` |
| Token 映射 | `token-mapping-YYYY-MM-DD-HHmmss.md` | `design-token-mapper` |
| 设计计划 | `design-plan-YYYY-MM-DD-HHmmss.md` | `implement-from-design` |
| 测试修复 | `test-fix-YYYY-MM-DD-HHmmss.md` | `test-and-fix` |
| 迁移计划 | `migration-plan-YYYY-MM-DD-HHmmss.md` | `legacy-to-modern-migration` |

> **建议**：在 `.gitignore` 中添加 `reports/` 避免提交自动生成的报告。

---

## 📥 更新

使用 Git 子模块安装时：

```bash
git submodule update --remote .frontend-craft
cp -r .frontend-craft/.agents .frontend-craft/.codex .
```

用户级安装时，重新复制更新后的 skills 和 agents。

---

## 🎯 关键概念

### Skills

Codex skills 是包含 `name` 和 `description` 的工作流定义，位于 `SKILL.md`。任务与描述匹配时 Codex 可隐式调用，也可通过 `$skill-name` 或提示词显式调用。

### 自定义子代理

自定义子代理定义在 `.codex/agents/*.toml`，包含 `name`、`description`、`developer_instructions`。需要专项分析（如架构、性能、设计还原度）时，在提示词中显式调用。

### Scripts（可选）

Codex 不支持 Hooks。`scripts/` 目录中的脚本可手动集成到 pre-commit、CI，或在 `AGENTS.md` 中引用，由 Codex 在适当时机执行。

---

## 📄 许可证

MIT — 可自由使用、修改，欢迎贡献。

---

**如果这个仓库有帮助，请给它一个 Star。构建一些很棒的前端。**
