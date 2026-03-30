# Vue 规则

当仓库或目标模块使用 Vue 时，应用本文件。

## 技术栈

<!-- 请根据项目实际情况修改 -->

- 框架: Vue 3 + TypeScript
- 状态管理: Pinia
- UI 组件库: 按项目实际选择（如 Element Plus、Naive UI、Vant 或内部 Design System）
- 版本与依赖：新建模块、补充 `package.json` 或更新本节前，优先采用彼此兼容的主流稳定版本（对齐官方文档、脚手架默认值或包管理器推荐），避免混用已停止维护或与仓库主线 major 不匹配的依赖。

## Vue 组件规范

- 使用 `<script setup lang="ts">`
- 明确使用 `defineProps` 和 `defineEmits`
- 保持模板逻辑简单、可读
- 将可复用逻辑提取到 composables
- 优先使用 computed，而不是大范围 watcher
- 保持组件职责聚焦，避免上帝组件
- props、emits、refs 和 expose 方法尽量使用强类型

## Vue 实现指导

创建新组件前：

1. 先搜索项目中是否已有可复用组件
2. 判断逻辑是否适合提取到 composable
3. 检查样式是否应沿用周边现有模式

编辑 Vue 组件时：

- 在可能的情况下，不要把 API 调用直接放进纯展示组件
- 不要在组件文件中内联大段业务逻辑
- 不要重复维护可从 props 或 store 推导出的状态
- 事件 payload 要明确且有类型约束

## Vue 文件组织

优先遵循项目已有约定。
常见输出可能包括：

- `ComponentName.vue`
- `types.ts`
- `useXxx.ts`
- 只有在符合仓库模式时才新增本地样式文件

## Vue 反模式

避免：

- 本该使用 computed 却使用大范围 watcher
- 对 props、emits 或 refs 无理由使用 `any`
- 模板分支层级过深却不提取
- 在一个组件中混入无关职责
- 用大范围全局样式覆盖去解决局部 UI 问题
