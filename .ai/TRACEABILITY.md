# Requirement Traceability Rules

## 1. Purpose

保证 Agent 能回答：为什么改这段代码、来自哪个需求、依赖哪个 API/设计、由什么测试证明正确。

## 2. IDs

统一使用：

- `SRC-P-001` Product source
- `SRC-A-001` API source
- `SRC-D-001` Design source
- `REQ-001` Requirement
- `API-001` API contract
- `DESIGN-001` Design contract
- `EDGE-001` Edge case
- `AC-001` Acceptance criterion
- `TASK-001` Implementation task
- `TEST-001` Unit/integration test
- `E2E-001` E2E test
- `VISUAL-001` Visual verification

ID 一旦在 feature 中使用，不要重排复用。

## 3. Required mapping

至少维护：

```text
SOURCE
  ↓
REQ
 ├─ API
 ├─ DESIGN
 └─ EDGE
  ↓
AC
  ↓
TASK
  ↓
TEST / E2E / VISUAL
```

## 4. Coverage rules

- 每个强制 REQ 至少有一个 AC。
- 每个 AC 至少有一个验证方法。
- 每个 API/DESIGN requirement 应能关联相关 REQ/TASK。
- 删除/修改 REQ 时必须检查受影响 API、DESIGN、TASK、TEST。

## 5. Traceability table

Spec/Review 中维护：

| REQ | Source | API | Design | AC | Task | Verification |
|---|---|---|---|---|---|---|
| REQ-001 | SRC-P-001 | API-001 | DESIGN-001 | AC-001 | TASK-002 | E2E-001 |

## 6. Change impact

需求变化时先做 Impact Analysis：

1. 找到变更 REQ
2. 找到关联 API / DESIGN
3. 找到关联 TASK / files
4. 找到关联 TEST / E2E / VISUAL
5. 只重新实现/验证受影响范围，并执行必要回归
