# Coding Agent Development Workflow V2

## 0. State machine

```text
SOURCE_INTAKE
→ ANALYZED
→ CLARIFIED
→ SPEC_CONFIRMED
→ PLANNED
→ IMPLEMENTING
→ INTEGRATED
→ VERIFIED
→ REVIEWED
→ READY
```

存在 BLOCKING 时进入 `BLOCKED`，直到获得确认。

## 1. Source Intake

创建/更新 `sources.md`，登记 PRODUCT / API / DESIGN 来源、版本、可访问状态。

读取 `.ai/SOURCE_POLICY.md`。

若用户明确提供了接口文档或设计稿/MCP，必须实际读取相关内容后才能声称已分析。

## 2. Requirement Analysis

基于 PRODUCT + CODE + RULE 生成 `requirement.md`：

- goal
- user flow
- functional requirements
- non-functional requirements
- constraints
- edge cases
- unknowns

此阶段不得写功能代码。

## 3. API Analysis

若功能涉及后端：读取 `.ai/API_CONTRACT_RULES.md`，生成 `api-contract.md`。

如果没有后端依赖，明确写 `N/A`，不要虚构 API。

## 4. Design Analysis

若功能涉及 UI：读取 `.ai/DESIGN_CONTRACT_RULES.md`，生成 `design-contract.md`。

如果没有 UI 变化，明确写 `N/A`。

## 5. Cross-source Clarification

对 PRODUCT / API / DESIGN / CODE 做交叉检查，生成 `clarification.md`。

检查：

- ambiguity
- conflict
- missing requirement
- API capability gap
- API field gap
- missing design state
- data/UI mismatch
- assumptions

每项标记 `BLOCKING` 或 `NON_BLOCKING`。

存在 BLOCKING：停止，向人确认。

## 6. SPEC

Clarification 通过后，按模板生成 `spec.md`。

Spec 必须包含 REQ、API、DESIGN、EDGE、AC 和 Traceability。

Spec 是后续实现的主要 source of truth。

## 7. Task Graph

按模板生成 `tasks.md`。

Task 应小而可验证，并标记依赖、文件、REQ、AC、verification。

## 8. Context Builder

执行某 Task 前只收集必要上下文：

`Spec + Task + relevant API/Design + relevant source files + relevant tests`

先观察现有模式，再新增抽象。

## 9. Coding Loop

每次处理一个逻辑 Task：

`Pick → Inspect → Implement → Lint → TypeCheck → Unit/Integration → Task Verify`

失败则 `Analyze → Fix → Verify Again`。

验证未通过不得标记 DONE。

## 10. Integration

全部 Task 完成后检查组件、store、router、API、loading/error/empty 等跨模块行为。

## 11. Build

运行真实项目 build。失败则不能 READY。

## 12. E2E

根据关键 AC 执行 E2E。浏览器验证同时关注 Console 和 Network。

禁止仅因页面可打开就认为 E2E 通过。

## 13. Visual Verification

UI 变化必须依据 Design Contract 验证关键页面与状态。无法执行则记录原因和 `NOT_RUN`。

## 14. Diff Review

执行/检查：

```bash
git diff --stat
git diff
```

按 `.ai/REVIEW_CHECKLIST.md` 评审。

## 15. Spec Compliance

逐条检查 AC：`PASS / FAIL / NOT_TESTED`，并提供 evidence。

强制 AC 有 FAIL / NOT_TESTED → `NOT READY`。

## 16. Final Report

按模板输出：

- implemented
- files changed
- verification actually executed
- AC status
- traceability summary
- known issues
- not-run checks
- final decision

不得把未执行的命令写成 PASS。
