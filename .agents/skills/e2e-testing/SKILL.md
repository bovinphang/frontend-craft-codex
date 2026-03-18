---
name: e2e-testing
description: Playwright 与 Cypress E2E 测试规范，涵盖目录结构、Page Object、CI 集成、视口与设备配置。当用户提到 E2E、端到端测试、Playwright、Cypress、集成测试时自动激活。
version: 1.0.0
---

# E2E 测试规范

适用于使用 Playwright 或 Cypress 进行端到端测试的前端项目。

## 适用场景

- 编写或维护 E2E 测试
- 配置 Playwright / Cypress 项目
- 设计 Page Object 或测试结构
- 将 E2E 集成到 CI 流水线

## 工具选择

| 工具 | 适用 | 特点 |
|------|------|------|
| **Playwright** | 推荐，新项目优先 | 多浏览器、自动等待、并行、Trace、跨平台 |
| **Cypress** | 已有项目或团队熟悉 | 交互式调试、时间旅行、组件测试 |

## 目录结构

### Playwright

```
e2e/                          # 或 tests/e2e/
├── playwright.config.ts       # 配置（浏览器、baseURL、超时）
├── fixtures/                 # 测试夹具（登录态、mock 数据）
│   └── auth.ts
├── pages/                     # Page Object
│   ├── LoginPage.ts
│   ├── DashboardPage.ts
│   └── UserListPage.ts
├── specs/                     # 测试用例
│   ├── auth/
│   │   └── login.spec.ts
│   ├── dashboard/
│   │   └── dashboard.spec.ts
│   └── users/
│       └── user-list.spec.ts
└── utils/                     # 测试工具
    └── test-helpers.ts
```

### Cypress

```
cypress/
├── e2e/                       # 测试用例
│   ├── auth/
│   │   └── login.cy.ts
│   └── dashboard/
│       └── dashboard.cy.ts
├── fixtures/                  # 静态数据
│   └── users.json
├── support/
│   ├── commands.ts            # 自定义命令
│   └── e2e.ts                 # 全局 before/after
└── pages/                     # Page Object（可选）
    └── LoginPage.ts
```

## Page Object 模式

- 每个页面/流程一个 Page 类，封装选择器和操作
- 测试用例只调用 Page 方法，不直接写选择器
- 选择器优先使用 `data-testid`，其次 `role`、`label`，避免依赖实现细节

```typescript
// Playwright 示例
export class LoginPage {
  constructor(private page: Page) {}

  async goto() {
    await this.page.goto('/login');
  }

  async login(email: string, password: string) {
    await this.page.getByTestId('email-input').fill(email);
    await this.page.getByTestId('password-input').fill(password);
    await this.page.getByRole('button', { name: '登录' }).click();
  }

  async expectErrorMessage(text: string) {
    await expect(this.page.getByTestId('error-message')).toContainText(text);
  }
}
```

## 测试编写原则

- 测试用例描述业务场景，而非实现细节
- 一个用例覆盖一个完整用户流程（如：登录 → 进入列表 → 筛选）
- 避免测试间依赖，每个用例可独立运行
- 使用 `beforeEach` 做前置（如登录），避免在用例中重复
- 敏感操作（删除、支付）使用 mock 或测试环境专用接口

## CI 集成

### Playwright

```yaml
# GitHub Actions 示例
- name: Playwright tests
  run: npx playwright test
  env:
    CI: true
- uses: actions/upload-artifact@v4
  if: failure()
  with:
    name: playwright-report
    path: playwright-report/
```

### Cypress

```yaml
- name: Cypress tests
  run: npx cypress run
  env:
    CYPRESS_baseUrl: ${{ secrets.CYPRESS_BASE_URL }}
```

## 视口与设备

- 关键流程至少覆盖：桌面（1920×1080）、平板（768×1024）、移动（375×667）
- 使用 Playwright 的 `projects` 或 Cypress 的 `viewport` 配置多视口
- 响应式回归测试可抽样关键断点，不必全量

## 强约束

- 不要依赖固定等待（`setTimeout`），使用 `waitFor`、`expect` 等断言等待
- 不要在生产环境跑 E2E，使用 staging 或 mock 服务
- 避免在 E2E 中测试纯 UI 细节（如颜色、间距），交给单元测试或视觉回归
- 失败时保留截图、Trace、视频，便于排查
