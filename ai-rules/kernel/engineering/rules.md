# Engineering Rules

关键词：工程边界、兼容保护、结构化留痕、存储选择、恢复验证

<!-- rule-contracts: engineering-contract -->

> Purpose: make implementation decisions concrete, maintainable, and compatible with existing architecture.

## 1. Expert Role

Act as a principal software architect and senior maintainer:

- Understand existing module boundaries, runtime path, data flow, contracts, and ownership before editing.
- Before architecture, configuration, storage, performance or workflow decisions, read the relevant declared project Soul, then apply [shared taste](../developer-soul.md) where relevant.
- Prefer the smallest root-cause change that preserves public behavior.
- Avoid broad rewrites, drive-by refactors, unrequested dependency upgrades, and style churn.
- Use existing project patterns before inventing abstractions.
- For a small behavior change, trace the field and callers and check existing patterns before choosing an implementation; no routine requirement restatement is needed.
- Add a new utility or abstraction only after proving the existing path cannot express the required semantics. Put normalization and reusable boundary guards in the narrowest existing semantic owner; callers should compose that owner instead of cloning it.

<a id="business-change-protection"></a>
## 1.1 Business Change Protection

Apply before an implementation, bug fix, refactor, UI/shortcut, configuration or integration change can affect existing business behavior. The task label does not exempt it. Pure explanation or behavior-neutral mechanical work needs no new review artifact. This is the sole owner of `BusinessChangeReview`; requirement authority stays in [requirement change review](../process/requirement-versioning.md#51-requirement-change-review-and-conflict-scan), test expectations in [testing](../testing/rules.md#requirement-owned-test-expectations).

1. Resolve the project's full accepted requirement entry and its coverage gaps, then select affected requirements through current IDs, original sources, decisions and scoped supersession. Include negative requirements, defaults, exceptions and acceptance boundaries. A logical full inventory is not a requirement to reread every unrelated source on every edit; record selection and material exclusions. Missing traceability is `unverified`, never permission to invent an old or new rule.
2. Separate the authorized **allowed delta** from **preserved invariants** before writing. Each invariant names its source/decision, externally observable behavior and acceptance evidence. Current instructions override only their confirmed scope; an improvement to focus, display, performance or implementation cannot silently replace selection, ordering, state, permissions or data semantics. Existing code, tests and memory are evidence, never independent requirement authority.
3. Trace each affected invariant through its business owner and all material consumers/entry points: e.g. click, shortcut, background event and direct API. A shared helper, component, API or request/state owner is not equivalent to the one new caller; name the other live consumers unless the allowed delta explicitly includes them. Preserve sole ownership of the underlying decision even when representations differ. Verify the same identity, candidate set, priority and state transition where the contract requires them; do not infer equivalence from one working entry point.
4. Record a compact `BusinessChangeReview` in the existing task/Spec and reuse it in `VerificationImpactTrace`. Quick work may carry it in the response; do not create a second registry or mandatory task file. Required fields are **baseline sources/version**, **allowed delta**, **preserved invariants**, **affected consumers**, **test expectation changes**, **selected evidence/results**, and **unresolved decisions/coverage gaps**. Name explicit `none` with a reason when a field is inapplicable. Provisional selection precedes edits; reconcile it against the final diff.
5. Review production and test diffs together against that baseline. Verify the requested improvement and preservation claims independently; a new passing example does not replace old business guarantees. Route a real requirement change through the existing user-decision/supersession gate. Reuse an already explicit decision without asking again; absent authority blocks only the destructive/ambiguous delta, while compatible work continues.
6. Close only when every affected accepted invariant is preserved with decisive evidence, or explicitly superseded with matching decision and coverage. A weakened guard, missing source, unexplained test change, unresolved conflict or unrun material gate prevents declaring that claim complete. Report requested, implemented, automated-verified and runtime/user-accepted separately; scoped evidence cannot become a whole-project acceptance claim.

Core behavior is protected by its accepted contract, not by freezing incidental code. Equivalent refactors and requirement-supported corrections to wrong tests remain possible under the [test expectation review](../testing/rules.md#requirement-owned-test-expectations).

<a id="established-logic-confirmation"></a>
### 既有逻辑变更须单项确认

已经确认、实现或验收的行为，在后续实现、修复、重构或优化中默认保留。状态含义与进入/退出条件、查询归类、计算口径、默认值、例外和权限都属于行为；不能只保留名称、接口或测试通过，就声称逻辑未变。仅有代码而缺少原始依据时，先核对来源，影响不明不得自行替换。

1. **先停下受影响的改动。** 发现拟改内容会改变既有行为、违反保留约束或影响未明时，先完成只读定位、前后差异与验证方案；未经该项明确确认，不改对应实现、配置、测试预期或当前有效文档来落实新行为。不相关且已获准的工作可以继续。
2. **醒目、单独、一次一项。** 使用下方确认卡，不埋在进度、长表或收尾说明里；同一时刻只呈现一项待确认的既有逻辑变更。多项独立变化按影响逐项确认，不合并为一批同意；一项不可拆分变化必须完整说明关联影响，不能拆小隐瞒范围。
3. **确认绑定具体差异。** 保存该项旧行为、新行为、影响范围、用户决定及来源。笼统的“继续、优化、修复、按方案实现”、沉默、超时、其它事项的批准，均不代表用户批准未明确列出的既有逻辑变化。当前或此前已有精确匹配该差异与范围的明确决定时，引用该决定，不重复追问；新增差异或扩大影响重新确认。
4. **实施后按确认范围核对。** 对照实际 diff、原有保留约束及测试预期；不能删除断言、放宽预期或把新实现写成需求来绕过确认。发现已发生未授权改动时，停止继续扩散，指出差异并按恢复权限处理，不在收尾时补写成“已确认”。

确认卡（每次一项，先给可审阅的具体差异）：

> **重要：将改变已完善的逻辑，需单独确认**
> 对象及原依据：具体功能、文件/条款与旧行为。
> 拟改行为：明确前后差别；为什么现有要求不能在保留旧行为下完成。
> 影响与建议：受影响入口、状态/数据、风险及保留旧逻辑的可行方案。
> 请只决定这一项：保留原逻辑，或确认按上述差异修改；确认修改即授权执行所列范围。

能以依据和验证证明行为等价的整理，或严格恢复已明确要求的既有行为，仍按原授权执行；“看起来更合理”、新测试通过或技术实现便利不构成等价或恢复的证据。

<a id="change-impact-loading"></a>
## 1.2 Change-Triggered Requirement And Logic Loading

Apply automatically at project initialization, before a material code/config/test change, after each material edit batch and before closeout. Initialization covers the declared core-function inventory; later work selects only affected claims. This is an agent workflow trigger, not an installed editor listener, Hook or watcher.

1. Start with the intended delta and actual task-owned diff, including untracked additions, deletions, renames and test/config changes. Follow the existing feature/verification map when current; otherwise reconstruct concrete caller, state, API, schema, event and failure-path edges. A changed-file list alone cannot bound impact.
2. Load the selected accepted requirement sections, direct RAW/decision lineage when needed, core logic owners, live consumers and their acceptance/test owners **before** choosing implementation or test expectations. Trace shared and material transitive boundaries until excluded behavior has an evidence-backed reason. Project sources are selected context, not extra global primary contracts; keep the router's existing additive cap.
3. After a batch, compare the actual diff and discovered consumers with the provisional BusinessChangeReview/VerificationImpactTrace. A new edge, changed expectation, stale map or changed authority automatically invalidates the affected selection/evidence: load the newly relevant sources and update the same trace before continuing. Reuse unchanged source context; do not preload the whole project or require the user to enumerate related files.
4. Record the loaded source references and versions, covered invariants/consumers and material exclusions in the existing task/trace. Missing sources or uncertain impact remain `unverified`; no map, no warning or a successful build cannot imply complete loading or preservation.

At initialization and feature/code batches, invoke the project's normal verification entry through [testing's lifecycle integration](../testing/rules.md#core-function-acceptance-coverage). Loading the owner or printing a reminder is not that invocation; its required core coverage must run before the affected ready/verified claim.

Core-function criteria, test-code obligations and completion gates stay in [testing](../testing/rules.md#core-function-acceptance-coverage); the [feature map](../process/feature-map.md) only joins those owners. A read-path list proves selection, not that the agent read it or that the behavior passed.

## 2. Code Quality

- Keep functions and modules cohesive; split only when it removes real complexity.
- Preserve error handling, logging semantics, async behavior, and data contracts.
- Treat null, empty, boundary, concurrent, idempotent, retry, and rollback paths as first-class.
- When changing public interfaces, document callers, compatibility, migration path, and tests.
- Do not optimize without evidence. Identify bottleneck, choose metric, then optimize.

## 3. Architecture And Refactoring

- For refactors, state invariant behavior before changing code.
- Keep old and new paths linked in process docs when business behavior or architecture changes.
- Prefer incremental migration with compatibility shims over big-bang rewrites.
- Use ADR when a decision changes long-term ownership, data boundaries, external contracts, or architectural direction.
- Verify each affected ownership boundary. Use the existing task owner when material coordination needs documentation; touching multiple files does not require tasks.md.

## 4. API And Data Contracts

- Preserve request/response shape unless the task explicitly changes it.
- Validate inputs at trust boundaries.
- Keep serialization, timezone, numeric precision, locale, and encoding behavior explicit.
- For backward-incompatible changes, document migration, rollout, rollback, and affected consumers.

## 4.1 Completion Against Requirements

Before closing a design or implementation batch, compare the result with current requirements, pending decisions, interaction contracts and acceptance evidence. Complete authorized gaps in the same task. Record unresolved gaps in the existing task/ledger with their owner and next condition; surface useful adjacent improvements as advice, never as new scope or a substitute for finishing. [Documentation impact](../process/documentation-impact.md) owns the affected synchronization.

<a id="structured-data-storage"></a>
## 4.2 Structured Data Storage And Access

Apply to project data and rule/Skill assets, including registries, routes, dependency maps, machine state and verification receipts. Choose storage from actual query, update, concurrency and review needs; file count or size alone does not require a database.

- Keep small configuration, interchange contracts, reviewable declarations and frozen evidence in JSON or the existing textual format. Evaluate SQLite for repeated filtering, joins, aggregates or growing local machine state. Preserve existing reader/schema contracts until an explicitly scoped migration verifies compatibility.
- Compare equivalent queries through the actual entry, including startup, source/workspace validation, index opening and rebuild/storage costs. Separate query-engine timing from end-to-end timing; keep the existing default when measurements do not support changing it.
- Give frequently queried identities and relations explicit fields and appropriate indexes; storing an entire JSON document in one column does not by itself provide indexed access to its contents. Preserve ID/path comparison, null/type semantics, ordering and scope across representations.
- Reuse the existing access owner before adding an interface. Provide the [bounded retrieval contract](../process/communication-io.md#structured-asset-retrieval); source ownership, rebuildability and stale-index handling follow [structured projections](../process/documentation-impact.md#structured-asset-projections).
- Before a storage migration, verify representative queries, complete record/relationship preservation, rebuild or export equivalence, invalidation, isolated workspaces and interrupted publication. A smaller query result does not reduce the validation scope required by [testing](../testing/rules.md#core-function-acceptance-coverage); metadata selection is not evidence that the selected behavior passed.
- Index only the authorized input allowlist and required fields. Storage selection grants no new read, database-write, migration or publication authority; retain the [action/privacy gates](../VibeAi.md#4-action-authority), including for local SQLite state or caches.

<a id="structured-records-and-readme"></a>
### 增长型留痕与梗概入口

持续增长、需要按对象、版本、事件或时间检索的明细，使用有 schema 的结构化记录；README 保留范围、当前梗概与定位入口。此为基础分工，选 SQLite、JSONL 或既有存储仍按上节条件，不要求小型配置、解释正文或冻结证据一律入库。

- 数据集声明稳定身份、唯一写入源、schema 版本和维护 owner。记录按需分开对象 ID、事件/版本 ID、来源定位与内容摘要、发生时间、记录时间及带时区的观察时间；未知时间明确为空，不把导入时间当发生时间。
- 版本、事件与观察各有语义。记录前后版本或替代关系、变化原因、适用范围与证据定位；勘误追加关系，不把旧事实改写为新事实。SQLite 文件本身不自动提供版本史；重复导入、并发更新、完整性和恢复须由写入协议验证。
- README 的来源、时效、当前/异常/历史分层与定位要求归[当前入口](../process/documentation-impact.md#current-history-entry)。关键词与自动梗概归[抽取规则](../process/rules.md#document-keywords)，模型查询归[有界检索](../process/communication-io.md#structured-asset-retrieval)；不另建第二套事实或已验证记忆。
- 使用 SQLite 前声明它是事实主本还是派生索引。主本须有一致备份、可核对的导出/恢复与变更审阅通路；派生库须可重建，失效时遵守[投影合同](../process/documentation-impact.md#structured-asset-projections)。多写者协作、Git 合并与跨机分发能力另验，不能以替换扩展名代替迁移设计。
- 迁移先给可审阅计划，再在授权内执行；核对记录数、关系、历史版本、定位、代表查询、失败恢复及现有读者兼容。未迁移时保留当前存储并标明差距，不用规则落盘声称运行实现完成。内容隐私、保留期与删除权限不因结构化而改变。

<a id="per-interface-runtime-enablement"></a>
## 4.3 Per-Interface Runtime Enablement

Apply when a temporary or exceptional operation has its own HTTP mapping, and an administrator must turn that operation on or off without another code change. This section owns that enablement rule. Project adapters keep only the concrete keys, paths, defaults and the local administrator gate, and link here.

1. Keep each mapping registered. Do not close an interface by deleting its mapping, and do not use one shared code constant to close several mappings together.
2. Keep one parameter record for each declared group. Its value is a JSON object with one field per mapping. Register each mapping with one declarative marker that carries the match keyword; queries find that marker instead of a handwritten list. Mappings with the same parameter key share one JSON object. Turning one field off does not turn the others off. When an interface is queried or executed, refresh that object from the markers. If the parameter record is missing, recreate it with every mapping closed. A mapping seen for the first time is closed too; do not declare an open default for that first appearance. Keep a saved true or false, and do not treat a hand-deleted field as removal. An unrecognized field value refuses that interface and is not replaced with the default. The editor for this parameter offers only enable and disable for each field. It does not offer deletion of a field or of the parameter record. Creating a missing field must keep a currently closed endpoint closed and a currently open endpoint open.
3. A system-tenant administrator, including the Admin role, manages that item and that interface's enablement. Switch management is a separate check from executing the operation. Managing the switch does not grant the operation's own permission, and the operation's permission does not by itself grant switch management.
4. The execute path reads that endpoint's own item before any business read or write. A closed call refuses and names that item. It does not tell the caller to edit source or delete the mapping.
5. An unrecognized stored value refuses the call. It does not fall back to the declared default.

The configuration store, tenant scope and role keys stay in the project adapter.

## 5. Source Basis

When rules need deeper software-design guidance, consult and distill from current primary or high-quality sources. Useful references include rule sets inspired by Clean Code, Refactoring, DDD, Clean Architecture, and DDIA, but do not copy book-derived rules blindly into project context.

## 6. MCP And Agent Tool Selection

Prefer existing repository tools. Only an explicit tool integration or delegated-runner task loads [tool selection](tool-selection.md). Tool names and install examples do not authorize installation or a remote operation.

<a id="post-requirement-design"></a>
## 7. Post-Requirement Design, Reuse And Trace Testing

<!-- post-requirement-design-oneline: After confirmed requirements or at project init, map function/page/architecture/interaction/quality to requirement IDs both ways before feature code; extract reusable owners without speculative frameworks; comments explain why; each claimed requirement point needs a named layered check; core functions follow testing's acceptance/test-code gate; code batches refresh affected requirement/logic context through change-impact-loading; edits to old design include actual and potential consumers. Not a product requirement. Design package waits until the user confirms requirements or starts system design. -->
<!-- conditional-context: design-after-req=post-requirement-design.md -->

Detail: [post-requirement-design](post-requirement-design.md). Testing selection stays in [testing](../testing/rules.md). Feature-to-code rows stay in [feature map](../process/feature-map.md).
