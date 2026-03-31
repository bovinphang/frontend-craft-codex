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

[**English**](../../README.md) | [简体中文](../../README.zh-CN.md) | [繁體中文](README.md) | [日本語](../ja-JP/README.md) | [한국어](../ko-KR/README.md)

</div>

---

**面向企業前端團隊的 Codex 插件。**

整合程式碼審查、安全審查、設計稿轉程式碼（Figma/Sketch/MasterGo/Pixso/墨刀/摹客）、無障礙檢查、自動化品質保障與專案範本。所有審查、分析與評估報告均自動儲存為 Markdown 檔案至專案 `reports/` 目錄，便於歸檔、追溯與團隊共享。

---

## 🚀 快速開始

### 第一步：安裝插件

**方式一：專案級安裝（建議）**

```bash
git submodule add https://github.com/bovinphang/frontend-craft-codex.git .frontend-craft
cp -r .frontend-craft/.agents .frontend-craft/.codex .
```

**方式二：使用者級安裝**

```bash
git clone https://github.com/bovinphang/frontend-craft-codex.git .frontend-craft
cp -r .frontend-craft/.agents/skills/* ~/.agents/skills/
cp -r .frontend-craft/.codex/agents/* ~/.codex/agents/
```

### 第二步：初始化專案設定（建議）

呼叫 `$frontend-craft-init` skill 或直接詢問 Codex：

```
請使用 frontend-craft-init skill 將專案範本初始化至 .codex/
```

### 第三步：開始使用

```
# 程式碼審查
使用 frontend-craft-review 或 frontend-code-review skill

# 建立頁面/功能/元件
使用 frontend-craft-scaffold skill

# 顯式呼叫子代理
使用 frontend-architect 分析元件架構
使用 performance-optimizer 進行效能分析
```

✨ **完成！** 您現在可使用 9 個自訂子代理、16 個 skills。

---

## 🌐 多代理技能安裝（Skills CLI）

若團隊同時使用 **Claude Code**、**OpenAI Codex**、**Cursor**、**OpenCode**、**Gemini CLI**、**OpenClaw**、**Continue**、**CodeBuddy**、**Trae**、**Kimi Code CLI** 等多種 AI 程式設計代理，可透過 [Skills CLI](https://skills.sh/docs/cli)（`npx skills`）將規範來源倉庫 [`bovinphang/frontend-craft`](https://github.com/bovinphang/frontend-craft) 中的**工作流技能**安裝到各工具約定的技能目錄。CLI 支援數十種代理；完整清單以互動提示或上游文件為準。

**Skills CLI 與本 Codex 倉庫的差異**

- **Skills CLI** — 從 `bovinphang/frontend-craft` 安裝技能封裝到所選代理的路徑，便於在多種工具間統一審查與前端規範。
- **本倉庫** — 提供 **Codex** 目錄結構（[`.agents/skills/`](../../.agents/skills/)、[`.codex/agents/`](../../.codex/agents/)，以及面向 Codex 的 init/review/scaffold 等技能），透過上文 **快速開始** 的子模組或複製方式使用。

**環境需求：** Node.js ≥ 18。

**安裝技能**

```bash
npx skills add bovinphang/frontend-craft
```

依提示選擇專案層級或全域安裝（`-g`）、符號連結或複製（`--copy`），以及要啟用的代理。若只想檢視倉庫內技能清單而不安裝，可執行 `npx skills add bovinphang/frontend-craft -l`。若需指定技能名稱或代理，可使用 `--skill` / `--agent`（詳見 `npx skills --help`）。

**更新技能**

在已安裝技能的專案目錄下執行（若為全域安裝，請使用對應範圍）：

```bash
npx skills update
```

此指令會將已安裝的技能更新至最新版本。亦可先執行 `npx skills check` 查看可用更新。

**遙測：** CLI 預設可能蒐集匿名遙測。若需關閉，請設定環境變數 `DISABLE_TELEMETRY=1`。說明見 [skills.sh CLI 文件](https://skills.sh/docs/cli)。

---

## 📦 目錄結構

```
frontend-craft-codex/
├── .agents/skills/     # Codex Skills（16 個）
├── .codex/agents/     # 自訂子代理（9 個）
└── scripts/           # 可選手動整合腳本
```

---

## 📋 功能概覽

### Skills

| Skill | 用途 |
|-------|------|
| `frontend-code-review` | 架構、型別、渲染、樣式、無障礙審查 |
| `frontend-craft-review` | 審查指定檔案或最近 Git 變更 |
| `frontend-craft-init` | 初始化專案範本 |
| `frontend-craft-scaffold` | 建立 page/feature/component |
| `security-review` | 安全審查 |
| `accessibility-check` | 無障礙檢查 |
| `implement-from-design` | 設計稿實作 |
| `test-and-fix` | 校驗與修復 |
| 等 | ... |

### 自訂子代理

| Agent | 用途 |
|-------|------|
| `frontend-architect` | 架構設計 |
| `performance-optimizer` | 效能優化 |
| `ui-checker` | UI 還原度檢查 |
| `figma-implementer` | 設計稿實作 |
| `design-token-mapper` | Token 對應 |
| `frontend-code-reviewer` | 前端程式碼審查 |
| `frontend-security-reviewer` | 瀏覽器端安全審查 |
| `frontend-e2e-runner` | E2E / Playwright |
| `typescript-reviewer` | TypeScript / JavaScript 審查 |

---

## 📄 授權條款

MIT - 自由使用、依需求修改，歡迎回饋。

---

**若本倉庫對您有幫助，請給予 Star。** 完整文件請參閱 [English](../../README.md) 或 [简体中文](../../README.zh-CN.md)。
