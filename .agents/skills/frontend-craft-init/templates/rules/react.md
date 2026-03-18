# React 规则

当仓库或目标模块使用 React 时，应用本文件。

## 技术栈

<!-- 请根据项目实际情况修改 -->

- 框架: React + TypeScript
- 样式: Tailwind CSS + CSS Modules
- 状态管理: Zustand / Redux Toolkit / Jotai（按项目实际选择）
- UI 组件库: 按项目实际选择（如 Ant Design、Material UI 或内部 Design System）

## React 组件规范

- 使用函数组件和 TypeScript
- 保持组件小而可组合
- 将可复用逻辑提取到 hooks
- props 保持明确且类型清晰
- 保持可访问性与键盘交互
- 优先使用可推导状态，避免重复维护 state
- 在创建新基础组件前，先复用现有设计系统
- 禁止使用 any，优先使用 unknown
- CSS 命名遵循 BEM（CSS Modules 场景）

## React 实现指导

创建新组件前：

1. 先搜索是否已存在等价组件
2. 判断逻辑是否应该放入自定义 hook
3. 与项目当前样式方案保持一致

编辑 React 组件时：

- 避免在同一个文件里混合数据请求、重业务逻辑和展示逻辑
- 避免设计过宽或语义不清的 props API
- 对局部问题避免滥用 context
- 保持条件渲染可读，必要时提取重复分支

## React 文件组织

优先遵循仓库已有约定。
常见输出可能包括：

- `Component.tsx`
- `Component.types.ts`
- `hooks/useComponentLogic.ts`
- `Component.module.css`
- 如果仓库采用就近测试，则补充测试文件，如：`__tests__/Component.spec.tsx`

## React 反模式

避免：

- 对可推导值使用多余 state
- 大段 JSX 不拆成子组件
- 使用不稳定 key
- 在 props 和 hooks 中无理由使用 `any`
- 没有充分理由时引入第二套样式体系
