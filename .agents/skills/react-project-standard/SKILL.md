---
name: react-project-standard
description: React + TypeScript 项目的完整工程规范，涵盖项目结构、组件设计、Hooks、路由、状态管理、API 层、错误处理、测试和性能优化。当用户在 React 项目中创建、修改组件或模块，涉及架构设计、代码编写时自动激活。
version: 2.0.0
---

# React 项目规范

适用于使用 React + TypeScript 的仓库。

## 项目结构

以下为中大型 React 项目的业界最佳实践结构，按项目实际情况裁剪：

```
src/
├── app/                        # 应用入口与全局配置
│   ├── App.tsx                 # 根组件（Provider 组合）
│   ├── routes.tsx              # 路由配置
│   └── providers.tsx           # 全局 Provider 组装
│
├── pages/                      # 页面组件（与路由一一对应）
│   ├── Dashboard/
│   │   ├── DashboardPage.tsx
│   │   ├── components/         # 页面私有组件
│   │   └── hooks/              # 页面私有 hooks
│   ├── UserList/
│   └── Settings/
│
├── layouts/                    # 布局组件
│   ├── MainLayout.tsx          # 主布局（侧边栏 + 顶栏 + 内容区）
│   ├── AuthLayout.tsx          # 登录/注册页布局
│   └── BlankLayout.tsx         # 空白布局（错误页等）
│
├── features/                   # 功能模块（按业务领域划分）
│   ├── auth/
│   │   ├── components/         # 模块组件
│   │   ├── hooks/              # 模块 hooks
│   │   ├── api.ts              # 模块 API 调用
│   │   ├── types.ts            # 模块类型定义
│   │   ├── constants.ts        # 模块常量
│   │   └── index.ts            # 模块公开导出
│   └── order/
│
├── components/                 # 全局共享 UI 组件
│   ├── Button/
│   │   ├── Button.tsx
│   │   ├── Button.module.css
│   │   └── __tests__/
│   ├── Modal/
│   ├── Form/
│   └── ErrorBoundary/
│
├── hooks/                      # 全局共享 hooks
│   ├── useAuth.ts
│   ├── useDebounce.ts
│   └── useMediaQuery.ts
│
├── services/                   # API 基础层
│   ├── request.ts              # Axios/fetch 实例与拦截器
│   └── endpoints/              # API 端点定义（如按领域拆分）
│
├── stores/                     # 全局状态管理
│   ├── authStore.ts
│   └── uiStore.ts
│
├── locales/                    # 国际化语言包
│   ├── zh-CN.json              # 中文
│   ├── en-US.json              # 英文
│   └── index.ts                # i18n 实例初始化（i18next / react-intl）
│
├── assets/                     # 静态资源
│   ├── images/                 # 图片（PNG、JPG、WebP）
│   ├── icons/                  # SVG 图标
│   └── fonts/                  # 自定义字体
│
├── config/                     # 应用配置
│   ├── env.ts                  # 环境变量类型化封装
│   └── features.ts             # Feature Flags 管理
│
├── types/                      # 全局共享类型
│   ├── api.ts                  # API 响应/请求通用类型
│   ├── models.ts               # 业务实体类型
│   └── global.d.ts             # 全局类型扩展（图片模块声明等）
│
├── utils/                      # 纯工具函数
│   ├── format.ts               # 日期、数字、货币格式化
│   ├── validators.ts           # 表单校验规则
│   └── storage.ts              # LocalStorage / SessionStorage 封装
│
├── styles/                     # 全局样式与主题
│   ├── global.css              # 全局基础样式（reset / normalize）
│   ├── variables.css           # CSS 变量（颜色、间距、字号）
│   ├── breakpoints.ts          # 响应式断点常量
│   └── themes/                 # 主题定义
│       ├── light.css           # 亮色主题变量
│       ├── dark.css            # 暗色主题变量
│       └── index.ts            # 主题切换逻辑
│
└── constants/                  # 全局常量
    ├── routes.ts               # 路由路径常量
    └── config.ts               # 业务常量（分页大小、超时时间等）
```

### 关键原则

- `pages/` 做路由映射和布局组合，不放业务逻辑
- `layouts/` 定义页面骨架（侧边栏、顶栏、面包屑），由路由配置引用
- `features/` 按业务领域划分，模块内自包含（components + hooks + api + types）
- `components/` 仅放无业务耦合的通用组件，可跨项目复用
- `hooks/` 仅放通用逻辑（防抖、媒体查询等），业务 hooks 放到对应 feature 中
- `locales/` 存放语言包 JSON 文件，组件中使用 `t('key')` 而非硬编码文案
- `assets/` 存放静态资源，图标优先使用 SVG，图片优先使用 WebP/AVIF
- `config/` 封装环境变量和 Feature Flags，禁止组件中直接读取 `import.meta.env`
- `styles/themes/` 通过 CSS 变量实现主题切换，组件中引用变量而非硬编码颜色
- 每个模块通过 `index.ts` 管控公开 API，避免深层路径导入

## 组件设计规范

- 使用函数组件和 TypeScript
- 保持组件职责单一、可组合
- 将可复用逻辑提取到 hooks
- 在合适场景优先使用受控组件 API
- props 定义清晰且类型明确
- 优先复用现有设计系统组件
- 保持可访问性与键盘交互
- 避免过深的 JSX 嵌套和重复分支
- 对可推导的值不要额外存 state

### 组件文件结构

```
ComponentName/
├── ComponentName.tsx
├── ComponentName.types.ts       # 类型定义（如需独立）
├── ComponentName.module.css     # 样式（如需）
├── hooks/
│   └── useComponentLogic.ts
├── components/
│   └── SubComponent.tsx
└── __tests__/
    └── ComponentName.spec.tsx
```

### 组件分层

```
页面组件 (Pages)        → 路由映射、布局组合
  └── 容器组件 (Containers) → 数据获取、状态编排
       └── 业务组件 (Features) → 领域逻辑展示
            └── 通用组件 (UI) → 纯展示，无业务耦合
```

## TypeScript 规范

- Props interface 命名: `ComponentNameProps`
- 事件处理函数: `handle` 前缀（如 `handleClick`）
- 回调 Props: `on` 前缀（如 `onChange`、`onSubmit`）
- 禁止使用 `any`，优先使用 `unknown` 或精确类型
- 泛型组件使用 `<T>` 约束，保持类型推导

```tsx
interface TableProps<T extends Record<string, unknown>> {
    data: T[];
    columns: ColumnDef<T>[];
    onRowClick?: (row: T) => void;
}
```

## Hooks 规范

### 自定义 Hook 设计

- 以 `use` 前缀命名
- 返回值使用对象（而非数组），方便按需解构
- 状态和行为封装在一起，组件只消费结果
- Hook 内部处理 loading / error / data 三态

```tsx
function useUserList(params: QueryParams) {
    const [data, setData] = useState<User[]>([]);
    const [loading, setLoading] = useState(false);
    const [error, setError] = useState<Error | null>(null);

    const fetch = useCallback(async () => {
        setLoading(true);
        setError(null);
        try {
            const res = await getUserList(params);
            setData(res.list);
        } catch (e) {
            setError(e as Error);
        } finally {
            setLoading(false);
        }
    }, [params]);

    useEffect(() => { fetch(); }, [fetch]);

    return { data, loading, error, refetch: fetch };
}
```

### Hook 使用原则

- `useEffect` 必须有正确的依赖数组和清理函数
- `useMemo` / `useCallback` 仅在子组件使用 memo 或依赖稳定性重要时使用
- 不要在条件分支或循环中调用 hooks
- 数据请求场景优先使用 React Query / SWR 等库（如项目已引入）

## 路由规范

### 路由组织

```tsx
// app/routes.tsx
const routes: RouteObject[] = [
    {
        path: '/',
        element: <MainLayout />,
        children: [
            { index: true, element: <DashboardPage /> },
            { path: 'users', element: <UserListPage /> },
            { path: 'users/:id', element: <UserDetailPage /> },
            { path: 'settings', element: <SettingsPage /> },
        ],
    },
    { path: '/login', element: <LoginPage /> },
    { path: '*', element: <NotFoundPage /> },
];
```

### 路由原则

- 路由配置集中管理，路径常量化
- 页面组件使用 `lazy` + `Suspense` 按需加载
- 权限路由使用 guard 组件包裹，而非在每个页面内判断
- URL 参数（分页、筛选、排序）与路由状态同步

```tsx
const UserListPage = lazy(() => import('@/pages/UserList/UserListPage'));

function ProtectedRoute({ children }: { children: React.ReactNode }) {
    const { isAuthenticated } = useAuth();
    if (!isAuthenticated) return <Navigate to="/login" replace />;
    return <>{children}</>;
}
```

## 状态管理

| 状态类型 | 推荐方案 |
|----------|----------|
| 组件内临时 UI 状态 | `useState` / `useReducer` |
| 跨组件共享业务状态 | 全局 store（Zustand / Redux Toolkit） |
| 服务端数据缓存 | React Query / SWR |
| URL 驱动状态 | 路由参数 / `useSearchParams` |
| 表单状态 | React Hook Form / Formik |

### 核心原则

- 就近管理：状态放在需要它的最近公共祖先
- 单一数据源：同一份数据只在一个地方维护
- 派生优于同步：可计算的值直接在渲染中计算
- 服务端数据用请求库管理，而非手动存入 store

## API 层规范

### 请求实例

```typescript
// services/request.ts
const request = axios.create({
    baseURL: import.meta.env.VITE_API_BASE_URL,
    timeout: 10000,
});

request.interceptors.response.use(
    (res) => res.data,
    (error) => {
        if (error.response?.status === 401) {
            redirectToLogin();
        }
        return Promise.reject(normalizeError(error));
    },
);
```

### API 函数

```typescript
// features/user/api.ts
export function getUserList(params: UserQueryParams): Promise<PageResult<User>> {
    return request.get('/users', { params });
}

export function updateUser(id: string, data: UpdateUserDTO): Promise<User> {
    return request.put(`/users/${id}`, data);
}
```

- API 函数按 feature 组织，而非全部堆在一个文件
- 请求参数和响应都有类型约束
- 拦截器统一处理认证、错误格式化、loading 提示

## 错误处理

### Error Boundary

每个功能模块应有 Error Boundary 包裹，避免局部错误导致全页白屏：

```tsx
<ErrorBoundary fallback={<ModuleErrorFallback />}>
    <UserDashboard />
</ErrorBoundary>
```

### 异步错误

- 数据请求失败必须有用户可见的错误提示
- 提供重试机制
- 不要吞掉错误（空 catch 块）

## Suspense 与懒加载

```tsx
const HeavyChart = lazy(() => import('./components/HeavyChart'));

function Dashboard() {
    return (
        <Suspense fallback={<ChartSkeleton />}>
            <HeavyChart data={chartData} />
        </Suspense>
    );
}
```

- 路由级组件使用 `lazy` + `Suspense`
- 重型第三方组件（图表、编辑器、地图）按需加载
- `fallback` 使用 Skeleton 而非简单 spinner

## 样式规范

- 与项目现有样式体系保持一致（Tailwind / CSS Modules / styled-components 等）
- 复杂动画或特殊样式使用 CSS Modules 或项目约定方案
- 禁止内联样式（除动态值外）
- 响应式处理需与项目断点约定一致
- 主题/全局变量通过 CSS 变量或 Token 管理

## 测试规范

### 必须测试

- 核心交互行为（点击、输入、提交）
- 条件渲染（loading / error / empty / data）
- 关键 hooks 的返回值和副作用
- API 调用 mock 与集成测试

### 测试风格

```tsx
describe('UserForm', () => {
    it('should submit with valid data', async () => {
        const onSubmit = vi.fn();
        render(<UserForm onSubmit={onSubmit} />);

        await userEvent.type(screen.getByLabelText('用户名'), 'test');
        await userEvent.click(screen.getByRole('button', { name: '提交' }));

        expect(onSubmit).toHaveBeenCalledWith({ username: 'test' });
    });

    it('should show error on invalid input', async () => {
        render(<UserForm onSubmit={vi.fn()} />);
        await userEvent.click(screen.getByRole('button', { name: '提交' }));
        expect(screen.getByText('用户名不能为空')).toBeInTheDocument();
    });
});
```

- 使用 `screen.getByRole` / `getByLabelText` 而非 `getByTestId`
- 测试用户行为，而非实现细节
- 避免测试组件内部 state

## 性能

- 合理使用 `React.memo`、`useMemo`、`useCallback`
- 列表渲染必须有稳定的 `key`
- 避免在渲染函数内创建新对象/数组/函数
- 大列表使用虚拟滚动（react-window / react-virtuoso）
- 避免在顶层 context 中放置高频变化的值
- 路由级 code splitting，重型组件 lazy load

## 反模式

- 用 prop drilling 传递过多层级而不考虑组合方案
- 对局部问题过度使用 context
- 在确实有影响的情况下仍使用不稳定回调
- 在同一个文件里同时混合数据请求、视图渲染和命令式 DOM 逻辑
- 无充分理由引入第二套样式方案
- 在 useEffect 中做可以在事件处理函数中完成的事
- 用 `useEffect` + `setState` 模拟 computed（应直接在渲染中计算）
- 将所有状态推入全局 store，而非就近管理
- 在 `components/` 中放业务耦合组件
- 直接从 feature 内部深层路径导入，绕过 `index.ts`

## 输出检查清单

- [ ] 文件结构与项目约定一致（pages / features / components 分离）
- [ ] Props 类型完整且明确
- [ ] 可复用逻辑已提取到 hooks
- [ ] Error Boundary 已包裹关键模块
- [ ] Loading / Error / Empty 状态均已处理
- [ ] 路由组件使用 lazy 加载
- [ ] 状态管理方案合理（就近原则）
- [ ] API 调用有类型约束和统一错误处理
- [ ] 样式接入方式与仓库保持一致
- [ ] 关键行为有测试覆盖
