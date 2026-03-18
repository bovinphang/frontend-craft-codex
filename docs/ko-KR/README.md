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

[**English**](../../README.md) | [简体中文](../../README.zh-CN.md) | [繁體中文](../zh-TW/README.md) | [日本語](../ja-JP/README.md) | [한국어](README.md)

</div>

---

**엔터프라이즈 프론트엔드 팀을 위한 Codex 플러그인.**

코드 리뷰, 보안 리뷰, 디자인 구현(Figma/Sketch/MasterGo/Pixso/墨刀/摹客), 접근성 검사, 자동화된 품질 보증, 프로젝트 템플릿을 통합합니다. 모든 리뷰·분석·평가 보고서는 프로젝트 `reports/` 디렉터리에 Markdown 파일로 자동 저장됩니다.

---

## 🚀 빠른 시작

### 1단계: 플러그인 설치

**방식 1: 프로젝트 수준 (권장)**

```bash
git submodule add https://github.com/bovinphang/frontend-craft-codex.git .frontend-craft
cp -r .frontend-craft/.agents .frontend-craft/.codex .
```

**방식 2: 사용자 수준**

```bash
git clone https://github.com/bovinphang/frontend-craft-codex.git .frontend-craft
cp -r .frontend-craft/.agents/skills/* ~/.agents/skills/
cp -r .frontend-craft/.codex/agents/* ~/.codex/agents/
```

### 2단계: 프로젝트 설정 초기화 (권장)

`$frontend-craft-init` skill을 호출하거나 Codex에 요청:

```
frontend-craft-init skill을 사용하여 프로젝트 템플릿을 .codex/에 초기화해 주세요
```

### 3단계: 사용 시작

```
# 코드 리뷰
frontend-craft-review 또는 frontend-code-review skill 사용

# 페이지/기능/컴포넌트 생성
frontend-craft-scaffold skill 사용

# 서브에이전트 명시적 호출
frontend-architect로 컴포넌트 아키텍처 분석
performance-optimizer로 성능 분석
```

✨ **완료!** 5개의 커스텀 에이전트, 16개의 skills를 사용할 수 있습니다.

---

## 📦 디렉터리 구조

```
frontend-craft-codex/
├── .agents/skills/     # Codex Skills (16개)
├── .codex/agents/     # 커스텀 서브에이전트 (5개)
└── scripts/           # 선택: 수동 통합 스크립트
```

---

## 📋 기능 개요

### Skills

| Skill | 용도 |
|-------|------|
| `frontend-code-review` | 아키텍처, 타입, 렌더링, 스타일, a11y 리뷰 |
| `frontend-craft-review` | 지정 파일 또는 최근 Git 변경 리뷰 |
| `frontend-craft-init` | 프로젝트 템플릿 초기화 |
| `frontend-craft-scaffold` | page/feature/component 생성 |
| `security-review` | 보안 리뷰 |
| `accessibility-check` | 접근성 검사 |
| `implement-from-design` | 디자인 구현 |
| `test-and-fix` | 검증 및 수정 |
| 등 | ... |

### 커스텀 서브에이전트

| Agent | 용도 |
|-------|------|
| `frontend-architect` | 아키텍처 설계 |
| `performance-optimizer` | 성능 최적화 |
| `ui-checker` | UI 충실도 검사 |
| `figma-implementer` | 디자인 구현 |
| `design-token-mapper` | Token 매핑 |

---

## 📄 라이선스

MIT - 자유롭게 사용·수정 가능. 기여 환영.

---

**이 리포지토리가 도움이 되었다면 Star를 눌러 주세요.** 자세한 내용은 [English](../../README.md) 또는 [简体中文](../../README.zh-CN.md)를 참조하세요.
