# Coding Agent Frontend Rules V2

一套面向前端 Coding Agent 的仓库级开发协议。

核心输入不是单一 PRD，而是三源事实：

1. Product / PRD
2. Backend API Contract
3. UI / Design Contract（可来自 Figma / MCP）

核心链路：

`SOURCE → REQ → API / DESIGN → TASK → AC → TEST → REVIEW`

## 推荐目录

```text
project/
├── AGENTS.md
├── .ai/
│   ├── WORKFLOW.md
│   ├── PROJECT_RULES.md
│   ├── SOURCE_POLICY.md
│   ├── API_CONTRACT_RULES.md
│   ├── DESIGN_CONTRACT_RULES.md
│   ├── TRACEABILITY.md
│   ├── TEST_STRATEGY.md
│   ├── REVIEW_CHECKLIST.md
│   └── templates/
│       ├── REQUIREMENT_TEMPLATE.md
│       ├── CLARIFICATION_TEMPLATE.md
│       ├── SPEC_TEMPLATE.md
│       ├── API_CONTRACT_TEMPLATE.md
│       ├── DESIGN_CONTRACT_TEMPLATE.md
│       ├── TASK_TEMPLATE.md
│       └── FINAL_REPORT_TEMPLATE.md
└── docs/requirements/<feature>/
    ├── sources.md
    ├── requirement.md
    ├── clarification.md
    ├── api-contract.md
    ├── design-contract.md
    ├── spec.md
    ├── tasks.md
    └── review.md
```

## 使用方式

1. 将整个目录复制到项目根目录。
2. 按真实项目修改 `.ai/PROJECT_RULES.md` 中技术栈、目录、命令和约束。
3. 每个需求创建 `docs/requirements/<feature>/`。
4. 在 `sources.md` 中登记 PRD、API 文档、设计稿/MCP 节点及版本。
5. 给 Agent 的入口指令只需类似：

> 实现 `docs/requirements/<feature>` 中的需求，严格遵循 `AGENTS.md`。先完成三源分析和 Clarification；存在 BLOCKING 问题时停止并等待确认。

## 关键原则

- 未读取到的文档不得假装已读取。
- API 未定义的字段、状态码、错误语义不得猜测。
- Design 未定义的关键交互不得自行发明。
- PRD / API / Design 冲突必须记录并按规则处理。
- BLOCKING 未解决前不得进入实现。
- 测试未实际运行不得标记 PASS。
- UI 变更必须进行视觉验证；无法验证时标记 NOT_RUN，而不是 PASS。
- Agent 不得自动 commit/push，除非用户明确要求。
