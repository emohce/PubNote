# Testing And Verification Rules

关键词：最小充分验证、影响追踪、需求保护、证据边界、结果复用

<!-- rule-contracts: verification-selection -->

This file is the sole owner of general verification selection and completion evidence. Domain specialists own protocol-specific replay suites; project authorities may narrow or strengthen a known local boundary, and task evidence records the selected route and actual outcome.

## 1. Default: Minimum Sufficient Verification

Choose the smallest evidence set that can falsify the changed contract and its material propagated effects. Test count is not confidence, and a repository-wide or system-wide suite is never the default acceptance gate.

Verification scope comes from the actual change and its impact graph, not from task size, document level, file count, dirty-tree size, commit intent, the existence of a `test` script, or a historical task that once ran a broader suite. Normal focused checks do not require the user to enumerate test files. Adding or running unrelated checks is out of scope.

Do not author tests that only restate a reversible, low-impact implementation. After the selected checks pass, expand or repeat only on a new change, a new failure, or an unresolved doubt. Delete unused task-local temp files at closeout.

Prefer this order when applicable:

1. static/source/configuration validation for an obvious local contract;
2. focused unit or contract checks for the changed behavior;
3. affected-package semantic type/compile/build evidence when the change reaches that boundary;
4. bounded integration/runtime evidence only for an affected boundary that static checks cannot prove;
5. broader regression only after a recorded escalation trigger;
6. user-owned acceptance for subjective UI/product judgment or externally controlled systems. When the user asks to view or accept the current local frontend and backend, use [本地前后台验收开页](../memory/ego-browser-preferences.md#本地前后台验收开页). Login and look-and-feel remain user-owned. A restarted or continued acceptance run uses the [result report](#result-report) before opening the page; opening it is not acceptance.

## 2. Change And Impact Analysis

Start from the intended behavior delta plus the current Git change set, including task-owned untracked files. Resolve impact through concrete edges: imports/exports and callers, package dependencies, public API/schema/config contracts, routes/events/jobs, storage or permission boundaries, generated artifacts, build graph, host integration and known failure paths. A changed-file list by itself is not an impact analysis.

### 2.1 Project Verification Map

A project may keep a reusable `ProjectVerificationMap` in its existing architecture, knowledge or rule owner and link it from the project entry. The map is an accelerator, not a prerequisite for [§2.1.1](#round-pending-test-list). Do not create a map for one isolated change when dynamic analysis is cheaper and no reusable edge was found. Each maintained row records:

```text
surface selector / behavior or contract / direct consumers / transitive boundaries / focused checks / escalation triggers / owner / last verified
```

Use the map only after checking that its selectors, commands, package graph and owner are current. A missing or stale map is not a reason for full-suite testing and does not waive consumer preservation; reconstruct the current task's impact graph from targeted source, manifest, build and test evidence. When implementation reveals a stable missing edge that will be reused, or a collateral regression is verified, add or refresh the map row in the same round (create the map if none exists). Do not duplicate the same mapping in every task.

<a id="round-pending-test-list"></a>
<a id="collateral-change-binding"></a>
### 2.1.1 Round Pending-Test List And Collateral Binding

This subsection binds every CodeNote-routed project. A missing `ProjectVerificationMap` does not waive it.

`VerificationImpactTrace.Selected checks` is the round pending-test list (`本轮待测试清单`). Write the provisional list **before** material edits and reconcile it against the final diff. Populate it from, in order:

1. matching current map rows, if any;
2. the current impact graph: changed surface, direct consumers, material transitive and failure-path boundaries;
3. preserved invariants from the [BusinessChangeReview](../engineering/rules.md#business-change-protection).

Matching map rows are appended automatically. Without a map, reconstruct the same consumer set from callers, contracts and known failure paths. Do not treat “no map” as “only test the new feature”.

Shared-surface binding applies to any helper, component, public API, default/filter/submit/ordering/pagination/loading/permission contract, or request/state owner used by more than one live caller:

1. Include preservation checks for every live consumer the change can affect, not only the new caller or the shared unit's own tests.
2. If a preserved invariant has no focused check, add a characterization/preservation test in the same round, or record the claim `unverified`. Do not invent a repository-wide suite or user-owned browser run to fill the gap.
3. An authorized behavior change updates the prediction first, then the implementation; other consumers' assertions stay until their own allowed delta says otherwise.
4. User-owned acceptance stays on the reminder list and is not auto-run.
5. A feature that reuses a shared surface may not rewrite another consumer's default, filter, submit, ordering, pagination, loading-state or permission contract as a supporting edit. Ask: if this hunk were dropped, would the authorized delta still hold? If yes, it is a separate allowed delta under [business change protection](../engineering/rules.md#business-change-protection). After a verified collateral regression, persist a map row in the same round.

### 2.2 Verification Impact Trace

Quick 的简明 `VerificationImpactTrace` 留在回复；Standard 留在 Task Card 或需求 Spec；Controlled 留在声明的[交付职责](../process/rules.md#content-role-profile)中。旧五文件布局继续以 Plan 记录初选、`verify.md` 记录最终结果；布局变化不改变验证内容与门槛。

| Field | Required content |
| --- | --- |
| Changed surface | Task-owned code/config/docs and the behavior or contract changed |
| Impact evidence | Map row or targeted dependency/caller/schema/build/runtime evidence |
| Affected set | Direct consumers plus material transitive and failure-path boundaries |
| Selected checks | The round pending-test list: smallest checks covering every material claim, including matching map rows or reconstructed live consumers |
| Skipped checks | Named broader suites/boundaries, exclusion reason and residual risk |
| Escalation | Trigger, wider check and decision it would change; otherwise `none` |
| Outcome | Actual result, unverified gap and evidence owner. Use the [result report](#result-report) when the work is a restarted or continued acceptance run, or when the user asks for a result review |

Create the provisional trace before material implementation when the impact is already knowable. Verification commands are outputs of that trace, not inputs to it: before an Agent-authored or Agent-expanded plan names a command or suite, record the provisional changed surface, affected set, selected checks, skipped checks and escalation state. Reconcile an incoming plan's verification clauses against this owner before accepting or executing the plan, then reconcile the trace against the actual diff afterward. A newly discovered consumer updates the same trace and, when reusable, the project map; it does not silently widen into an unrecorded full gate.

<a id="result-report"></a>
### 2.2.1 Result Report

Use this report for a restarted or continued local acceptance run or a requested test-result review. Keep the evidence in the existing carrier from §2.2: Quick may report in the reply, Standard in its Task Card/Spec, and Controlled in its verification record. Reporting alone never requires a new `verify.md`, task package or test execution.

The coverage set is the whole evolved goal, including already-passed points. Give each accepted checkpoint a stable key and a requirement/decision reference; distinguish materially different scenarios, environments and verification levels. Keep those keys across rounds. A superseded requirement stays in history with its successor and decision source, not as a second current obligation. Do not reopen an already-resolved decision merely because an older expectation differs.

Count one current conclusion per checkpoint/scenario key, using its latest complete evidence that is valid for the current requirement and source/environment boundary. Historical attempts, duplicate summaries and raw unit-test counts are not extra checkpoints. Preserve failed and retest rows together in a separate attempt history or linked step log, with the same key; do not also count a resolved historical failure as a current failure. State the counting unit and do not mix requirement, test-case and attempt counts.

Start with a prefix naming the report version/status/date, coverage total, counts for `已通过`, `失败`, `不符合`, `未测`, the checklist's existing evidence entry, and the environment or linked environment record. Use mutually exclusive current buckets; add `待裁定` when a requirement conflict prevents a conclusion. Their sum equals the declared coverage total; historical attempts are reported separately.

| Current bucket | Meaning |
| --- | --- |
| 已通过 | The scoped check completed and matched the accepted expectation; this includes an expected rejection. |
| 失败 | Applicable evidence establishes an unexpected failure, including an observed error or timeout; state product, test or tool/environment cause when known. A run interrupted before a conclusive result is 未测. |
| 不符合 | The operation completed but its observed business result missed the accepted requirement. Do not also count it as 失败. |
| 未测 | No complete applicable evidence: distinguish pending execution, blocked, excluded, interrupted/incomplete, or invalidated evidence requiring retest. |
| 待裁定 | The actual observation is retained, but competing requirements remain unresolved. Do not call it a product failure, unexecuted test or pass. |

Then show two sections: not-passed points first, passed points second. Keep both, explicitly saying zero when empty. Recommended columns remain `路径`, `结果`, `是否成功`, `符合要求`; the stable key and evidence may be in the path cell or a link, without forcing more columns. Add columns only when useful; leave an unused recommended column blank and invent no filler.

`是否成功` uses `成功`, `失败`, or `未测` with a reading/reason in parentheses. Record the actual operation in `结果`; an expected rejection can be `成功（按预期拒绝）`. `符合要求` uses `符合`, `不符合`, `未测`, or `待裁定` and references the actual requirement/decision. Verify that the linked line/anchor contains that requirement; file existence alone is insufficient. Preserve the executed observation even when its conformance is undecided. `未测（阻塞）` names the missing prerequisite and resume condition; `未测（排除）` names the user's exclusion or accepted scope boundary. Lack of authorization is pending/blocked, not evidence that the user chose to exclude it.

A failure inside the currently authorized implementation may be fixed and retested without a new product decision. Link the failure, change and retest. Distinguish `修复后通过` from `原样重试通过`: the latter retains the earlier failure and any unresolved instability/root-cause gate, rather than claiming a fix. Retry permission and bounds remain in §6. A report never grants browser, service, data-cleanup or other action authority. For an unresolved requirement conflict, record the competing files/anchors and consequences and stop only the dependent implementation until the user chooses.

Each current conclusion links its requirement version, observed time, tested source/build identity and material environment/fixture boundary. A dirty checkout needs the relevant patch/content identity, not HEAD alone; PID/port identifies a process, not its code. Batch defaults may be shared, but rows from another run must name their own evidence. Missing historical metadata stays explicitly unverified, never reconstructed as a measured fact. Reuse and invalidation follow [§6](#6-evidence-reuse-and-failure-handling): a restart or source/configuration/data/requirement change invalidates only affected claims; unchanged results may be carried with their original evidence and a stated impact basis. A changed page path is `未测（需重测）` until re-executed; an old unit result proves only the inputs it tested.

After the tables, record residual risks and leftover data: document, observed state/time, what it blocks, old residue or newly created data, and any accepted later-reset decision. Link unchanged details instead of repeatedly asserting an old state is current. Do not clean business rows without the applicable authorization. State that this is an agent record, not user acceptance; add no acceptance-passed column and infer no pass rate or release go/no-go from this report.

<a id="test-record-versions"></a>
### 2.2.2 Test Record Versions

A task with multiple documented acceptance rounds keeps one index under its existing task's `assessment/test-records/`; a Quick reply does not create this hierarchy solely for reporting. The index is the sole current-version pointer. `verify.md`, project hubs, maps and other consumers link that index rather than copying counts or independently choosing a version.

Each index row names version, date, state (`进行中` or `已封存`), meaningful delta and evidence file. If a new round is in progress, say so; its creation is not completion and must not imply that its pending points inherited an older pass. A version contains the whole evolved checkpoint set, valid carried evidence, attempt history links, residual data/risk and requirement conflicts. Keep old step logs in place.

An in-progress version may receive evidence and explicitly identified corrections. Seal it on completion or when the next version starts; sealing preserves a record, not user acceptance. After sealing, leave its observations and original counts unchanged. Put verified mistakes in a separate dated erratum linked from the index, identifying the original location, correction, basis and effect on conclusions. A later version consuming that evidence also cites the erratum; do not back-edit a sealed successor. Stable checkpoint/decision IDs and version-bound evidence preserve meaning when current-document line numbers move.

Update the index and affected current statements in the same authorized batch. Preserve historical records, label historical banners as such, and do not let stale failure/pass summaries compete with the current entry. Check links semantically as well as structurally. Do not delete a prior version or invent missing evidence to make the latest round appear complete.

<a id="requirement-owned-test-expectations"></a>
## 2.3 Requirement-Owned Test Expectations

For changes affecting established behavior, consume the [BusinessChangeReview](../engineering/rules.md#business-change-protection). Accepted requirements determine expected results; tests and implementation must not validate each other's unsupported assumptions. Keep the existing minimum-sufficient selection and full-suite escalation rules.

Keep stable requirement IDs/source links and existing business guards in the project's current verification map when it has one; otherwise record only the affected mapping in the task. Do not create a parallel requirement registry or silently assign accepted status to unregistered source fragments.

- Before editing a business expectation, inspect the previous assertion/fixture and its accepted requirement or decision. Classify the test delta as **add**, **equivalent-refactor**, **correct-wrong-expectation**, **authorized-behavior-change**, or **coverage-reduction**. Record before/after semantics, source authority and replacement coverage in the existing review. Unchanged tests need no per-test ledger.
- Preserve independent regression evidence for each affected invariant. Use a relevant existing guard, or derive a missing guard from accepted sources before accepting the new implementation. For a regression repair, show the guard rejects the known bad behavior and accepts the fix when a bounded replay is practical; otherwise state the evidence limit. Do not manufacture tests for behavior-neutral, low-impact edits.
- Deleting/skipping an assertion, weakening a predicate, widening a tolerance, reducing fixtures, changing snapshots or mocking away a business owner is a potential **coverage-reduction**, even when the suite becomes green. It needs either equivalent/stronger coverage of the same obligation or an explicit requirement decision retiring that obligation. A test rename or higher passing count is not replacement evidence.
- **correct-wrong-expectation** is valid only when accepted source evidence proves the old expectation wrong; code convenience, a new implementation, a green suite or an Agent-authored plan is not that evidence. **authorized-behavior-change** binds the current explicit decision or scoped supersession; do not ask again for an already granted change or preserve superseded business behavior as current.
- Separate delta checks from preservation checks. Shared decision logic requires affected consumer-path evidence (for example click → shortcut, or provider → reducer → view), including relevant sequence/concurrency/failure boundaries; pure selector assertions alone do not prove downstream consumers retained that selector's decision.
- After a confirmed requirement slice, each implemented requirement point needs a named verification path recorded as `requirement_id → check` and the reverse ([post-requirement design](../engineering/post-requirement-design.md#5-requirement-mapped-tests)). Interaction, cross-binding and auth include happy, empty/error and abuse cases. Changing an old module includes actual and potential consumers; untested old code gets characterization tests before behavior change. Prefer unit/contract over brittle UI. A missing path on an affected accepted claim is `unverified`. This does not escalate to a repository-wide suite.
- Before closeout, inspect the final test diff for lost coverage and bind the reported checks to the tested source state. Later relevant code/config/test changes invalidate only their affected evidence. Do not increase unrelated test scope to compensate for a missing business oracle. Unresolved expectation authority or lost required coverage leaves the affected claim **unverified**.

<a id="core-preservation-automatic-gates"></a>
## 2.4 Core Preservation And Automatic Gates

For an established shared state/command/selection/lifecycle owner, protect accepted invariants independently of the tests being edited in the same change. A green suite after its old business expectation was changed is not preservation evidence.

1. Before changing an existing business assertion, run the affected unchanged baseline guard or use still-valid executed baseline evidence. Bind the allowed delta to an explicit requirement source; if the guard fails after implementation, first explain that failure against the preserved contract. Do not classify it as a wrong expectation merely from the current implementation or an ambiguous request.
2. Where a verified regression escaped because its guard expectation was rewritten, add a small independent requirement-owned preservation check in the project's existing verification entry. It must exercise the semantic owner and material consumer outputs, reject the known bad implementation, and accept the corrected one. Editing the ordinary regression fixture must not change this check's oracle.
3. Connect such checks to an existing bounded build/validation/CI entry so producing or validating the affected artifact runs them automatically. Preserve the previous execution path and all existing gates; do not add services, watchers, unapproved hooks, full-suite runs or a second rule corpus. A deterministic package check should also exercise the packaged semantic owner when its source-to-artifact boundary is affected.
4. Record the trigger, accepted invariant, entry and negative-canary result in the existing VerificationImpactTrace/project map. Changes to this independent guard or its expected outcome require the same requirement and test-expectation review; automation does not authorize a business change or establish real-host acceptance.

<a id="core-function-acceptance-coverage"></a>
## 2.5 Core-Function Acceptance And Test-Code Coverage

At initialization, enumerate the project's declared core functions from accepted requirements and architecture; during implementation or changes, maintain the affected subset. Core functions include business decisions, shared state/command/lifecycle owners, critical flows, authorization/isolation and data-integrity boundaries. Incidental helpers and behavior-neutral cosmetic edits do not automatically become core functions.

Each core function binds its stable capability/requirement IDs to:

1. accepted requirement/decision anchors and its semantic code owner plus material consumers;
2. observable acceptance criteria: preconditions/input, action/state transition, expected output/invariant and applicable failure/negative/boundary cases;
3. actual test-code paths and case identifiers for every criterion, with fixtures and expected results derived from the accepted source rather than the new implementation;
4. the existing bounded validation/build/CI entry that runs those tests, and actual results bound to the tested source state.

Keep this mapping in the existing project verification/feature map or task VerificationImpactTrace; never create a competing requirement registry. Before first feature code, criteria and planned checks must be named. Before a core claim is automated-verified or complete, its test code must exist and the selected checks must have run; missing paths, omitted criteria, stale results or unrun entries remain `unverified`. Initialization may leave future functions planned, but cannot label them tested.

Use the narrowest meaningful unit/contract and affected-consumer tests; add integration or critical-flow tests only for their actual boundary. Exercise applicable empty/error/abuse, sequence/concurrency/idempotency and recovery cases. For a regression, demonstrate rejection of the known bad behavior and acceptance of the fix when a bounded replay is practical; otherwise state the evidence limit. Subjective UI and external-system validation remain separately user-owned and never replace tests for controllable core logic. Preserve §1's low-impact test exclusion and §4's full-suite gate.

Consume [change-triggered loading](../engineering/rules.md#change-impact-loading) before planning and after each code batch. Append matching core tests to the existing round pending-test list, wire them into an already-authorized project validation entry when that boundary is in scope, and invalidate only affected results after later source/config/test changes. A missing automatic entry is an explicit implementation gap; this rule does not install a Hook, service or CI workflow in another repository.

An optional `core-verification-map/v1` JSON export of that same mapping can be checked by [check_core_verification.py](../scripts/check_core_verification.py#L1). It has `capabilities` rows with `capability_id`, `requirement_refs`, `logic_paths`, `consumer_paths`, `criteria` and `validation_entry`; each criterion has `id`, `given`, `when`, `then` and `tests`, and each test has `path` and `case`. The checker selects impacted rows and required read paths, rejects missing declarations/paths and unmapped changes, and executes no supplied command. It proves declaration/file-metadata coverage only: neither selector existence, real CI wiring, semantic correctness nor executed-test acceptance. Consume its read list by actually reading the relevant owners; dynamic analysis remains required when no export exists or an edge is unmapped.

**Normal lifecycle integration.** At initialization, register the accepted verification entry and existing mapping in the compact project entry; run declared core coverage before claiming initialization ready. Feature implementation names criteria/planned tests before code, then automatically invokes the normal verification entry after each material batch and before completion. That entry selects affected registered cores and runs their tests without requiring the user or agent to remember a separate diagnostic command. Missing/failed coverage remains unverified. Unregistered affected behavior still needs dynamic impact analysis and its accepted checks; a partial map is never a full-project inventory.

CodeNote registers one `core-verification-map` in `vibe/rules/README.md`. Its [normal check_rules entry](../scripts/check_rules.sh#L1) invokes [automatic selection](../scripts/auto_core_verification.py#L1) in fast/full/default modes using staged, unstaged and untracked Git paths; `--init` selects the declared inventory. Map/registration changes also select the inventory. The existing [test executor](../scripts/run_core_verification.py#L1) checks actual bindings and runs selected cases; failures, skips and source changes block completion. The legacy skip variable cannot skip this gate. `--core-map` remains an explicit diagnostic lane. This CodeNote-only executor runs no export command and establishes no other project's framework/CI or fresh-host acceptance; no editor watcher or Hook is installed.


<!-- core-inventory-disposition-gate -->
CodeNote 的全项目核心连接通过项目唯一功能索引登记；正常入口在执行选择前核对 Git 可见可执行文件与 canonical Skill 的逐文件处置，并核对已登记 Python 测试类中新增用例是否有绑定。新增未分类、失效处置、漏绑用例不得以“范围外变更”静默放行。`registered` 只表示标准/代码/测试/入口连接齐全；程序型 Skill、参考、历史及外部/人工验证各保留来源和处置理由，未跑的真实宿主/设备/业务门禁仍是未验。JSON v2 是该既有连接的派生导出，固定审核过的 Python/Node/Swift 车道不执行导出里的任意命令；全部自动化通过也不证明所有分支或所有 Skill 场景完成。

## 3. Selecting The Affected Checks

For every material acceptance claim, select at least one check able to fail when that claim is false. Deduplicate checks when one command demonstrably covers another; for example, a build satisfies semantic typecheck only when its output proves that configured typecheck ran.

| Changed surface | Minimum candidate evidence | Add only when impacted |
| --- | --- | --- |
| Leaf/domain logic | Closest unit/contract tests and local static checks | Direct caller or failure-path tests when the contract crosses the leaf boundary |
| Shared/public API or library | Changed contract tests plus affected direct-consumer compile/tests | Transitive package checks only for consumers reached by the dependency graph; shared defaults include every live caller, not only the new one |
| Frontend/UI/runtime source | Focused component/state tests, matching map rows or reconstructed consumers, and affected-package semantic typecheck | Shared helper/component changes include live consumer rows. Build when bundle/output/config/entrypoint behavior changed; runtime/visual/interaction evidence only for affected states. If the write set is a review-document or position-navigation surface, add [named UI preference checks](../scripts/check_named_ui_preferences.py#L1) (`PNP-*` / `RDA-*`) plus A-class runtime probes; do not copy those owner algorithms here |
| Backend/service/shared logic | Focused module/service tests and affected-target type/compile evidence | Shared module changes include live consumer tests, not only the new caller. Integration smoke only for a touched boundary that static evidence cannot prove; do not launch a service merely to compile |
| Build/config/dependency/codegen | Parser/schema/graph check plus builds or tests of packages receiving the changed output | Repository-wide build only when a root input has verified unbounded fan-out |
| Docs/rules/Skills | Changed-owner links, ownership/conflict and affected route/replay checks; one strict batch for changed Skills (strict includes base checks) | Whole registry/tree/manifest audit only when contract identity, discovery, ownership, publication or generated inventory changed |
| SQL/schema/data handoff | Static contract, pre/post/rollback and authorized read-only evidence | Runtime/DBA path owned by the DB gate; agents do not execute mutation SQL |

Project-specific prohibitions and required host/runtime evidence still apply. They must name the affected boundary; they do not authorize unrelated project-wide testing.

## 4. Full-Suite Escalation

A full repository, monorepo or system suite may run only when at least one trigger is recorded in the `VerificationImpactTrace`:

- the user independently and explicitly requests that exact wider suite as the current verification outcome, or an applicable release policy requires it;
- a current project map names it for the changed selector and explains the fan-out;
- a root build/toolchain/lockfile/codegen/public-contract change has materially unbounded consumers after targeted analysis;
- a focused failure or newly discovered dependency proves the provisional affected set incomplete;
- security, authorization, persistence, concurrency or data-integrity behavior cannot be bounded by a smaller check set.

Before escalation, record why focused evidence is insufficient, the exact wider suite, its expected decision value, cost/side effects and stop condition. Approval, continuation or implementation of an Agent-authored or Agent-expanded plan does not convert a suite that the Agent inserted into an independent user request; the Agent cannot bootstrap its own escalation trigger. If such a plan conflicts with this owner, update the plan before implementation. Controlled/global/multi-file work, staging/commit/push preparation, a dirty worktree, or a historically green full suite are not escalation triggers by themselves.

If impact cannot be bounded and the justified wider suite cannot run, report the affected claim as `unverified`; never substitute an unrelated green suite or silently weaken the gate.

## 5. Execution And Runtime Boundary

Tests, semantic typechecks and compile/package builds may run when they are selected by the impact trace, deterministic, bounded and non-watch. This does not authorize starting an application, native host, browser, service, dev/preview server, watcher, daemon, scheduled job, deployment or external write. Treat generated packaging artifacts as worktree changes and preserve unrelated files.

A transpiler, bundler parse or syntax-only check is not semantic typechecking. Passing typecheck/build does not prove real-runtime UI, native-window, integration or user acceptance behavior.

## 6. Evidence Reuse And Failure Handling

Reuse deterministic evidence only when relevant inputs, tool/version, configuration, environment boundary and Git view are unchanged. Reuse may remove a duplicate check, but it must remain linked in the trace; no unpromoted verification cache is authority.

<a id="same-round-verification-owner"></a>
### Same-Round Verification Owner And Freeze

Root names one final verification owner for a Work Unit. Other sessions return delta evidence to that owner; they do not launch an equivalent final gate or write shared acceptance inputs during its frozen interval. The document executor first reconciles required owner, task and current/status projections; preserve historical evidence by link and finish those input writes before freezing.

The owner binds the selected checks to the actual relevant source/requirements/configuration/test/registration/validator bytes, tool/runtime and environment boundary, Git view and reviewed change set. Record map-external changes and their dynamic impact disposition separately: a registered-core pass never silently covers them. A frozen result becomes reusable only after the required checks pass and readback confirms the same bound inputs. Do not remove a real authority from the input set to prevent drift.

Within that same round, a downstream summary, closeout or wrapper consumes the already accepted result and evidence reference after checking the matching scope/inputs; it does not rerun a green test, receipt lookup or check merely because the caller changed. If relevant inputs, requirements, registration, runtime, Git view or scope change, invalidate the affected result and route only necessary checks back to the same owner. Uncertain matching means `unverified`, not a cache hit. 本节不引入跨调用持久缓存或新结果账本；仅明确采用下方[受控发布批次回执](#release-batch-receipt)的发布入口可按该限定合同复用。其他检查不因此取得持久缓存权限。

When CodeNote initialization and the unchanged change-core gate are due together, the existing `check_rules.sh --init-fast` executes the core once and re-evaluates the change selection in that process. Consume its two phase outcomes; keep its outside-map flag and legacy fast checks. This does not make an earlier `--init` reusable after material edits, skip required dynamic checks or turn focused evidence into a repository-wide pass.

After freeze, write execution facts only to the declared evidence output outside the consumed input set. Any later consumed-input write invalidates the old claim; update the trace and revalidate the affected scope instead of retaining a stale pass. Keep one document and one verification result owner; summaries link their fact record rather than copying mutable counts.


For serialized acceptance, divide checks by invalidators rather than by ceremony. Phase A owns implementation behavior, package, contract and affected-runtime evidence. After the accepted switch, finish the final document/receipt update and freeze the active manifest's documents/dependencies/validators. Phase B owns only read-only freeze equality, accepted canonical/current tuple and task-sync projection, plus the exact receipt. Carry each Phase A result forward with its bounded scope/input and validator/tool digest; do not rerun it after a projection-only switch. Rerun only the result whose source, dependency, scope, authority, validator/tool, environment or required-check set changed. Unknown change, a missing/changed freeze or failed evidence blocks acceptance; it does not justify unrelated full-suite work.

When the orchestration result bus is active, closed verification producers publish newly executed accepted envelopes automatically; exact fully reused hits perform no persistent record. Compatible Skill packages, code-link documents and Runner Schema facts retain combined coverage, while changed/failed hashed identities invalidate only affected reusable facts. `operation-efficiency/v1` remains the four-count Runner projection, but exact reads are intentionally absent, so counts are lower-bound state-changing observations. Silent-hit rows suppress reuse-rate and narrow-scope/owner advice rather than drawing a false conclusion from incomplete reads. Counts never replace selected evidence, justify a missing check or establish Token savings. Do not rerun tests or audits for metric collection.

When verification fails:

- stop claiming completion and keep the same impact trace;
- classify product defect, test defect, environment/tool issue or stale impact assumption;
- recall matching verified error memory before repeating the route;
- update the same failure fingerprint when the root cause is unchanged;
- widen only when the failure establishes a new impact edge or another escalation trigger;
- use a verified Alternative Route or report the safe resume condition.

Do not delete, weaken or bypass a relevant test merely to obtain green output. Flakes require evidence of nondeterminism, a bounded rerun and a recorded owner; repeated blind reruns are not verification.

<a id="release-batch-receipt"></a>
### 受控发布批次回执

明确采用此合同的发布工具，每组件、每轮发布执行一次完整工具回归；同轮打包、预演、应用、工具同步和清理可以消费同一回执。最长有效期为12小时；新轮次、已关闭或失败批次必须重新执行。帮助与历史查询不触发完整回归；`--force-gate`强制重测。`--core-only`仅供只读隔离检查，不读取或写入完整回执，任何与`--apply`组合均拒绝。

回执绑定真实工作区、组件、候选来源及身份、相关源码/工具/测试集合与摘要、运行环境、通过用例数和有效期。使用共享锁防止并发重复建立完整结果。输入变化、缺失用例、失败、损坏或匹配不明均失效；不得通过减少用例、缩小输入集或导入未经证明的旧结果保留通过状态。回执留在项目忽略目录，其证据链接进入现有任务验证记录，不充当新业务验收账本。

版本分类和现场状态逐次独立核验。合法的产物分类登记只能通过拥有分类权的入口产生、绑定前后摘要的明确转换续接；不能简单排除分类目录表或接受任意漂移。历史摘要与运行时证明的边界由[发布登记与保留](../ops/rules.md#release-registry-and-retention)拥有。

测试夹具只可在自己的临时脚本中替换唯一门禁调用，必须断言恰好一次并验证没有递归完整套件输出；不能削弱正式入口。复用性能记录完整执行次数、回执读取耗时和绑定输入；工具回归通过不证明真实登录态、业务验收、服务器安装或应用上线。

## 7. Completion Standard

Record one `VerificationDecision` for Standard/Controlled work:

```text
route / changed surface / impact source and freshness / affected set / selected checks / skipped checks / escalation / outcome / owner / residual risk
```

A result is complete only when every material changed or propagated claim has evidence, expected and actual results match, partial/timeout/interrupted output cannot be mistaken for acceptance, skipped checks and residual risk are visible, affected documentation/maps are synchronized, and Root accepts the evidence.

Use `not run` or `unverified` precisely. Do not translate tool silence into success or estimate coverage, usage or savings that were not observed.

## 8. Specialist Routes

Codex runtime supervision tests, isolated Home smoke, Hook contracts, error reconciliation and PreTool Shadow behavior are owned by [runtime supervision](../codex-evolution/runtime-supervision/README.md) and its Skill. Work Unit/Runner Schema, Attempt, budgets and model-observation tests are owned by [orchestration](../codex-evolution/orchestration/README.md) and its Skill. Design-preference Gate order, candidate/conflict behavior and UI Skill preconditions are owned by [design preferences](../design-preferences/README.md).

Task verification links the applicable specialist result and affected boundary; it does not copy the specialist algorithm or automatically run the specialist's complete suite.

When PROJECT_STATUS carries the `project-status-link-only-v1` marker, the master audit applies 80-line / 480-char budgets and owner-body anti-copy; without that marker the live long status is not gated. Fixed-guard owners must stay unique, single-contract and ≤16 KiB (loading fail-closed). `kernel_load_epoch` is hashed from authority content and is never stored as a mutable snapshot.

## Operation Artifact Retention

For screenshots, downloaded/uploaded/generated files and structured test results, apply [operation artifact retention](operation-artifacts.md). Preserve the existing operation/verification owner and link its events to durable project-local artifacts before temporary files expire.

规则快速入口的 P0 失败传播、声明正文读取授权及最小正反例见[规则验证门禁与读取边界](rule-gate-boundaries.md)；该笔记为实现证据，不新增规范契约。

CodeNote 离线文档/表格fixture使用固定白名单模块及已安装运行时的真实pdf2image/pandas；仅对应两个测试可选择文档运行时，不安装或mock掉依赖。缺运行时/依赖、官方SDKfixture被skip均阻断，不能以离线逻辑通过关闭实际渲染、远端结构或宿主显示验收。可用性及显式覆盖行为由执行器正反例维护。
