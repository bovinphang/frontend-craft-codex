---
name: frontend-craft-init
description: 将 frontend-craft 的项目模板（AGENTS.md、config.toml、rules）初始化到当前项目的 .codex 目录和仓库根目录。当用户要求初始化项目配置、设置 Codex 项目模板时自动激活。
---

# Frontend Craft 项目初始化

将 frontend-craft 提供的 Codex 项目模板复制到当前项目中。

## 执行步骤

1. 检查当前项目根目录下是否已存在 `AGENTS.md` 和 `.codex/` 目录。

2. 如果 `AGENTS.md` 已存在，提示用户确认是否覆盖。不要在未确认的情况下覆盖现有文件。

3. 将以下模板文件从本 skill 的 `templates/` 目录复制到项目：

   **从 `.agents/skills/frontend-craft-init/templates/` 复制：**

   - `templates/AGENTS.md` → 项目根目录 `AGENTS.md`
   - `templates/config.toml` → `.codex/config.toml`
   - `templates/rules/vue.md` → `.codex/rules/vue.md`
   - `templates/rules/react.md` → `.codex/rules/react.md`
   - `templates/rules/design-system.md` → `.codex/rules/design-system.md`
   - `templates/rules/testing.md` → `.codex/rules/testing.md`
   - `templates/rules/git-conventions.md` → `.codex/rules/git-conventions.md`
   - `templates/rules/i18n.md` → `.codex/rules/i18n.md`
   - `templates/rules/performance.md` → `.codex/rules/performance.md`
   - `templates/rules/api-layer.md` → `.codex/rules/api-layer.md`
   - `templates/rules/state-management.md` → `.codex/rules/state-management.md`
   - `templates/rules/error-handling.md` → `.codex/rules/error-handling.md`
   - `templates/rules/naming-conventions.md` → `.codex/rules/naming-conventions.md`
   - `templates/rules/ci-cd.md` → `.codex/rules/ci-cd.md`
   - `templates/rules/refactoring.md` → `.codex/rules/refactoring.md`

4. 复制时需确定本 skill 的 templates 路径。若项目通过 git submodule 安装 frontend-craft-codex 于 `.frontend-craft/`，则模板路径为 `.frontend-craft/.agents/skills/frontend-craft-init/templates/`。若 skills 直接位于 `.agents/skills/`，则路径为 `.agents/skills/frontend-craft-init/templates/`。

5. 复制完成后，提醒用户：
   - 根据项目实际技术栈修改 `AGENTS.md` 中的项目基础信息和常用命令
   - 删除项目不使用的规则（如纯 React 项目删除 `vue.md`，不需要 i18n 的项目删除 `i18n.md`）
   - 根据项目实际情况修改 `rules/react.md` 或 `rules/vue.md` 中的技术栈配置
   - 检查 `.codex/config.toml` 中的 MCP 配置是否符合项目需求

6. 输出初始化完成的确认信息和文件清单。
