# Project Rules

> 必须按真实项目修改本文件。不要保留不适用的示例规则。

## Stack

- Framework: [Vue 3 / React / ...]
- Language: TypeScript
- Build: [Vite / Next.js / ...]
- State: [Pinia / Zustand / Redux / ...]
- HTTP: [Axios / fetch wrapper / ...]
- Unit: [Vitest / Jest / ...]
- E2E: Playwright

## Commands

```bash
# install
[command]

# dev
[command]

# lint
[command]

# typecheck
[command]

# unit test
[command]

# build
[command]

# e2e
[command]
```

未配置的命令不得由 Agent 随意猜测；先检查 package.json / workspace 配置。

## Architecture

- API requests location: `[src/api]`
- Shared components: `[src/components]`
- Feature modules: `[src/features]`
- Stores: `[src/stores]`
- Types: `[src/types]`
- Tests: `[tests / colocated]`

## TypeScript

- 新代码禁止无理由引入 `any`。
- 禁止用 `@ts-ignore` / `@ts-expect-error` 掩盖普通类型问题。
- API types 必须与 API Contract 对齐。
- 优先使用 domain type，而不是重复匿名结构。

## API

- 组件不得绕过项目 API client 直接调用底层 HTTP 库（除非现有架构如此规定）。
- auth、baseURL、错误转换、重试策略沿用项目基础设施。
- 禁止在 UI 层自行解释未定义后端错误码。

## UI

- 优先复用 Design System / shared component。
- 优先使用 design tokens。
- 禁止为了单一需求引入新的 UI/CSS 框架。
- Feature 样式不得无必要污染全局。

## State

- 本地 UI state 保持局部。
- 跨组件/跨页面业务状态按现有 store 模式处理。
- 禁止为了方便将临时状态全局化。

## Scope

- 不做无关重构。
- 不升级依赖，除非需求明确需要并获批准。
- 不修改 lockfile，除非依赖确实发生变化。
