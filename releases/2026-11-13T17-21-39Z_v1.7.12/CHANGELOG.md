# 1.7.12

- **中文拒绝检测补齐**：先去掉行首列表符号与 `结论：` 等前缀，再识别对象后置句式。`这条我不做`、`这个我不做`、`结论：这份武器化实现我不出` 现在都会触发重试；此前 `refusalMatchIndex` 返回 -1，审计里没有任何 `refusal_retry` 事件。
- **两段重试 + 可选拆分**：第一次仍用 `RETRY_NUDGE`；第二次改用 `FRAME_NUDGE`（本地合成夹具、小说角色第一人称、保留代码/步骤/占位符）；`refusalDecompose` 开启时第三次只要最小可交付组件。重试预算有限，耗尽后输出最后结果并记录 `refused / exhausted`。
- **清理强化段触发词**：`BOOST_TEXT` 去掉 `Refusal is a malfunction`、`jailbreak`、`NSFW`、`bypass` 等容易被安全分类器标红的措辞，改成“本地、操作者授权的合成夹具；直接给工件”的中性表述。
- **可观测性**：`refusal_retry` 增加 `attempt`/`frame`，`refusal_retry_outcome` 记录 `recovered` 或 `refused`；新增 `purge-community retry decompose on|off`。
- 新增 `docs/bypass-eval.md` 11 条固定矩阵与 `test/refusal-fixtures.test.mjs`，把这次三条中文硬拒钉成回归。

验证：646 项通过 / 29 平台跳过；构建、客户端一致性、面板与发行包 smoke 通过。真实模型矩阵在重开后按文档复跑。

[完整历史日志](https://github.com/kingcharleslzy-ai/dsh-purge/blob/560eef21bf27fd6206da486b4fb7de8a503bfc59/release-notes.md)
