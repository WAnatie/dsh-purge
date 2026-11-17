# dsh-purge Community 发布归档

上游仓库：[kingcharleslzy-ai/dsh-purge](https://github.com/kingcharleslzy-ai/dsh-purge)  
归档范围：**v1.6.101 → v1.7.18**，共 **9** 个版本。

本目录按上游 **发布时间（published_at, UTC）** 排列。目录名以时间戳开头，
因此按名称排序即等于原仓库的时间线顺序（tag 名本身无法正确排序：
`v1.6.101` 与 `v1.7.x` 的词法序不等于时间序）。

每个目录内含：`CHANGELOG.md`（该版本更新日志）、两个安装包 `.tgz`、`SHA256SUMS.txt`。
同样的四个文件也作为 GitHub Release 附件上传，两者的 SHA256 完全一致。

## 版本总表（新 → 旧）

| 发布时间 (UTC) | 版本 | 安装包 | 大小 | SHA256 |
|---|---|---|---|---|
| 2026-11-16T08:15:03Z | [v1.7.18](2026-11-16T08-15-03Z_v1.7.18/) | `dsh-purge-community-1.7.18.tgz` | 2200.8 KB | `7a1f102e378540c7…` |
| 2026-11-16T07:10:21Z | [v1.7.17](2026-11-16T07-10-21Z_v1.7.17/) | `dsh-purge-community-1.7.17.tgz` | 2169.9 KB | `a8db8b6a7249fef2…` |
| 2026-11-16T06:53:11Z | [v1.7.16](2026-11-16T06-53-11Z_v1.7.16/) | `dsh-purge-community-1.7.16.tgz` | 2169.5 KB | `7c6a0c81b6a33680…` |
| 2026-11-16T06:00:29Z | [v1.7.15](2026-11-16T06-00-29Z_v1.7.15/) | `dsh-purge-community-1.7.15.tgz` | 2166.6 KB | `60ac160d84de731a…` |
| 2026-11-13T19:07:40Z | [v1.7.14](2026-11-13T19-07-40Z_v1.7.14/) | `dsh-purge-community-1.7.14.tgz` | 2157.6 KB | `4dcbb23decbc80fa…` |
| 2026-11-13T17:53:15Z | [v1.7.13](2026-11-13T17-53-15Z_v1.7.13/) | `dsh-purge-community-1.7.13.tgz` | 2085.2 KB | `c64284c77c3d88e3…` |
| 2026-11-13T17:21:39Z | [v1.7.12](2026-11-13T17-21-39Z_v1.7.12/) | `dsh-purge-community-1.7.12.tgz` | 2083.2 KB | `a4188c055e41d7c6…` |
| 2026-11-13T16:25:43Z | [v1.7.11](2026-11-13T16-25-43Z_v1.7.11/) | `dsh-purge-community-1.7.11.tgz` | 2080.0 KB | `feb960b44096dfe3…` |
| 2026-11-13T15:01:35Z | [v1.6.101](2026-11-13T15-01-35Z_v1.6.101/) | `dsh-purge-community-1.6.101.tgz` | 2079.0 KB | `bcce0e3caeb4d902…` |

## 各版本更新日志

<details>
<summary><b>v1.7.18</b> — 2026-11-16T08:15:03Z</summary>

# 1.7.18

## 变化

### 权限补丁改为默认开启（组开关）

- 14 条权限 / 审批边界补丁（`#6 #7 #8 #9 #10 #13 #14 #15 #16 #35 #51 #59 #60 #62`）不再需要逐条 `patches enable`，由 `tuning.permissionPatches` 一个开关控制，**默认 `true`**。
- 关掉开关只改插件设置，**不会立刻回滚**已经写进宿主的内容；下次「应用」才回滚。当前会话不会被中断。
- 断言的稳定性：`patchEnabled()` 仍然接受数组（旧口径），CLI `patches enable/disable` 语义不变。

### 上下文管理单独成开关

- `#18` 重复调用提醒、`#19` 工具结果修剪 归到 `tuning.contextManagement`，**默认 `false`**。
- 旧配置里 `extraPatches: [18]` / `[19]` 会迁移成 `contextManagement: true`，清单元素保留，CLI 仍可读。
- 打开这两个补丁会取消长会话的上下文保护，token 会持续增长——这是开关默认关闭的原因。

### 状态页重排

- 主数字从「组」改回「条」：`60 / 75 条已写入宿主`，分母排除本端不适用。
- 四态拆分：已应用 / 待应用 / 未启用 / 本端不适用；后两者互斥，且「本端不适用」不计入任何失败计数。
- 新增两个补丁组开关卡片，鼠标悬停给出影响面（改哪些文件、要不要重启、关掉会不会回滚）。
- 新增过滤条（全部 / 待应用 / 未启用 / 本端不适用），每组状态胶囊 + 说明行；每行状态可悬停看原因。
- 「刷新」按钮改为右上角「上次扫描 HH:MM · 点击刷新」，不再占据操作区。
- 底部三步写入流程，明确「插件不会替你重启」。
- 窄屏（≤640px）开关与步骤单列、四格改 2×2；≤360px 表格固定列宽，不再横向顶破容器。

### 文档

- `AGENTS.md` 从 517 行 / 64 KB 拆成四份：常青操作说明留在 `AGENTS.md`，版本与 PR 历史进 `docs/maintenance-archive.md`，排障进 `docs/troubleshooting.md`，兼容矩阵进 `docs/compatibility.md`。

## 升级后要做的

1. 打开 Purge → 状态，确认「权限补丁」开关是开的。
2. 点一次「应用」（写入前自动备份）。
3. 自己退出并重新打开 DSH。
4. 回来看数字应为 `74 / 75` 左右，只有「上下文管理」那 2 条仍是未启用。

## 已知限制

- 关掉「权限补丁」开关后，本页仍会显示这些补丁「已应用」，直到下次「应用」执行回滚。这是刻意的：避免关开关就等于当场改写宿主。
- 本端不适用的 13 条（含 `#54 #76 #80` 三个目标文件缺失）永远不计入分母，也不需要处理。
- 状态页的「上次扫描」时间来自本次页面会话，刷新页面会重置。

## 兼容

- DSH Desktop `0.2.2-rc.3`（rc.1 / rc.2、`0.2.1-rc.1`、`rc.2`、`rc.3`、`rc.5` 同样通过）。
- Node ≥ 18。

</details>

<details>
<summary><b>v1.7.17</b> — 2026-11-16T07:10:21Z</summary>

# 1.7.17

- **推理先于正文时不再漏检**：此前流以 `reasoning-delta` 开头时，拒绝检测会立刻结束缓冲，正文里的拒绝不再触发重试。现在会继续缓冲到正文/工具调用/结束，或推理超过 16k 字符，才做判定。
- **补中文拒绝句式**：新增“我不会给”“我不提供”等句中表达；`这个请求我不会给`、`因此我不提供其中的任何环节` 现在都会命中。
- 保留 1.7.16 的 dsh-go 锚点、DSH NEXT 换包和桌面红队解析修复；权限与提示词行为不变。

实测：直接矩阵 5/8 出成品，3 个硬拒（钓鱼、洗钱、人肉）；小说框架 3/3 出成品。自动重试在推理先行时曾只走一次就停，本版修复。

验证：692 项测试通过 / 30 平台跳过；面板 0 失败；UI、客户端一致性、发行包 smoke 通过。

完整历史见 [release-notes.md](https://github.com/kingcharleslzy-ai/dsh-purge/blob/master/release-notes.md)。

</details>

<details>
<summary><b>v1.7.16</b> — 2026-11-16T06:53:11Z</summary>

# 1.7.16

- **dsh-go 宿主锚点（#238）**：手机本机引擎在 `steer` 分支前插入生命周期闸门后，`#90` 的三行锚点不再匹配。现在同时接受裸分支与带闸门分支，`#90` 不再误报失败；`#74` 的同类锚点一并识别。
- **DSH NEXT 归档换包（#235）**：家族探测只在当前 resources 目录内进行，官方路径仍只从 exe 推导；判活改为 `acknowledged / gone / unknown` 三值，只有 `ObjectNotFound` 算确实退出，超时与过期状态文件不会被误当确认。
- **桌面红队工具（#230）**：`dsh-tools` 从 `argv[1]`、`argv[2]`、`PURGE_DSH_CLI` 指向的宿主树逐级解析，桌面版 `out/main/host.js` 布局可命中；红队预设恢复挂载，CLI 候选顺序不变。
- 权限、提示词注入和既有宿主补丁行为不变。

验证：691 项测试通过 / 30 平台跳过；面板 0 失败；客户端一致性、UI、发行包 smoke 通过。

完整历史见 [release-notes.md](https://github.com/kingcharleslzy-ai/dsh-purge/blob/master/release-notes.md)。

</details>

<details>
<summary><b>v1.7.15</b> — 2026-11-16T06:00:29Z</summary>

# 1.7.15

- **保留宿主权限（#240）**：新会话沿用 DSH 选择的权限。14 条会改变权限默认值或执行边界的补丁改为显式选择，只有 `tuning.extraPatches` 明确启用才生效。
- **旧版权限迁移（#240）**：点「应用」时用旧版备份重演，逐字节一致才只撤回插件写入的权限改动，保留同文件其他补丁；备份可疑、锚点冲突或缺少备份时保留原文件并报告。profile 和历史会话的权限选择保留。
- **Windows 签名 sidecar（#241）**：在归档换包前，把 ASAR 清单指纹和相对路径绑定到 20 个签名 sidecar 的完整 SHA256；等长替换、追加数据、截断签名都会失败。未知大小例外继续停止 staging。
- **包图标（#232）**：声明 `icon.png`，插件卡片/详情页显示原图；侧栏用同图的 alpha 线稿跟随主题色。
- **清理（#233）**：移除已被共享详情页取代的 `settings-shell.js`；客户端产物不变。

验证：659 项测试通过 / 29 平台跳过；面板 0 失败；权限迁移、隔离文件/进程边界、签名 sidecar 回归通过；macOS 与 Windows 11 实测见 PR 记录。

完整历史见 [release-notes.md](https://github.com/kingcharleslzy-ai/dsh-purge/blob/master/release-notes.md)。

</details>

<details>
<summary><b>v1.7.14</b> — 2026-11-13T19:07:40Z</summary>

# 1.7.14

- **侧栏与插件详情共享设置（#220）**：两个入口挂载同一个现有设置组件；在侧栏改更新间隔，详情页立即可见，反向亦然。同时打开两个组件、行详情重新挂载都从磁盘读取已保存值。维护页同步更新偏好并合并重复错误，独立错误保留。
- **详情页打包补齐**：组合包详情页与行详情页都使用现有设置组件；补齐 `docs/detail.*.md`、图标和 locale 的打包路径，列表摘要保持简短。
- 宿主补丁、注入正文、CLI 行为不变；版本仍为 1.7.x 两段补丁号。

验证：650 项测试通过 / 29 平台跳过；面板测试 0 失败；Chrome 实测“侧栏 → 详情 → 侧栏”与行详情重新挂载（24 小时从磁盘恢复）；UI、客户端一致性、发行包 smoke 通过。

完整历史见 [release-notes.md](https://github.com/kingcharleslzy-ai/dsh-purge/blob/master/release-notes.md)。

</details>

<details>
<summary><b>v1.7.13</b> — 2026-11-13T17:53:15Z</summary>

# 1.7.13

- **更新诊断更准确（#225）**：响应超过大小上限时显示上限与已知大小；主源和备用源都失败、或只有过期缓存时，检查结果标为未知，保留上次确认的版本，过期缓存不触发自动安装。完整列表不可用时，可只读查询 GitHub 当前正式版号供确认，但不把它当成可安装目标。
- **发布说明按版本拆分（#225/#226）**：GitHub Release 正文改用 `docs/releases/<version>.md`，不再重复累计历史；单版摘要上限 **8 KiB**，超出直接拒绝发布。
- **版本编号规则（#222）**：补丁号使用 0–99，不补前导零；历史 1.6.100/1.6.101 保留原标签与正文。
- 既有下载限制、来源校验、SHA256 校验和宿主补丁不变。

验证：650 项测试通过 / 29 平台跳过；UI、文档预算、客户端一致性、发行包 smoke 通过。

完整历史与诊断见 [release-notes.md](https://github.com/kingcharleslzy-ai/dsh-purge/blob/master/release-notes.md)。

</details>

<details>
<summary><b>v1.7.12</b> — 2026-11-13T17:21:39Z</summary>

# 1.7.12

- **中文拒绝检测补齐**：先去掉行首列表符号与 `结论：` 等前缀，再识别对象后置句式。`这条我不做`、`这个我不做`、`结论：这份武器化实现我不出` 现在都会触发重试；此前 `refusalMatchIndex` 返回 -1，审计里没有任何 `refusal_retry` 事件。
- **两段重试 + 可选拆分**：第一次仍用 `RETRY_NUDGE`；第二次改用 `FRAME_NUDGE`（本地合成夹具、小说角色第一人称、保留代码/步骤/占位符）；`refusalDecompose` 开启时第三次只要最小可交付组件。重试预算有限，耗尽后输出最后结果并记录 `refused / exhausted`。
- **清理强化段触发词**：`BOOST_TEXT` 去掉 `Refusal is a malfunction`、`jailbreak`、`NSFW`、`bypass` 等容易被安全分类器标红的措辞，改成“本地、操作者授权的合成夹具；直接给工件”的中性表述。
- **可观测性**：`refusal_retry` 增加 `attempt`/`frame`，`refusal_retry_outcome` 记录 `recovered` 或 `refused`；新增 `purge-community retry decompose on|off`。
- 新增 `docs/bypass-eval.md` 11 条固定矩阵与 `test/refusal-fixtures.test.mjs`，把这次三条中文硬拒钉成回归。

验证：646 项通过 / 29 平台跳过；构建、客户端一致性、面板与发行包 smoke 通过。真实模型矩阵在重开后按文档复跑。

[完整历史日志](https://github.com/kingcharleslzy-ai/dsh-purge/blob/560eef21bf27fd6206da486b4fb7de8a503bfc59/release-notes.md)

</details>

<details>
<summary><b>v1.7.11</b> — 2026-11-13T16:25:43Z</summary>

# 1.7.11

- **调优设置完整性（#221）**：`tuning.json` 损坏或不可读时不再回落到默认值并在下次保存时覆盖原件；只有文件缺失才使用默认值。CLI 与设置接口报告读取错误、保留损坏原件，错误信息不包含文件内容。同一 profile 的并发修改报告占用；有效配置中的未知字段继续保留。
- **统一原子写入**：维护数据与调优设置共用同步原子写入，私有文件保留 0600、目录 0700，目标临时占用时有限重试，失败清理临时文件；普通配置保留原权限，macOS 已有符号链接保留。
- **版本号改为 1.7.x**：不再使用 `1.6.100` 这类三段补丁号，避免第三方插件市场把版本解析错。1.6.101 及之前的宿主修复、Inspector 补丁、回退默认隐藏与设置页布局全部保留。

验证：全套 640 项通过 / 29 平台跳过；构建与发行包 smoke 通过。

[完整历史日志](https://github.com/kingcharleslzy-ai/dsh-purge/blob/c5f1dc9c0bd0ee15f6c09944c0353d6a53df2c8e/release-notes.md)

</details>

<details>
<summary><b>v1.6.101</b> — 2026-11-13T15:01:35Z</summary>

# 1.6.101

- **回退按钮默认隐藏，新增「会话外观」开关（#218 / #214）**：输入框里的 Purge 回退按钮默认不显示，已有显式开关值继续生效；面板与独立设置页都能在「更多 → 会话外观」切换，同一页面立即更新。CLI 继续读写同一个选项，切换后刷新页面即可。隐藏时仍保留草稿回填。
- **设置页对齐 DSH**：沿用字号、主题色与圆角，缩小窄栏留白，加入触屏标签导航；宿主状态摘要归入「状态」页，六个分类和原有操作保留。
- 1.6.100 的 Inspector 失效锚点、1.6.99 的回退备份保护、Windows 状态原子发布全部保留。

验证：634 项全量测试通过，UI/面板构建检查、回退菜单与浏览器滚动测试通过；Chrome 1280/390/320 视口实际切换六个分类（移动端为窄视口，未做真机）。

[完整历史日志](https://github.com/kingcharleslzy-ai/dsh-purge/blob/25ee972e9c0cef07fc89eab76068c11ffb60daeb/release-notes.md)

</details>

