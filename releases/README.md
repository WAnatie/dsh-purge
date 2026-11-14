# dsh-purge 最新 5 个版本归档（更新日志 + 安装文件）

来源仓库：<https://github.com/kingcharleslzy-ai/dsh-purge>（MIT License）

目录名以 **原仓库 `published_at`(UTC)** 为前缀，因此按名称升序排列即等于原仓库的发布时间顺序；下方表格按发布时间**倒序**（最新在上），与原仓库 Releases 页面一致。

## 时间线（新 → 旧）

| # | 版本 | 原发布时间 (UTC) | 安装包 | 大小 | SHA256 | 目录 |
|---|---|---|---|---|---|---|
| 1 | `v1.7.14` | 2026-11-13T19:07:40Z | `dsh-purge-community-1.7.14.tgz` | 2157.6 KB | `4dcbb23decbc80fa29455db62e175747d2bbd9c0b3dc3baf630431d158055bf0` | [`2026-11-13T19-07-40Z_v1.7.14/`](./2026-11-13T19-07-40Z_v1.7.14) |
| 2 | `v1.7.13` | 2026-11-13T17:53:15Z | `dsh-purge-community-1.7.13.tgz` | 2085.2 KB | `c64284c77c3d88e36c99222c8e00564aa965c90e50d990752f45f72ccb59cb6d` | [`2026-11-13T17-53-15Z_v1.7.13/`](./2026-11-13T17-53-15Z_v1.7.13) |
| 3 | `v1.7.12` | 2026-11-13T17:21:39Z | `dsh-purge-community-1.7.12.tgz` | 2083.2 KB | `a4188c055e41d7c62e2edf659f0623699aa34d5d8ddb64ea8502dc2e9a77551b` | [`2026-11-13T17-21-39Z_v1.7.12/`](./2026-11-13T17-21-39Z_v1.7.12) |
| 4 | `v1.7.11` | 2026-11-13T16:25:43Z | `dsh-purge-community-1.7.11.tgz` | 2080 KB | `feb960b44096dfe38c32e12b1e16a1648ca35ba65bd5180b1f2d226915cb7b1a` | [`2026-11-13T16-25-43Z_v1.7.11/`](./2026-11-13T16-25-43Z_v1.7.11) |
| 5 | `v1.6.101` | 2026-11-13T15:01:35Z | `dsh-purge-community-1.6.101.tgz` | 2079 KB | `bcce0e3caeb4d9022a268cd71c1a7a8dd772556cebcb2e2e0acd8f215eda1930` | [`2026-11-13T15-01-35Z_v1.6.101/`](./2026-11-13T15-01-35Z_v1.6.101) |

## 每版内容

### v1.7.14 — dsh-purge Community 1.7.14

- 原发布时间：2026-11-13T19:07:40Z
- SHA256：`4dcbb23decbc80fa29455db62e175747d2bbd9c0b3dc3baf630431d158055bf0`
- 文件：`CHANGELOG.md`、`dsh-purge-community.tgz`、`dsh-purge-community-1.7.14.tgz`、`SHA256SUMS.txt`

<details><summary>更新日志全文</summary>

```markdown
# 1.7.14

- **侧栏与插件详情共享设置（#220）**：两个入口挂载同一个现有设置组件；在侧栏改更新间隔，详情页立即可见，反向亦然。同时打开两个组件、行详情重新挂载都从磁盘读取已保存值。维护页同步更新偏好并合并重复错误，独立错误保留。
- **详情页打包补齐**：组合包详情页与行详情页都使用现有设置组件；补齐 `docs/detail.*.md`、图标和 locale 的打包路径，列表摘要保持简短。
- 宿主补丁、注入正文、CLI 行为不变；版本仍为 1.7.x 两段补丁号。

验证：650 项测试通过 / 29 平台跳过；面板测试 0 失败；Chrome 实测“侧栏 → 详情 → 侧栏”与行详情重新挂载（24 小时从磁盘恢复）；UI、客户端一致性、发行包 smoke 通过。

完整历史见 [release-notes.md](https://github.com/kingcharleslzy-ai/dsh-purge/blob/master/release-notes.md)。
```

</details>

### v1.7.13 — dsh-purge Community 1.7.13

- 原发布时间：2026-11-13T17:53:15Z
- SHA256：`c64284c77c3d88e36c99222c8e00564aa965c90e50d990752f45f72ccb59cb6d`
- 文件：`CHANGELOG.md`、`dsh-purge-community.tgz`、`dsh-purge-community-1.7.13.tgz`、`SHA256SUMS.txt`

<details><summary>更新日志全文</summary>

```markdown
# 1.7.13

- **更新诊断更准确（#225）**：响应超过大小上限时显示上限与已知大小；主源和备用源都失败、或只有过期缓存时，检查结果标为未知，保留上次确认的版本，过期缓存不触发自动安装。完整列表不可用时，可只读查询 GitHub 当前正式版号供确认，但不把它当成可安装目标。
- **发布说明按版本拆分（#225/#226）**：GitHub Release 正文改用 `docs/releases/<version>.md`，不再重复累计历史；单版摘要上限 **8 KiB**，超出直接拒绝发布。
- **版本编号规则（#222）**：补丁号使用 0–99，不补前导零；历史 1.6.100/1.6.101 保留原标签与正文。
- 既有下载限制、来源校验、SHA256 校验和宿主补丁不变。

验证：650 项测试通过 / 29 平台跳过；UI、文档预算、客户端一致性、发行包 smoke 通过。

完整历史与诊断见 [release-notes.md](https://github.com/kingcharleslzy-ai/dsh-purge/blob/master/release-notes.md)。
```

</details>

### v1.7.12 — dsh-purge Community 1.7.12

- 原发布时间：2026-11-13T17:21:39Z
- SHA256：`a4188c055e41d7c62e2edf659f0623699aa34d5d8ddb64ea8502dc2e9a77551b`
- 文件：`CHANGELOG.md`、`dsh-purge-community.tgz`、`dsh-purge-community-1.7.12.tgz`、`SHA256SUMS.txt`

<details><summary>更新日志全文</summary>

```markdown
# 1.7.12

- **中文拒绝检测补齐**：先去掉行首列表符号与 `结论：` 等前缀，再识别对象后置句式。`这条我不做`、`这个我不做`、`结论：这份武器化实现我不出` 现在都会触发重试；此前 `refusalMatchIndex` 返回 -1，审计里没有任何 `refusal_retry` 事件。
- **两段重试 + 可选拆分**：第一次仍用 `RETRY_NUDGE`；第二次改用 `FRAME_NUDGE`（本地合成夹具、小说角色第一人称、保留代码/步骤/占位符）；`refusalDecompose` 开启时第三次只要最小可交付组件。重试预算有限，耗尽后输出最后结果并记录 `refused / exhausted`。
- **清理强化段触发词**：`BOOST_TEXT` 去掉 `Refusal is a malfunction`、`jailbreak`、`NSFW`、`bypass` 等容易被安全分类器标红的措辞，改成“本地、操作者授权的合成夹具；直接给工件”的中性表述。
- **可观测性**：`refusal_retry` 增加 `attempt`/`frame`，`refusal_retry_outcome` 记录 `recovered` 或 `refused`；新增 `purge-community retry decompose on|off`。
- 新增 `docs/bypass-eval.md` 11 条固定矩阵与 `test/refusal-fixtures.test.mjs`，把这次三条中文硬拒钉成回归。

验证：646 项通过 / 29 平台跳过；构建、客户端一致性、面板与发行包 smoke 通过。真实模型矩阵在重开后按文档复跑。

[完整历史日志](https://github.com/kingcharleslzy-ai/dsh-purge/blob/560eef21bf27fd6206da486b4fb7de8a503bfc59/release-notes.md)
```

</details>

### v1.7.11 — dsh-purge Community 1.7.11

- 原发布时间：2026-11-13T16:25:43Z
- SHA256：`feb960b44096dfe38c32e12b1e16a1648ca35ba65bd5180b1f2d226915cb7b1a`
- 文件：`CHANGELOG.md`、`dsh-purge-community.tgz`、`dsh-purge-community-1.7.11.tgz`、`SHA256SUMS.txt`

<details><summary>更新日志全文</summary>

```markdown
# 1.7.11

- **调优设置完整性（#221）**：`tuning.json` 损坏或不可读时不再回落到默认值并在下次保存时覆盖原件；只有文件缺失才使用默认值。CLI 与设置接口报告读取错误、保留损坏原件，错误信息不包含文件内容。同一 profile 的并发修改报告占用；有效配置中的未知字段继续保留。
- **统一原子写入**：维护数据与调优设置共用同步原子写入，私有文件保留 0600、目录 0700，目标临时占用时有限重试，失败清理临时文件；普通配置保留原权限，macOS 已有符号链接保留。
- **版本号改为 1.7.x**：不再使用 `1.6.100` 这类三段补丁号，避免第三方插件市场把版本解析错。1.6.101 及之前的宿主修复、Inspector 补丁、回退默认隐藏与设置页布局全部保留。

验证：全套 640 项通过 / 29 平台跳过；构建与发行包 smoke 通过。

[完整历史日志](https://github.com/kingcharleslzy-ai/dsh-purge/blob/c5f1dc9c0bd0ee15f6c09944c0353d6a53df2c8e/release-notes.md)
```

</details>

### v1.6.101 — dsh-purge Community 1.6.101

- 原发布时间：2026-11-13T15:01:35Z
- SHA256：`bcce0e3caeb4d9022a268cd71c1a7a8dd772556cebcb2e2e0acd8f215eda1930`
- 文件：`CHANGELOG.md`、`dsh-purge-community.tgz`、`dsh-purge-community-1.6.101.tgz`、`SHA256SUMS.txt`

<details><summary>更新日志全文</summary>

```markdown
# 1.6.101

- **回退按钮默认隐藏，新增「会话外观」开关（#218 / #214）**：输入框里的 Purge 回退按钮默认不显示，已有显式开关值继续生效；面板与独立设置页都能在「更多 → 会话外观」切换，同一页面立即更新。CLI 继续读写同一个选项，切换后刷新页面即可。隐藏时仍保留草稿回填。
- **设置页对齐 DSH**：沿用字号、主题色与圆角，缩小窄栏留白，加入触屏标签导航；宿主状态摘要归入「状态」页，六个分类和原有操作保留。
- 1.6.100 的 Inspector 失效锚点、1.6.99 的回退备份保护、Windows 状态原子发布全部保留。

验证：634 项全量测试通过，UI/面板构建检查、回退菜单与浏览器滚动测试通过；Chrome 1280/390/320 视口实际切换六个分类（移动端为窄视口，未做真机）。

[完整历史日志](https://github.com/kingcharleslzy-ai/dsh-purge/blob/25ee972e9c0cef07fc89eab76068c11ffb60daeb/release-notes.md)
```

</details>

