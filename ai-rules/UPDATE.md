# UPDATE — 本目录怎么迭代

## 源仓侧（维护者）

## 2026-11-09.2

- 补完此前只更新哈希的蒸馏：`model`、`guards`、`memory`、`ops-db`、`skills`、`adapters`、`skeleton`。
- 任务分级、SQL 交接、发布阶梯、Skill 工序复用和浏览器默认与当天母版对齐。

## 2026-11-09.1

- `kernel/` 按当天母版重拷。
- `distilled/process.md` 改为现行任务分级：Standard 需求默认一份 `spec.md`，Controlled 默认 `spec.md / delivery.md / history.md`。
- `distilled/ui.md` 写明外部浏览器默认 Eagle Light / ego lite。
- `SOURCES.md` 的 sha256 前 8 位已按当天源文件重算。


分发通道：**PubNote 仓库的 `ai-rules/` 目录**（`pack.py` 出的 zip 只是可选存档）。

两类文件同步成本不同：

### kernel/（verbatim 快照）

源文件变了 → 跑 `sync_pubnote.py` 直接重拷，无需手工改写。

### distilled/（脱敏改写）

1. `SOURCES.md` 记录每个 distilled 文件 ← 源规则路径 + 打包时 sha256。
2. 源规则变更后，用 `shasum -a 256 <源文件>` 与 `SOURCES.md` 比对：hash 变了才需要重蒸馏对应文件；没变就不动。
3. 重蒸馏时只改受影响的 distilled 文件，沿用同一脱敏规则：
   - 机器路径 → 泛化（`~/`、`<RULES_ROOT>`）
   - 个人 infra / launcher / 编排系统名 → 删除或泛化为"宿主编排器"
   - 个人项目名 / 命名空间 → `<project-key>`
   - 能力实测证据、治理登记表、错误档案实例 → 不携带
4. 跑 `sync_pubnote.py` 同步到 PubNote，在 PubNote 仓提交并推送。

### 加新文件

- 零污染源文件 → 加进 `pack.json` 的 `kernel_files`，即走 verbatim 通道（sync 和 zip 都读这份清单）。
- 含项目细节 → 新建 `distilled/<name>.md` 并在 `SOURCES.md` 登记溯源行。
- `pack.json` 的 `forbidden_name_parts` 是兜底：误加个人域目录会 fail-closed。

## 接收方侧

1. 仓库分发：`git pull` 即得最新版。
2. 若你改过本地副本：保留你的改动，用 git 的 diff/merge 逐文件合并。
3. 不建议把本目录内容反向 PR 回源仓——回写流是给维护者的 `SOURCES.md` 通道，改进建议走 issue/口头同步给维护者。

## 原则提醒

- 源仓是唯一权威；本目录是快照投影。两处的冲突以源仓为准。
- 永远不要在 `kernel/` 或 `distilled/` 里写回你的项目私有信息——那会污染下一次分发。
