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

[**English**](../../README.md) | [简体中文](../../README.zh-CN.md) | [繁體中文](../zh-TW/README.md) | [日本語](README.md) | [한국어](../ko-KR/README.md)

</div>

---

**エンタープライズフロントエンドチーム向け Codex プラグイン。**

コードレビュー、セキュリティレビュー、デザイン実装（Figma/Sketch/MasterGo/Pixso/墨刀/摹客）、アクセシビリティチェック、自動品質保証、プロジェクトテンプレートを統合。すべてのレビュー・分析・評価レポートはプロジェクトの `reports/` ディレクトリに Markdown ファイルとして自動保存されます。

---

## 🚀 クイックスタート

### ステップ 1：プラグインをインストール

**方式一：プロジェクトレベル（推奨）**

```bash
git submodule add https://github.com/bovinphang/frontend-craft-codex.git .frontend-craft
cp -r .frontend-craft/.agents .frontend-craft/.codex .
```

**方式二：ユーザーレベル**

```bash
git clone https://github.com/bovinphang/frontend-craft-codex.git .frontend-craft
cp -r .frontend-craft/.agents/skills/* ~/.agents/skills/
cp -r .frontend-craft/.codex/agents/* ~/.codex/agents/
```

### ステップ 2：プロジェクト設定を初期化（推奨）

`$frontend-craft-init` skill を呼び出すか、Codex に依頼：

```
frontend-craft-init skill を使ってプロジェクトテンプレートを .codex/ に初期化してください
```

### ステップ 3：使い始める

```
# コードレビュー
frontend-craft-review または frontend-code-review skill を使用

# ページ/機能/コンポーネント作成
frontend-craft-scaffold skill を使用

# サブエージェントを明示的に呼び出し
frontend-architect でコンポーネントアーキテクチャを分析
performance-optimizer でパフォーマンス分析
```

✨ **完了！** 9 つのカスタムエージェント、16 の skills が利用可能です。

---

## 🌐 マルチエージェント向けスキル（Skills CLI）

**Claude Code**、**OpenAI Codex**、**Cursor**、**OpenCode**、**Gemini CLI**、**OpenClaw**、**Continue**、**CodeBuddy**、**Trae**、**Kimi Code CLI** など複数の AI コーディングエージェントを使う場合、[Skills CLI](https://skills.sh/docs/cli)（`npx skills`）で正規のスキル源リポジトリ [`bovinphang/frontend-craft`](https://github.com/bovinphang/frontend-craft) から**ワークフロースキル**を各ツールのスキルディレクトリにインストールできます。CLI は数十種類のエージェントに対応します。一覧は対話プロンプトまたは公式ドキュメントを参照してください。

**Skills CLI と本 Codex リポジトリの違い**

- **Skills CLI** — `bovinphang/frontend-craft` からスキルパッケージを、選択したエージェント用のパスに配置します。ツール横断でレビューやフロントエンド規約を揃えたいとき向けです。
- **本リポジトリ** — **Codex** 向けレイアウト（[`.agents/skills/`](../../.agents/skills/)、[`.codex/agents/`](../../.codex/agents/)、Codex 用の init/review/scaffold など）を、前述の **クイックスタート**（サブモジュールまたはコピー）で提供します。

**要件:** Node.js ≥ 18。

**スキルのインストール**

```bash
npx skills add bovinphang/frontend-craft
```

プロジェクト／グローバル（`-g`）、シンボリックリンク／コピー（`--copy`）、対象エージェントなどはプロンプトに従って選択します。インストールせずリポジトリ内のスキル一覧だけ見る場合は `npx skills add bovinphang/frontend-craft -l` を使います。特定のスキルやエージェントだけ入れる場合は `--skill` / `--agent`（`npx skills --help` 参照）。

**スキルの更新**

スキルをインストールしたプロジェクトのディレクトリで（グローバル導入の場合はそのスコープで）実行します。

```bash
npx skills update
```

インストール済みスキルを最新版に更新します。事前に `npx skills check` で更新の有無を確認できます。

**テレメトリ:** CLI は既定で匿名テレメトリを収集する場合があります。無効化するには環境変数 `DISABLE_TELEMETRY=1` を設定してください。詳細は [skills.sh CLI ドキュメント](https://skills.sh/docs/cli) を参照してください。

---

## 📦 ディレクトリ構造

```
frontend-craft-codex/
├── .agents/skills/     # Codex Skills（16 個）
├── .codex/agents/     # カスタムサブエージェント（9 個）
└── scripts/           # オプション：手動統合スクリプト
```

---

## 📋 機能概要

### Skills

| Skill | 用途 |
|-------|------|
| `frontend-code-review` | アーキテクチャ、型、レンダリング、スタイル、a11y レビュー |
| `frontend-craft-review` | 指定ファイルまたは最近の Git 変更のレビュー |
| `frontend-craft-init` | プロジェクトテンプレートの初期化 |
| `frontend-craft-scaffold` | page/feature/component の作成 |
| `security-review` | セキュリティレビュー |
| `accessibility-check` | アクセシビリティチェック |
| `implement-from-design` | デザイン実装 |
| `test-and-fix` | 検証と修正 |
| 等 | ... |

### カスタムサブエージェント

| Agent | 用途 |
|-------|------|
| `frontend-architect` | アーキテクチャ設計 |
| `performance-optimizer` | パフォーマンス最適化 |
| `ui-checker` | UI 忠実度チェック |
| `figma-implementer` | デザイン実装 |
| `design-token-mapper` | Token マッピング |
| `frontend-code-reviewer` | フロントエンドコードレビュー |
| `frontend-security-reviewer` | ブラウザ側セキュリティレビュー |
| `frontend-e2e-runner` | E2E / Playwright |
| `typescript-reviewer` | TypeScript / JavaScript レビュー |

---

## 📄 ライセンス

MIT - 自由に使用・改変可能。貢献歓迎。

---

**このリポジトリが役に立ったら Star をお願いします。** 詳細は [English](../../README.md) または [简体中文](../../README.zh-CN.md) をご覧ください。
