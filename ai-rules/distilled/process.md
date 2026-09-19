# 过程层：任务分级、文档纪律、断点续作

> 蒸馏自：process 域各 owner（任务分级、预检、文档同步、归档处置、worktree 生命周期、需求版本化、checkpoint/resume、需求枢纽、feature-map、intent-notes、引导式执行）。verbatim 的 `kernel/process/` 四文件（outcome-stop、prior-overlap、sidecar、communication-io）和九份模板随包携带，此处不复述。

## 1. 任务分级（最小足够级）

| 级别 | 适用 | 任务文档 |
| --- | --- | --- |
| Quick | 小、可控、可逆、单会话、验证路径直接 | 无任务文件；终态回复承载决策与证据 |
| Standard 非需求 | 中等连续性或评审风险，无需求增量 | 一份 `task-card.md` |
| Standard 需求 | 有界需求增量、无需受控恢复 | `raw-requirement.md + spec.md` |
| Controlled | 高风险/跨仓/发布权限/DB 边界/长周期恢复/多方协调 | `spec.md / plan.md / tasks.md / verify.md / handoff.md`（带需求再加 raw） |

原则：文件数、可否委派、文档可用性都**不**升级任务；用能保住连续性/权威/恢复的最小级。模板在 `kernel/process/templates/`。

补充产物：

- `changes.md`：交付跨多个文件/批次/会话时必填——只回答"改了哪些文件、每个改了什么"，每行带一句核心描述，从实测事实（git diff、扫描输出）生成，不凭记忆。
- `assessment/`：对既有任务的评审/复核/二审落盘在被评任务自己目录的 `assessment/` 子模块（`<yyMMdd>-<评审方>-<类型>.md`，追加不覆盖），索引用 `assessment-index-template.md`；它是证据不是 owner，冲突由一手重跑证据裁决并写回 `verify.md`。

## 2. 预检门（material work 之前）

1. 解析仓库边界、脏树、权威边界；
2. 分级 Quick/Standard/Controlled；
3. 带需求的工作先跑需求变更评审，待定决策挂起；
4. 跑 Prior Task Overlap（`kernel/process/prior-task-overlap.md`）：`reuse | delta-only | no-op | supersede | new-task`；
5. 判断独立评审是否实质降险（sidecar 条件触发，非默认）；
6. 声明验证 owner 与文档影响分类；
7. 非平凡实现先完成 Plan-mode 预检包再写第一个字。

**Plan-mode 预检包**：范围（目标/界内/界外/风险边界）、文档级与产物、测试范围策略（从改动面推 `VerificationImpactTrace`，聚焦检查不需要用户枚举，全量套件需要一个记录的升级触发）、prior-overlap 决策、文档影响分类（`none-with-reason | task-only | project-current | requirement-canonical | global-rule | template-propagation`）、Authority Packet（咨询过的 owner + 确切问题/预期增量）、`doc_drift` 解决策略。任一字段不可得 → 停下来问最小问题。

## 3. 文档同步与归档

- **single authority**：每个事实一个 owner；枢纽/索引是派生视图，不复制事实本体。
- **同轮同步**：行为/架构/配置/数据契约变化后，受影响的所有 owner 在同一任务内同步；`doc_drift`（源与文档不一致）要显式报告、按权威裁决，不静默选边。
- **Documentation Sync Group**：每个 Work Unit 一个稳定 `group_key`，任务 owner 维护一个活跃 `documentation-sync-group` 块（Git 文档前缀 + 成员清单 + 排除的无关脏文档）；验收用成员必须显式进回执，前缀只做发现。
- **归档处置**（Document Archive Disposition）：候选分类唯一——`retain-current | archive-pending | archived-linked | physical-migration-ready | archived-physical`。默认 `archived-linked`：原路径保留历史体 + 头部归档通告（`document-archive-notice-v1`）指向当前替代；物理迁移需要项目声明归档根 + 精确 `source -> target` 映射 + 全部链接/符号链接/Git 可恢复性通过 + **动作时刻的精确授权**（"ready" 本身不授权移动）。

## 4. 执行日志纪律

- Quick 无日志；Standard 记在 task-card/spec；Controlled 用 `tasks.md`。
- 只记**改变执行的事件**：分派、用户纠正、中断、失败、回退、reported/accepted/rejected/superseded。不记常规搜索、prompt、转录、原始输出、命令、密钥、隐藏推理。
- 效率/Token 证据：有可比基线才记；无计数器写 `usage unavailable`；不从模型名推断节省、不为了指标重跑。

## 5. Worktree 生命周期

- 触发信号：大改/跨仓/并行/主仓脏/恢复敏感。选不选 worktree 与任务分级**无关**，不因此升级测试或权限。
- **主仓 = 控制面**：分支创建、里程碑、集成、清理归主仓；子 worktree 结果保持 `reported`，只有主任务能 accept/integrate/close。
- 同轮状态同步：子树进展以有界状态回主仓，主仓是唯一账本。
- 推送边界：未授权不 push；集成前过验证与文档同步；清理打包（分支/状态/残留）一次性做完。

## 6. 需求版本化

- **权威分层**：原始输入（`raw-requirement.md`，逐字保留）→ 规范化当前权威（`spec.md` Canonical Merge）→ 实现证据（verify/代码）。三层不互相覆盖。
- **需求清单**：需求项有稳定 ID（`DEC-*` 决策 / `ARCH-*` 架构等世系），变更走显式评审而非就地改写；移除走归档链不删历史。
- **变更评审**：带需求的改动先扫冲突——与现有权威冲突的列给用户裁决，未裁决前不实现。
- **spec delta**：增量需求写 delta，不进 Canonical Merge 前不算权威；merge 是显式动作。

## 7. 断点续作（Checkpoint / Resume）

- 项目维护一个 resume 登记表，条目为 `RP-nn`：任务指针、已验证状态、下一步、恢复时要重查的回归点。
- 恢复时按条目重放验证而非信任叙述——登记表是索引，证据在任务文档里。
- 中断/交接/跨会话的任务在收尾时显式写 resume 条目；完成即关闭条目，不堆积。

## 8. 派生视图与标记（按需，不默认建）

| 机制 | 触发 | 形态 |
| --- | --- | --- |
| Requirements hub | 项目需求迭代超过阈值 | 实时同步的派生需求视图；不复制权威体 |
| Feature map | 需要"功能→实现"导航 | 派生索引，链接 owner 不复制 |
| Intent notes | 用户显式要求记意图 | `IN-nn` 标记，挂在需求世系上；无活动 note 不建空表 |

## 9. 引导式执行

需求不完整但有明确推进意图时：把待定决策列成编号清单让用户逐项裁决，已决项立即生效，未决项保持 pending；不要把"引导"变成无确认的实现。
