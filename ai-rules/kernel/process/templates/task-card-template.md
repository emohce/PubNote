# Task Card

> Standard non-requirement work only. Standard requirement work uses `raw-requirement.md + spec.md` from the dedicated template.

Tool:
Date:
Task:

## Task Documentation Sync Group

- Group key: `dsg:<repository-key>:<work-unit-key>`
- Group owner: this `task-card.md`
- Git document prefixes:
- Durable document members, including clean consulted owners:
- Declared code/config dependencies:
- Linked current/canonical/rule/memory authorities:
- Excluded unrelated dirty documents:
- Lookup contract: follow [Task Documentation Sync Group](../rules.md#243-task-documentation-sync-group).
- In-progress archive: declare the group; the closeout executor owns checkpoint.
- Active-group lifecycle: one active manifest; a new Work Unit replaces key/members in place.
- Shared-file stage ownership: membership is not hunk ownership; record any patch-stage boundary.

```json documentation-sync-group-v1
{
  "schema": "documentation-sync-group-v1",
  "group_key": "dsg:<repository-key>:<work-unit-key>",
  "group_owner": "<repository-relative-path>/task-card.md",
  "documents": ["<repository-relative-document>"],
  "dependencies": ["<repository-relative-code-or-config>"],
  "validators": ["<repository-relative-validator>"],
  "git_scope_prefixes": ["<repository-relative-document-root>"]
}
```

## Goal And Scope

- For existing-behavior changes, record the [BusinessChangeReview](../../engineering/rules.md#business-change-protection) here and reuse it in verification; omit for behavior-neutral work.
- Goal:
- In scope:
- Out of scope:
- Success evidence:

## Decision

- Documentation level: `standard`
- Execution: `main-only | native-agents`
- Automation lane: `not-applicable | explicit-cli`
- Key decision and reason:
- High-risk / DB boundary:
- Plan-mode preflight completed before first edit: `yes/no`
- Plan artifact scope and documentation impact: `none-with-reason | task-only | project-current | requirement-canonical | global-rule | template-propagation`
- Verification map: `<owner/row + freshness> | absent — dynamic analysis`
- Provisional `VerificationImpactTrace` completed before verification commands: `yes | no — rework`
- Verification-command provenance: `impact-trace | independent-user-request | release-policy | incoming-plan-reconciled`
- Test additions/execution: impact-selected only; no separate user enumeration required

## Prior Task Overlap

Use when the work is similar, repeated, resumed or recovery-sensitive; otherwise write `none`.

- Relationship: `none | reference-only | partial-overlap | continuation | supersedes`
- Prior authority and verified state:
- Document governance:
- Execution logic verification / residual gates:
- Traceability and decision: `reuse | delta-only | no-op | supersede | new-task`

## Documentation Realization

Use for a durable runtime/rule correction; otherwise write `not applicable`.

- Task and mechanism design authority:
- Requirement evolution / canonical merge authority:
- Intermediate problem / verified alternative / verification authority:
- Semantic execution account and unavailable-information boundary:

## Optimization And Template Propagation

- Optimization promotion: `not-applicable | current-task | deferred-parent-task`
- Applied project/template impact: `none | roots listed below`
- Parent task / excluded roots:

## Rule Task Trace

Use only when this task is an admitted global/shared/cross-project/template parent or implements one. Project-local changes stay in project authorities; Quick project-local maintenance has no Task Card and no central registry row.

- Registry scope: `global | shared | cross-project | template-propagation | project-local / not-admitted`
- Registry identity / row:
- Requirement and implementation authority:
- Propagation / delegation / Root acceptance:

## Work And Verification

- Changed surface:
- Verification:
- Unverified gaps:
- Delegated read-only result and Root decision, if any:

### Verification Decision

- Route: `live-ui | static | sql-static-handoff | focused-automated | user-owned | not-required`
- Reason:
- Impact source and freshness:
- Plan verification clauses reconciled before execution: `yes | no — rework | not-applicable`
- Affected modules / boundaries:
- Checked:
- Skipped:
- Full-suite escalation: `none | <trigger + wider check + decision value>`
- Owner:
- Residual risk:

### Verification Impact Trace

| Changed surface / claim | Direct consumers | Material transitive or failure boundary | Selected evidence | Skipped suites / reason | Outcome / residual |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |

## Authority Packet And Documentation Impact

- Authority refs read:
- Decisive source evidence:
- `doc_drift`: `none | resolved | retained-gap`
- Document impact: `none-with-reason | task-only | project-current | requirement-canonical | global-rule | template-propagation`
- Synchronized authorities and verification:
- Root acceptance gate: `accepted | pending-doc-sync | rework | unverified`

## Execution Journal

Use `none` when no material event occurred. Do not reconstruct routine reads or tool calls.

| Event ID | Local Time | Work Unit / Attempt | Actor / Surface | Event | Prior -> Resulting State | Trigger / Evidence | Root Decision / Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- |
| none |  |  |  |  |  |  |  |

## Efficiency / Token Evidence

Use only when delegation, interruption, fallback, or an optimization materially affected execution. Unknown runtime usage is `usage unavailable`.

| Metric | Baseline | Observed | Delta | Confidence / Source |
| --- | --- | --- | --- | --- |
| not applicable |  |  |  |  |

## TaskExperienceObservation

Optional for a material Standard-task experience/evolution signal; Quick does not create this section. Record only the closed evaluator result or `not applicable`. `null` remains unavailable and no Token saving is inferred.

- Result: `not applicable | task-owner-optional | none-no-material-signal`
- Control score / observed dimensions:
- Failed / unavailable dimensions:
- Promotion decision: `observe | show-evolution-preview | versioned-change-review | not applicable`

## Implementation Sync

- Authoritative current behavior:
- Module / document mapping:
- Evidence or `not applicable`:

## Closeout

- Sidecar: `main-thread | Start Explorer + Closeout Reviewer | not applicable`
- Requirement / business / tech route:
- Memory / error route:
- Evolution Candidate:
