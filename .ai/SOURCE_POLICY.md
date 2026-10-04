# Source Intake & Conflict Policy

## 1. Three primary sources

每个功能尽可能从三类输入建立事实：

- `PRODUCT`: PRD、需求说明、用户确认
- `API`: 后端接口文档、OpenAPI/Swagger、后端明确约定
- `DESIGN`: Figma、设计稿、Design MCP 输出、交互说明

另外可使用：

- `CODE`: 当前仓库已验证实现
- `RULE`: 项目规范

## 2. Source registry

每个 feature 必须维护 `sources.md`：

```md
| ID | Type | Source | Version/Updated | Status |
|---|---|---|---|---|
| SRC-P-001 | PRODUCT | PRD link/file | v3 | READ |
| SRC-A-001 | API | OpenAPI link/file | 2026-10-01 | READ |
| SRC-D-001 | DESIGN | Figma node ... | v8 | READ |
```

Status 只能是：`READ`, `PARTIAL`, `UNAVAILABLE`, `STALE`。

Agent 不得将 `PARTIAL/UNAVAILABLE` 当成完整事实源。

## 3. Evidence rule

需求、API、Design Contract 中的重要结论应能回溯 Source ID。

例如：

`REQ-003 ← SRC-P-001`

`API-002 ← SRC-A-001`

`DESIGN-004 ← SRC-D-001`

## 4. Conflict classes

### C1 Product ↔ API

例：PRD 要求批量删除，但 API 只有单条删除。

默认：BLOCKING。

### C2 Product ↔ Design

例：PRD 要求生成中可取消，设计没有取消入口。

若影响主流程：BLOCKING；纯文案/轻微视觉差异可 NON_BLOCKING 并按优先级执行。

### C3 API ↔ Design

例：设计展示 avatar，但 API 没有 avatar。

默认：BLOCKING，除非已有明确可用数据源。

### C4 Source ↔ Existing Code

现有代码不是天然真相。先判断是历史兼容、旧实现还是当前合同。

## 5. Assumption policy

NON_BLOCKING assumption 必须：

- 明确写出
- 给出理由
- 可撤销
- 不改变关键业务语义

禁止将 assumption 伪装为需求事实。
