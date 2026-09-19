# Verify Template

Tool:
Date:
Task:

Documentation level: `controlled`

## Commands

-

## Results

-

## Verification Decision

- Route: `live-ui | static | sql-static-handoff | focused-automated | user-owned | not-required`
- Reason:
- Impact source and freshness:
- Provisional trace preceded plan verification commands; command provenance/reconciliation:
- Affected modules / boundaries:
- Checked:
- Skipped:
- Full-suite escalation: `none | <trigger + wider check + decision value>`
- Owner:
- Residual risk:

## Verification Impact Trace

| Changed surface / claim | Direct consumers | Material transitive or failure boundary | Selected evidence | Skipped suites / reason | Outcome / residual |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

## Requirement Integration

Use only for requirement-bearing work.

- Raw/Spec/canonical backlinks:
- Project requirement version:
- Spec revision/status:
- Pending item stayed out of canonical:
- All canonical targets synchronized:
- Actual/mock/planned evidence label:

For a serialized canonical switch, record the exact switch-ready identity only after every pre-switch check passes while the base canonical remains current. After switching, rerun decisive checks and require a fresh exact documentation receipt before `accepted`.

```text
<!-- codex-switch-ready: RAW-.../rev.../WO.../W.../R... -->
```

## Requirement Change Review Verification

- Reconcile the [BusinessChangeReview](../../engineering/rules.md#business-change-protection) with the final production/test diff: each preserved invariant has evidence, and changed expectations have requirement authority or equivalent coverage.
Use only for requirement-bearing work.

- Bounded owner scan completed:
- Added / changed / removed / superseded facts visibly presented:
- Conflict classification and affected owners verified:
- Decision status / decision source: `explicit-current-request | selected-option | pending`.
- Pending alternative stayed out of canonical/current/design/rule accepted projections:
- Post-sync rescan: `pass | unresolved`.
- Result: unresolved conflict or missing user decision blocks `integrated` / `accepted`.

## Prior Task Overlap Verification

- Relationship: `none | reference-only | partial-overlap | continuation | supersedes`
- Document governance verified:
- Prior execution state/logic and residual gates verified:
- Traceability / reused evidence / net-new delta:
- Decision: `reuse | delta-only | no-op | supersede | new-task`

## Documentation Realization Verification

| Lane | Authority / Link | Required Evidence Present | Result |
| --- | --- | --- | --- |
| Task and mechanism design |  |  | `not-applicable | pass | fail` |
| Requirement evolution |  |  | `not-applicable | pass | fail` |
| Intermediate problems |  |  | `not-applicable | pass | fail` |

- Semantic execution account: highest goal, per-item status, decisive evidence, Hook route, interruption/impact/recovery and unavailable-information boundary present or `not applicable`.

## Execution Audit

| Work Unit | Attempt | Surface | Requested Profile | Observed Model | Exit / Thread Result | Changed Files / Output | Scope Check | Local Verification | Main Decision |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |  |  | `unverified` |

`Main Decision`: `accepted | rework | rejected | superseded | unverified`.

## Documentation Impact Verification

| Work Unit | Authority Refs Read | Source Evidence | `doc_drift` | Final Document Impact | Synchronized Authorities | Root Decision |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  | `none | resolved | retained-gap` | `none-with-reason | task-only | project-current | requirement-canonical | global-rule | template-propagation` |  | `unverified` |

A behavior-changing Work Unit cannot be `accepted` while an affected authority is unsynchronized. Use `none-with-reason` only when no durable documentation change is justified.

## Efficiency / Token Evidence

Use for material delegation, interruption, fallback, or governance optimization. Compare only equivalent scope and acceptance criteria; use `usage unavailable` for unexposed counters and do not rerun solely for measurement.

| Metric | Baseline | Observed | Delta | Confidence / Source |
| --- | --- | --- | --- | --- |
| Token usage |  | `usage unavailable` | unavailable | runtime counter only |
| Attempts / rework |  |  |  | Work Unit ledger |
| Elapsed / critical path |  |  |  | material event timestamps |

## TaskExperienceObservation

Use only when the Controlled task has a material task-experience/evolution signal. Verify the closed evaluator input source, unavailable dimensions and no-write/no-Token-claim flags; otherwise record `not applicable`.

| Control Score | Observed / Total | Failed Dimensions | Unavailable Dimensions | Persistence Recommendation | Promotion Decision |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  | `observe | show-evolution-preview | versioned-change-review | not applicable` |

## Template Propagation Audit

Before release gates pass, master-only is allowed only as an explicit `rollout-pending` candidate with no downstream writes. After propagation starts, every frozen root needs one row; master-only success or incomplete downstream acceptance cannot be called rollout complete.

| ID | Repository / Worktree | Adapter | Rules | Documentation | Status Hub | Local Constraints Preserved | Root Decision |
| --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  | `unverified` |

## Rule Task Trace

- Admission: `global | shared | cross-project | template-propagation | project-local / no central row`
- Registry identity / row:
- Requirement, implementation and verification backlinks:
- Target-project parent backlink / local result / residual gate:
- Delegation / propagation / error-memory state synchronized:
- Root acceptance: `accepted | rollout-pending | rework | rejected | superseded`

## Sidecar Result

| Field | Result |
| --- | --- |
| `Start Explorer` |  |
| `Closeout Reviewer` |  |
| `missing_required_updates` |  |
| `optional_improvements` |  |
| `memory_routing_decision` |  |
| `risk_gates` |  |
| `verification_required` |  |
| `evolution_candidates` |  |

## Evolution Candidate

| Evidence | Candidate | Target | Promotion Condition | Risk | Decision |
| --- | --- | --- | --- | --- | --- |
| none | none | no update | not applicable | none | no update |

## Gaps

-

## Memory Decision

-

## Rule Declaration

- Global entry:
- Project entry:
- Sidecar:
- Document routing:
- High-risk gate:
