# Testing Strategy V2

## Principle

测试验证的是 Spec 行为，而不是“让 CI 变绿”。

`REQ → AC → TEST/E2E/VISUAL → Evidence`

## Levels

1. Static/Lint
2. TypeCheck
3. Unit
4. Integration
5. Build
6. E2E
7. Network/Console runtime checks
8. Visual verification

使用成本最低且足够可靠的验证，但关键 AC 必须有合适层级。

## API tests

验证：

- request mapping
- response mapping
- optional/nullable
- error mapping
- duplicate request prevention
- loading/cancel/retry（适用时）

E2E/Browser 中关注真实 method、URL、payload、status 和重复请求。

## UI tests

验证：

- interaction
- loading/success/error/empty/disabled
- responsive/overflow
- keyboard/focus（适用时）
- Design Contract 的关键视觉要求

## Playwright

关键用户流优先使用 Playwright，并将测试 ID 映射 AC。

例：`E2E-003 → AC-005, AC-006`。

## Failure discipline

测试失败时先判断：

1. implementation wrong
2. spec/contract misunderstanding
3. environment problem
4. test wrong

不得为了通过而直接删除断言、放宽断言、skip 测试或修改预期。

## Result vocabulary

只允许：

- PASS：实际执行且通过
- FAIL：实际执行且失败
- NOT_RUN：未执行
- BLOCKED：因环境/依赖无法执行

Mock 通过不得冒充真实集成通过。
