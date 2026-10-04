# Backend API Contract Rules

## 1. Goal

后端接口不是“参考资料”，而是前端实现的数据与行为合同。Agent 必须先建立 API Contract，再实现依赖接口的功能。

## 2. API analysis

对每个相关接口确认：

- API ID
- source ID / version
- endpoint
- HTTP method
- auth / permission
- request params/body
- field type / required / nullable
- response schema
- enum values
- pagination
- error codes / error body
- loading / timeout / cancellation expectations（若有定义）
- idempotency / duplicate submission（若有定义）

未知项写 `UNKNOWN`，不得猜测。

## 3. Frontend constraints

- API 调用必须遵循 `.ai/PROJECT_RULES.md` 的 API 层约束。
- 不得在组件中创造 API 未声明字段。
- 不得为了匹配 UI 修改后端语义。
- API 类型应从可信 schema 生成或显式定义。
- nullable / optional 必须真实反映 contract。
- 不得使用 `any` 掩盖 contract 不确定性。

## 4. Contract mismatch

以下情况进入 clarification：

- Design 需要字段但 API 不提供
- PRD 需要操作但 API 无能力
- API enum 与 PRD 状态不一致
- request required field 无来源
- response 字段语义不明确
- 同一接口文档与现有实现明显冲突

核心流程 mismatch 默认 BLOCKING。

## 5. Verification

接口相关 AC 应通过适当方式验证：

- unit：request/response mapping
- integration：API client + store/component
- E2E：关键真实用户流
- browser network：method、URL、payload、重复请求、错误状态

Mock 通过不能证明真实 API Contract 已通过集成验证。

## 6. Traceability

必须支持：

`SRC-A-* → API-* → REQ-* → TASK-* → AC-* → TEST-*`
