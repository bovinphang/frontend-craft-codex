# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- `code-comments.md` 规则模板（前端代码注释规范），已纳入 `frontend-craft-init` 复制清单与 `AGENTS.md` 规则索引

## [2.0.0] - 2025-03-18

### Added

- **Codex 插件支持** — 完整转换为 Codex 插件格式
- `.agents/skills/` — 16 个 Codex Skills（含 frontend-craft-init、frontend-craft-review、frontend-craft-scaffold）
- `.codex/agents/` — 5 个自定义子代理（TOML 格式）
- `frontend-craft-init` — 初始化 AGENTS.md、config.toml、rules 到项目
- `frontend-craft-review` — 支持 Git 范围的代码评审
- `frontend-craft-scaffold` — 创建 page/feature/component 脚手架
- Codex 格式模板：AGENTS.md、config.toml（替代 CLAUDE.md、settings.json）

### Changed

- README 更新为 Codex 安装与使用说明
- 子代理由 Markdown 转为 TOML 格式
- 项目配置由 .claude/ 转为 .codex/ 与 AGENTS.md

### Note

- Codex 不支持 Hooks，scripts/ 可手动集成到 pre-commit 或 CI

---

## [1.1.0] - 2025-03-18

### Added

- `legacy-to-modern-migration` skill — jQuery/MPA 迁移至 React/Vue 3 + TS 的策略与流程
- `e2e-testing` skill — Playwright/Cypress E2E 测试规范
- `nextjs-project-standard` skill — Next.js 项目规范（App Router、SSR/SSG）
- `nuxt-project-standard` skill — Nuxt 3 项目规范（SSR/SSG）
- `monorepo-project-standard` skill — Monorepo 项目规范
- `rules/ci-cd.md` 模板 — CI/CD 流水线规范
- `rules/refactoring.md` 模板 — 重构项目约束（图片、样式、功能等价）
- CONTRIBUTING.md — 贡献指南
- CHANGELOG.md — 版本变更记录

### Changed

- `testing.md` — 补充 E2E 测试规则
- `frontend-architect` agent — 增加 `legacy-to-modern-migration` skill 引用
- `legacy-to-modern-migration` skill — 新增重构实施要求：图片（使用原项目资源、禁止内联 SVG）、样式（参考效果不照搬 CSS、优先 flex、禁止内联样式）、目标（视觉交互一致、功能等价、代码更简洁易维护）

---

## [1.0.0] - 2025-03-18

### Added

- 初始发布
- 5 个 Agents：frontend-architect、performance-optimizer、ui-checker、figma-implementer、design-token-mapper
- 9 个 Skills：frontend-code-review、security-review、accessibility-check、react-project-standard、vue3-project-standard、implement-from-design、test-and-fix、legacy-web-standard、legacy-to-modern-migration
- 3 个 Commands：init、review、scaffold
- Hooks：SessionStart、PreToolUse、PostToolUse、Stop、Notification
- 11 个规则模板：CLAUDE.md、settings.json、vue、react、design-system、testing、git-conventions、i18n、performance、api-layer、state-management、error-handling、naming-conventions
- MCP 集成：Figma、Sketch、MasterGo、Pixso、墨刀
- 多语言 README：English、简体中文、繁體中文、日本語、한국어
- 报告自动保存为 Markdown 至 `reports/` 目录
