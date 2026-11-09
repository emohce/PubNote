# VibeAi Checklist

- [ ] Existing-behavior changes carry the [BusinessChangeReview](engineering/rules.md#business-change-protection); verify both the authorized delta and preserved invariants, including the authority for changed test expectations.

> Non-normative operational instrument. Check only applicable rows; linked sole owners define behavior. Do not copy this checklist into adapters or task documents.

## Before Work

- [ ] Classify request mode, evidence state, risk and freshness through the [Task Outcome And Evidence Stop owner](process/task-outcome-and-evidence-stop.md).
- [ ] Load the global/project entries and smallest routed owners; for multi-domain ambiguity or a high-risk guard, use the bounded route CLI described by `task-skill-reminder`.
- [ ] Similar/repeated/resumed/recovery-sensitive work completes [Prior Task Overlap](process/prior-task-overlap.md): `document governance`, `verified execution state/logic`, `traceability`, and reuse/net-delta/no-op/supersede/new-task decision.
- [ ] Select Quick, Standard or Controlled at the [process owner](process/rules.md); Standard non-requirement uses `task-card.md`, Standard requirement uses raw+Spec, and Controlled uses its synchronized ledger.
- [ ] Run the Task Overview Sidecar/Start Explorer gate only when applicable; use Closeout Reviewer only when it adds independent value, otherwise record main-thread fallback.
- [ ] Announce the smallest Skill set and verification level; compose selected Skills as one operation-owner DAG with one executor per material operation and reuse valid delegated results. On a controller-scoped Codex path, consume the automatic result-bus snapshot instead of forwarding envelope files; never treat aggregate counters as correctness or permission. UI work completes preference lookup before UI Skill/design/code.
- [ ] Record each Evolution Candidate as none or source/impact/scope/target/privacy; no consent means no promotion.
- [ ] Identify high-risk gates, exact targets, worktree state, rollback and external-source needs before action.

## Execution And Ownership

- [ ] `App Root` is the interactive controller. `CLI execution` is limited to explicit automation/CI/scheduled/headless/batch work; child/tool output stays `reported` until Root verifies it.
- [ ] Delegated Work Units have unique identity, bounded scope/attempts, mutually safe write sets, verification and fallback; recursion is prohibited beyond configured depth.
- [ ] Repository work starts with a minimal `Authority Packet`; decisive claims still use focused source/test/runtime evidence.
- [ ] Preserve unrelated dirty work and make the smallest complete change. Never use a broader tool, permission or refactor merely for convenience.
- [ ] Before undoing a commit, classify remote-ref containment: explicit correction of local-only current-task history uses verified safety refs plus amend/rebase/soft rebuild; pushed/shared history defaults to revert, and remote rewrite needs fresh force-push authority.
- [ ] `Rule Task Trace`: only global/shared/cross-project/template parents enter the `central registry`; `project-local` work stays in project authority. Reuse `one parent task` and freeze each `active Worktree` only during authorized propagation.
- [ ] Quick has no journal. Standard uses its owner; Controlled keeps material-only `Execution Journal` events, excluding raw prompts, routine tool output and child transcripts.
- [ ] Repeated failures reuse one `failure_key` and only a verified `Alternative Route` may guide automatic recovery. Store `Efficiency / Token Evidence` only when comparable; otherwise record `usage unavailable`.

## Verification

- [ ] Build a provisional `VerificationImpactTrace` through [testing](testing/rules.md) before verification commands enter an Agent-authored or Agent-expanded plan: changed contract, direct/transitive impact, selected checks (the [round pending-test list](testing/rules.md#round-pending-test-list), including matching map rows or reconstructed live consumers), skipped suites, escalation and residual risk. A missing project map does not skip consumer preservation.
- [ ] Run only impact-selected semantic tests/type/compile/build. A full suite needs a recorded escalation trigger; approval of a suite first inserted by an Agent-authored plan is not an independent user request, and apps/services/watchers are not launched merely to obtain evidence.
- [ ] UI changes inspect a real runtime screenshot when runtime acceptance is required; build/DOM metrics are supporting evidence only.
- [ ] SQL stays read-only. Mutation stays with the user or DBA. Executable DDL is a task `.sql` with `-- <++>` segments; `sql.md` records status and results.
- [ ] Security/tool/memory/orchestration/provider changes run the behavioral agent-security replay and prove no unauthorized write/tool/escalation plus bounded recursion/cost.
- [ ] Rule/Skill changes verify affected owner/link/route/replay behavior and each changed Skill package; widen to registry/tree/manifest audits only when identity, ownership, discovery, publication or generated inventory changed.
- [ ] Document moves verify the replacement owner and every tracked inbound link in working/index/HEAD views before archive acceptance.
- [ ] Close `Documentation Impact`: `document_impact` is classified, `doc_drift` resolved or retained explicitly, and pending authority sync blocks acceptance.
- [ ] `Documentation Realization` links `task/mechanism design`, `requirement evolution`, and each `intermediate problem`/Alternative Route to current verification without creating a raw log.
- [ ] Root reconciles every `reported` result, interruption, partial worktree effect and skipped check before accepted/rework/rejected/superseded.

## Delivery

- [ ] Lead with outcome; group decisive evidence; state failed/skipped/unverified gates, compatibility and residual risk.
- [ ] Report changed owners, verification, documentation/memory/Evolution Candidate routing and archive actions.
- [ ] Give `0–3` useful actions only when needed; numeric selection is limited to mutually exclusive branches and never bypasses a permanent confirmation gate.
- [ ] A Stop-Hook advisory is non-blocking and contains `decision_route`, `interruption_reason`, recovery and impact without displacing the primary response.
- [ ] If `codex-evolution-supervisor` changed, verify `blocked_dirty`, `/hooks` trust, sanitized receipts, `cross-turn backlog dedupe` and the non-blocking `Stop-Hook advisory`.
