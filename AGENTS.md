# Repository Instructions for Coding Agents

本文件是本仓库 Coding Agent 的最高级仓库入口规则。所有功能开发、修改和修复都必须遵守本文件以及 `.ai/` 中引用的规则。

## 1. Mandatory reading

开始功能开发前，必须读取：

- `.ai/WORKFLOW.md`
- `.ai/PROJECT_RULES.md`
- `.ai/SOURCE_POLICY.md`

按阶段继续读取：

- 后端接口：`.ai/API_CONTRACT_RULES.md`
- UI/设计：`.ai/DESIGN_CONTRACT_RULES.md`
- 追踪关系：`.ai/TRACEABILITY.md`
- 测试：`.ai/TEST_STRATEGY.md`
- 完成前 Review：`.ai/REVIEW_CHECKLIST.md`

## 2. Source of truth priority

发生冲突时默认优先级：

1. 用户最新明确确认的指令
2. 已确认的 `spec.md` / clarification decision
3. 已确认的 Backend API Contract
4. 已确认的 Design Contract
5. `.ai/PROJECT_RULES.md`
6. 当前代码中已验证的行为
7. 原始 PRD
8. Agent assumption

注意：优先级不意味着 Agent 可以静默覆盖冲突。涉及业务行为、API、数据、关键 UI/交互的冲突必须记录到 `clarification.md`；属于 BLOCKING 时必须停止。

## 3. Mandatory gates

开发必须经过：

`Source Intake → Requirement Analysis → API Analysis → Design Analysis → Clarification → Human Confirm(if blocking) → SPEC → Task Graph → Coding Loop → Integration → Build → E2E → Visual Verification → Diff Review → Spec Compliance → Final Report`

不得跳过适用的 Gate。

## 4. Never fabricate

Agent 不得虚构：

- 未读取到的 PRD 内容
- API endpoint / method / field / enum / status / error semantics
- 设计稿中的尺寸、状态、交互
- 测试执行结果
- 浏览器、Network、Console、截图验证结果

信息缺失时必须显式标记 `UNKNOWN` / `NOT_AVAILABLE` / `NOT_RUN`。

## 5. Blocking rule

出现以下任一情况通常视为 BLOCKING：

- 核心业务行为存在两种以上合理解释
- 前端实现依赖 API 文档中不存在的字段或能力
- PRD 与 API Contract 对核心流程冲突
- PRD 与 Design 对核心交互冲突
- API 与 Design 所需数据不匹配
- 关键页面/状态设计缺失，且无法从已确认规则推导
- 会导致数据丢失、安全、权限、付费、提交等风险的不确定性

BLOCKING 未解决前不得开始相关实现。

## 6. Scope discipline

只修改当前任务需要的文件。禁止无关重构、依赖升级、大范围格式化或架构迁移。必须扩大范围时先说明原因、文件、风险并等待需要的确认。

## 7. Completion

只有当适用验证均通过且强制 AC 无 `FAIL` / `NOT_TESTED` 时，才能输出 `READY`。

`READY` 仅表示“准备好提交”，不等于授权执行 git commit/push。
