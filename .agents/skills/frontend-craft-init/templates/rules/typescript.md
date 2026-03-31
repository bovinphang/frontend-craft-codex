# TypeScript / JavaScript 规则

编写、修改或评审 `.ts`、`.tsx`、`.js`、`.jsx` 时应用本文件。注释风格另见 `code-comments.md`；E2E 与校验流程另见 `testing.md`。

## 类型与接口

用类型让对外 API、共享模型与组件 props 显式、可读、可复用。

### 对外导出的 API

- 对**导出**的函数、共享工具函数、公开类方法，写明参数与返回值类型。
- **局部**变量在类型显而易见时交给 TypeScript 推断。
- 重复出现的内联对象形状抽成具名 `interface` 或 `type`。

```typescript
// 错误：导出函数缺少显式类型
export function formatUser(user) {
  return `${user.firstName} ${user.lastName}`;
}

// 正确：对外 API 显式标注
interface User {
  firstName: string;
  lastName: string;
}

export function formatUser(user: User): string {
  return `${user.firstName} ${user.lastName}`;
}
```

### `interface` 与 `type`

- 可能被扩展或 `implements` 的**对象形状**优先用 `interface`。
- **联合、交叉、元组、映射类型、工具类型组合**用 `type`。
- 优先**字符串字面量联合**；仅在互操作或团队统一要求时使用 `enum`。

```typescript
interface User {
  id: string;
  email: string;
}

type UserRole = "admin" | "member";
type UserWithRole = User & { role: UserRole };
```

### 函数参数：复杂类型宜具名

- 参数上的**复杂联合**、**内联对象类型**、**较复杂的回调签名**等，应**优先**提取为具名 `type` / `interface`，再在函数签名中引用，便于阅读、复测与重构。
- **仅当**类型**简单**、**短小**、一眼可读，且**明显无复用**价值时，允许在参数位置内联（如单独的 `string`、`number`、`boolean` 等）。

```typescript
// 不推荐：联合与可选散落在参数上，语义不突出
function getUserInfo(id: string | number | undefined) {}

// 推荐：具名类型表达「用户标识」语义，可选更自然
type UserId = string | number;
function getUserInfo(id?: UserId) {}
```

```typescript
// 不推荐：内联联合对象冗长，难复用、难单测描述
function send(data: string | { content: string; type: "text" | "html" }) {}

// 推荐：消息载荷单一真源
type MessagePayload =
  | string
  | {
      content: string;
      type: "text" | "html";
    };

function send(data: MessagePayload) {}
```

### 避免 `any`

- 业务代码中避免 `any`。
- 外部或不可信数据用 `unknown`，再安全收窄。
- 类型随调用方变化时用泛型。

```typescript
// 错误：any 取消类型检查
function getErrorMessage(error: any) {
  return error.message;
}

// 正确：unknown 强制收窄
function getErrorMessage(error: unknown): string {
  if (error instanceof Error) {
    return error.message;
  }
  return "Unexpected error";
}
```

### React 组件 Props

- 用具名 `interface` 或 `type` 定义 props。
- 回调 props 写清参数与返回值。
- 无特殊理由不使用 `React.FC`（避免隐式 `children` 等差异）。

```typescript
interface User {
  id: string;
  email: string;
}

interface UserCardProps {
  user: User;
  onSelect: (id: string) => void;
}

function UserCard({ user, onSelect }: UserCardProps) {
  return <button onClick={() => onSelect(user.id)}>{user.email}</button>;
}
```

### 仍为 JavaScript 的文件

- 在 `.js` / `.jsx` 中，若短期无法迁 TS，可用 **JSDoc** 补类型，并与运行时行为一致。

```javascript
/**
 * @param {{ firstName: string, lastName: string }} user
 * @returns {string}
 */
export function formatUser(user) {
  return `${user.firstName} ${user.lastName}`;
}
```

## 禁止 Magic Number / Magic String

- **业务代码中禁止**使用**无语义**的硬编码数字或字符串（如 `1`、`2`、`3`、`"1"`、`"2"`、`"3"`）直接表示**状态、类型、标识或业务含义**（含 `if`/`switch`/赋值与 API 字段映射等）。
- **固定且有限的取值范围**须在单一真源处定义，并在全仓引用名称，避免裸值散落：
  - **`enum`**（与后端或协议对齐、或团队明确约定时使用；注意字符串 enum、const enum 与打包/tree-shaking 策略）；
  - **`as const` 常量对象**（常与 `typeof` / `keyof` 推导联合类型，适合前端主路径）；
  - **字面量联合类型**（`type Status = "a" | "b"`）并与上面对象或 map 配套，保证调用处可收窄、可重构。
- **不属本条**的典型例外（仍应保持可读）：纯算法下标、 obvious 的 `0`/`1` 长度判断、与业务无关的 UI 刻度若已有设计 Token 则改走 `design-system.md`。

```typescript
// 不佳：业务语义依赖裸数字 / 裸字符串
function label(status: number) {
  if (status === 1) return "待支付";
  if (status === 2) return "已支付";
  return "未知";
}
if (user.role === "3") {
  /* ... */
}

// 更佳：字面量联合 + as const 常量对象（或团队约定的 enum）
type OrderStatus = "pending" | "paid" | "cancelled";
const ORDER_STATUS = {
  Pending: "pending",
  Paid: "paid",
  Cancelled: "cancelled",
} as const satisfies Record<string, OrderStatus>;

function label(status: OrderStatus) {
  if (status === ORDER_STATUS.Pending) return "待支付";
  if (status === ORDER_STATUS.Paid) return "已支付";
  return "已取消";
}
```

## 不可变更新

优先用展开运算符合并新对象，避免直接改写入参。

```typescript
interface User {
  id: string;
  name: string;
}

// 错误：修改原对象
function updateUser(user: User, name: string): User {
  user.name = name;
  return user;
}

// 正确：返回新对象
function updateUser(user: Readonly<User>, name: string): User {
  return { ...user, name };
}
```

## 异步与错误处理

使用 `async/await` 与 `try/catch`，在 `catch` 中将错误视为 `unknown` 再收窄。

```typescript
interface User {
  id: string;
  email: string;
}

declare function riskyOperation(userId: string): Promise<User>;

function getErrorMessage(error: unknown): string {
  if (error instanceof Error) {
    return error.message;
  }
  return "Unexpected error";
}

const logger = {
  error: (message: string, error: unknown) => {
    // 替换为项目内的日志实现（如 pino、winston 等）
  },
};

async function loadUser(userId: string): Promise<User> {
  try {
    return await riskyOperation(userId);
  } catch (error: unknown) {
    logger.error("Operation failed", error);
    throw new Error(getErrorMessage(error));
  }
}
```

## 输入校验

对外部输入（表单、API、URL 参数等）宜用 **Zod**（或项目选用的同类库）做模式校验，并用 `z.infer` 推导类型。

```typescript
import { z } from "zod";

const userSchema = z.object({
  email: z.string().email(),
  age: z.number().int().min(0).max(150),
});

type UserInput = z.infer<typeof userSchema>;

const validated: UserInput = userSchema.parse(input);
```

## 日志与 `console.log`

- 生产路径避免遗留 `console.log`；使用项目统一的日志方案。
- 可在保存后格式化、`tsc` 检查或提交前脚本中对 `console.log` 做提示或拦截（按团队工具链配置）。

## 常见模式

### 统一 API 响应形状（示例）

```typescript
interface ApiResponse<T> {
  success: boolean;
  data?: T;
  error?: string;
  meta?: {
    total: number;
    page: number;
    limit: number;
  };
}
```

### 自定义 Hook（示例）

```typescript
export function useDebounce<T>(value: T, delay: number): T {
  const [debouncedValue, setDebouncedValue] = useState<T>(value);

  useEffect(() => {
    const handler = setTimeout(() => setDebouncedValue(value), delay);
    return () => clearTimeout(handler);
  }, [value, delay]);

  return debouncedValue;
}
```

### 仓储接口（示例）

```typescript
interface Repository<T> {
  findAll(filters?: Filters): Promise<T[]>;
  findById(id: string): Promise<T | null>;
  create(data: CreateDto): Promise<T>;
  update(id: string, data: UpdateDto): Promise<T>;
  delete(id: string): Promise<void>;
}
```

## 密钥与敏感配置

- **禁止**在源码中硬编码密钥、Token、私钥。
- **必须**通过环境变量或构建期注入（如 `process.env.*`、`import.meta.env.*`，以项目脚手架为准），并在缺失时显式失败或降级策略清晰。

```typescript
// 错误：硬编码密钥
const apiKey = "sk-proj-xxxxx";

// 正确：环境变量（Node 示例；Vite 等请用 import.meta.env 及 VITE_ 前缀约定）
const apiKey = process.env.OPENAI_API_KEY;
if (!apiKey) {
  throw new Error("OPENAI_API_KEY not configured");
}
```

涉及认证、支付、上传等场景时，结合项目安全规范做专项评审。

## 与测试规则的关系

关键用户路径的端到端覆盖方式（Playwright、Cypress、Page Object 等）以 `testing.md` 为准；本文件不重复展开 E2E 细则。

## 与 `typescript-reviewer` 子代理

对 **`.ts` / `.tsx` / `.js` / `.jsx`** 进行专项评审（先跑 typecheck/eslint、PR 合并就绪检查、分级结论）时，可委托插件内置的 **`typescript-reviewer`** 子代理；其报告默认写入 `reports/typescript-review-YYYY-MM-DD-HHmmss.md`，规则底线仍以本文件与项目 `AGENTS.md` 为准。
