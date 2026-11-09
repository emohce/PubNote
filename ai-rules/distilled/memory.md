# 记忆层：路由、写入门槛、错误档案

> 蒸馏自：memory 域 owner（记忆路由矩阵、写入门槛、错误档案、自适应文档索引、实现同步、提醒）与设计偏好索引 owner。实例（具体档案记录、私人路由表）不携带。

## 1. 核心原则

- 记忆/档案/回执是**有界缓存和证据**，不是 canonical truth。权威永远在当前规则/需求/代码 owner。
- **最近 owner 优先**：事实写到作用域最窄的 owner——任务事实留任务文档，项目事实留项目知识，只有跨项目可复用且通过隐私/冲突/去重检查才升全局。
- 命中记忆 ≠ 指令：过期、矛盾、过宽的记忆按"待验证证据"处理；对答案有实质影响时报告用了哪些记忆。
- 可以有派生索引避免每次打开全部档案。档案文件仍是唯一事实；索引损坏或不可用时照常查原文，不因此停工。索引不存 prompt、命令、输出、绝对路径或凭据，也不能改变授权。
- 浏览器路线另有唯一 owner：外部网站交互默认 Eagle Light / ego lite；已打开的本机预览才用宿主自带浏览器。

## 2. 写入门槛（六条全满足才落盘）

1. 超出当前回复的可复用价值；
2. 有证据或用户明确确认；
3. 作用域稳定且有具名权威；
4. 内容隐私安全、已规范化；
5. 不与更高位的 canonical/ADR/规则 owner 冲突；
6. 写完回读。

不入门：一次性措辞、推测、原始 prompt/转录、命令、输出、路径、身份、密钥、易变观测。未确认的演化候选留在对话里（演化候选门见 process §演化），设计类候选走偏好索引。

## 3. 错误档案

- **触发**：只有"已验证的可复用失败 + 新的/修正的预防指导"才建档；常规修复、一次性纠正不建档、不刷索引、不打印空收尾。
- **记录结构**：机读元数据 `id/status/scope/fingerprint/first_seen/last_verified/review_after/evidence/tags` + 六节（症状、失败路径、已验证根因、替代路径、正确检测顺序、预防规则）。模板在 `kernel/memory/templates/error-memory-template.md`。
- **同一根因一个 `failure_key`**：重复发生更新同一条的 Occurrence History，不新建 fingerprint。
- **召回纪律**：只有 `status: verified` 且带已验证替代路径的记录可影响后续路由；candidate/superseded/retired/过期评审材料不静默变成当前路由。回忆失败路线前先查档案。
- **分层**：任务证据 → 项目错误档案 → 全局档案；全局不吸收产品细节，外部项目只存链接。

## 4. 自适应文档索引（adaptive document index）

根索引/路由枢纽扫描成本过高时加**纯链接中间层**，永远不制造第二个事实 owner。触发阈值（任一）：

- 根索引直接链接 ≥30 个叶子；
- 索引/过程枢纽 >150 行；
- 场景路由文档 ≥12 个平级场景或 >300 行；
- 一个稳定业务域 ≥6 条记录；
- 用户点名高频模块。

采用后：每条错误记录恰好一个 Primary owner（最多再在 2 个模块的 Related 出现）；模块只含 Scope/Authorities/Primary/Related/Historical；模块 >30 Primary 或 >150 行再拆一层，路径上中间层 ≤2；自动适应只能加链接和标题，不能移动/删除/改写叶子、不能扩大写集。

## 5. 实现同步（latest-implementation sync）

行为/架构/配置/数据契约变化后，只更新事实变了的现有 owner。好的同步记：用户可见的当前行为、决定性入口与权属边界、兼容/回退路径、验证证据与残留、必要的需求/ADR 回链。**当前文档不变成执行日志**；源与文档不一致 → 报 `doc_drift`。模板 `kernel/memory/templates/implementation-sync-template.md`。

## 6. 提醒（reminders）

只在"能防止一次很可能发生的遗漏"时写；作用域收窄、非阻塞。模板 `kernel/memory/templates/reminder-template.md`。

## 7. 宿主自动记忆（auto-memory）

宿主自带的记忆目录（如 `~/<host>/memory/`）：`MEMORY.md` 只存索引行，指针指向各域文件，不复制事实体；写入同样过第 2 节门槛。

## 8. 设计偏好索引（design-preference）

- 索引（`index.json` / 项目偏好 JSON）只存**路由**：`id/category/scope/surfaces/authority_ref/tags/status/priority/last_verified`，偏好本体在各自 authority_ref。
- 权威顺序：canonical 需求/ADR > 项目设计系统/偏好 > 普通全局品味；同级真冲突要裁决，通用风格 Skill 不能裁决。
- 门控：项目有 `design-preference-gate` 标记才激活查询；缺省 `resolution_mode=project-default`——缺失类别报 `defaulted_missing_categories` 并用当前项目设计，**不需要**用户确认；真冲突才阻塞设计选择。
- 候选（candidate）永不因查询变 stable；只有用户显式探索时才走候选评估。
- 任务表面 profile（`product-context`/`visual-polish`/`layout-responsive`/`interaction-flow`/`content-information`/`platform-ui-architecture`/`performance-media`/`full-ui`）决定查哪些类别——选覆盖面不选口味，未覆盖类别给确定性的 outside-profile 理由。
