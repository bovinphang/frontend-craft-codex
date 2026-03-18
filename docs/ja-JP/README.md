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

✨ **完了！** 5 つのカスタムエージェント、16 の skills が利用可能です。

---

## 📦 ディレクトリ構造

```
frontend-craft-codex/
├── .agents/skills/     # Codex Skills（16 個）
├── .codex/agents/     # カスタムサブエージェント（5 個）
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

---

## 📄 ライセンス

MIT - 自由に使用・改変可能。貢献歓迎。

---

**このリポジトリが役に立ったら Star をお願いします。** 詳細は [English](../../README.md) または [简体中文](../../README.zh-CN.md) をご覧ください。
