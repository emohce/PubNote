# Testing And Verification Rules

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
6. user-owned acceptance for subjective UI/product judgment or externally controlled systems.

## 2. Change And Impact Analysis

Start from the intended behavior delta plus the current Git change set, including task-owned untracked files. Resolve impact through concrete edges: imports/exports and callers, package dependencies, public API/schema/config contracts, routes/events/jobs, storage or permission boundaries, generated artifacts, build graph, host integration and known failure paths. A changed-file list by itself is not an impact analysis.

### 2.1 Project Verification Map

A project may predeclare a reusable `ProjectVerificationMap` in its existing architecture, knowledge or rule owner and link it from the project entry. Do not create a new map for one isolated change when dynamic analysis is cheaper. Each maintained row records:

```text
surface selector / behavior or contract / direct consumers / transitive boundaries / focused checks / escalation triggers / owner / last verified
```

Use the map only after checking that its selectors, commands, package graph and owner are current. A missing or stale map is not a reason for full-suite testing; reconstruct only the current task's impact graph from targeted source, manifest, build and test evidence. When implementation reveals a stable missing edge that will be reused, update the existing map after the code change and link the evidence. Do not duplicate the same mapping in every task.

### 2.2 Verification Impact Trace

Quick work keeps a compact `VerificationImpactTrace` in the final response. Standard work records it in the Task Card or requirement Spec; Controlled work records the provisional selection in the Plan and the final trace in `verify.md`.

| Field | Required content |
| --- | --- |
| Changed surface | Task-owned code/config/docs and the behavior or contract changed |
| Impact evidence | Map row or targeted dependency/caller/schema/build/runtime evidence |
| Affected set | Direct consumers plus material transitive and failure-path boundaries |
| Selected checks | The smallest checks covering every material claim |
| Skipped checks | Named broader suites/boundaries, exclusion reason and residual risk |
| Escalation | Trigger, wider check and decision it would change; otherwise `none` |
| Outcome | Actual result, unverified gap and evidence owner |

Create the provisional trace before material implementation when the impact is already knowable. Verification commands are outputs of that trace, not inputs to it: before an Agent-authored or Agent-expanded plan names a command or suite, record the provisional changed surface, affected set, selected checks, skipped checks and escalation state. Reconcile an incoming plan's verification clauses against this owner before accepting or executing the plan, then reconcile the trace against the actual diff afterward. A newly discovered consumer updates the same trace and, when reusable, the project map; it does not silently widen into an unrecorded full gate.

<a id="requirement-owned-test-expectations"></a>
## 2.3 Requirement-Owned Test Expectations

For changes affecting established behavior, consume the [BusinessChangeReview](../engineering/rules.md#business-change-protection). Accepted requirements determine expected results; tests and implementation must not validate each other's unsupported assumptions. Keep the existing minimum-sufficient selection and full-suite escalation rules.

Keep stable requirement IDs/source links and existing business guards in the project's current verification map when it has one; otherwise record only the affected mapping in the task. Do not create a parallel requirement registry or silently assign accepted status to unregistered source fragments.

- Before editing a business expectation, inspect the previous assertion/fixture and its accepted requirement or decision. Classify the test delta as **add**, **equivalent-refactor**, **correct-wrong-expectation**, **authorized-behavior-change**, or **coverage-reduction**. Record before/after semantics, source authority and replacement coverage in the existing review. Unchanged tests need no per-test ledger.
- Preserve independent regression evidence for each affected invariant. Use a relevant existing guard, or derive a missing guard from accepted sources before accepting the new implementation. For a regression repair, show the guard rejects the known bad behavior and accepts the fix when a bounded replay is practical; otherwise state the evidence limit. Do not manufacture tests for behavior-neutral, low-impact edits.
- Deleting/skipping an assertion, weakening a predicate, widening a tolerance, reducing fixtures, changing snapshots or mocking away a business owner is a potential **coverage-reduction**, even when the suite becomes green. It needs either equivalent/stronger coverage of the same obligation or an explicit requirement decision retiring that obligation. A test rename or higher passing count is not replacement evidence.
- **correct-wrong-expectation** is valid only when accepted source evidence proves the old expectation wrong; code convenience, a new implementation, a green suite or an Agent-authored plan is not that evidence. **authorized-behavior-change** binds the current explicit decision or scoped supersession; do not ask again for an already granted change or preserve superseded business behavior as current.
- Separate delta checks from preservation checks. Shared decision logic requires affected consumer-path evidence (for example click → shortcut, or provider → reducer → view), including relevant sequence/concurrency/failure boundaries; pure selector assertions alone do not prove downstream consumers retained that selector's decision.
- Before closeout, inspect the final test diff for lost coverage and bind the reported checks to the tested source state. Later relevant code/config/test changes invalidate only their affected evidence. Do not increase unrelated test scope to compensate for a missing business oracle. Unresolved expectation authority or lost required coverage leaves the affected claim **unverified**.

## 3. Selecting The Affected Checks

For every material acceptance claim, select at least one check able to fail when that claim is false. Deduplicate checks when one command demonstrably covers another; for example, a build satisfies semantic typecheck only when its output proves that configured typecheck ran.

| Changed surface | Minimum candidate evidence | Add only when impacted |
| --- | --- | --- |
| Leaf/domain logic | Closest unit/contract tests and local static checks | Direct caller or failure-path tests when the contract crosses the leaf boundary |
| Shared/public API or library | Changed contract tests plus affected direct-consumer compile/tests | Transitive package checks only for consumers reached by the dependency graph |
| Frontend/UI/runtime source | Focused component/state tests and affected-package semantic typecheck | Build when bundle/output/config/entrypoint behavior changed; runtime/visual/interaction evidence only for affected states. If the write set is a review-document or position-navigation surface, add [named UI preference checks](../scripts/check_named_ui_preferences.py#L1) (`PNP-*` / `RDA-*`) plus A-class runtime probes; do not copy those owner algorithms here |
| Backend/service/shared logic | Focused module/service tests and affected-target type/compile evidence | Integration smoke only for a touched boundary that static evidence cannot prove; do not launch a service merely to compile |
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
