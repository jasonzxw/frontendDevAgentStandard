# Final Review Checklist V2

## 1. Scope

- 修改是否都服务于 Spec？
- 是否存在无关重构/格式化/依赖变化？
- 是否有意外生成文件？

## 2. Product compliance

- 每个 mandatory REQ 是否实现？
- 用户流是否完整？
- Edge cases 是否处理？

## 3. API compliance

- endpoint/method/payload 是否匹配 API Contract？
- required/nullable/enum 是否正确？
- 是否读取了不存在字段？
- 是否出现重复请求/竞态？
- error handling 是否符合已知 contract？

## 4. Design compliance

- component/layout/state 是否匹配 Design Contract？
- loading/error/empty/disabled 是否覆盖？
- 是否复用项目 token/component？
- responsive/overflow 是否验证？

## 5. Correctness

检查 async、race、stale state、null/undefined、cleanup、重复提交、错误状态恢复。

## 6. Type safety

检查 `any`、unsafe assertion、ignore directive、API type mismatch。

## 7. Performance

检查重复 render/request、昂贵计算、effect/watch cleanup、大依赖。

## 8. Security

检查 XSS、unsafe HTML/URL、敏感信息日志、权限假设。

## 9. Debug residue

检查 console.log、debugger、TODO、临时 mock、注释掉的旧代码。

## 10. Test integrity

- 是否削弱/删除测试以通过？
- AC 是否有验证证据？
- 未执行测试是否被错误标 PASS？

## 11. Traceability

检查 `REQ → API/DESIGN → AC → TASK → TEST` 是否覆盖完整。

## 12. Decision

输出：

- Critical Issues
- Warnings
- Suggestions
- AC Matrix
- NOT_RUN/BLOCKED checks
- `READY` 或 `NOT READY`
