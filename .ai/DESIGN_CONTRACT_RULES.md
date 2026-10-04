# UI / Design Contract Rules

## 1. Goal

Design/Figma/MCP 是 UI 与交互合同，不应只在生成 Spec 时读取一次。设计要求必须进入实现和最终视觉验证。

## 2. Design analysis

对相关页面/组件确认：

- DESIGN ID
- source / Figma node / MCP reference
- page/component name
- layout hierarchy
- spacing / sizing（设计明确时）
- typography
- color/token
- assets/icons
- responsive behavior
- interaction
- state variants
- content/text

重点状态：

- default
- hover/focus/active（适用时）
- disabled
- loading
- empty
- success
- error
- permission/locked（适用时）

## 3. Do not over-infer

设计稿没有展示某状态，不等于该状态不存在。

如果 PRD/API 明确存在 error/loading/empty，但设计缺失：

- 先查项目 Design System / 已有模式
- 若存在稳定项目模式，可作为 NON_BLOCKING assumption 并记录来源
- 若属于关键流程且无法安全推导，进入 clarification

## 4. Design vs implementation

优先复用项目已有：

- Design tokens
- Shared components
- Layout primitives
- Icon system
- Typography system

不得仅为了像素匹配复制已有组件能力。

## 5. Visual verification

UI 任务完成后必须检查：

- 页面整体布局
- alignment / spacing
- typography
- color
- assets
- responsive
- overflow
- state variants

推荐：Playwright 打开页面 → 到达指定状态 → screenshot → 与设计进行人工/工具辅助比较。

无法获得设计或无法截图时，Visual 状态必须为 `NOT_RUN` / `UNAVAILABLE`，不得标记 PASS。

## 6. Traceability

必须支持：

`SRC-D-* → DESIGN-* → REQ-* → TASK-* → AC-* → VISUAL/TEST-*`
