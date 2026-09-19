# Plan Template

Tool:
Date:
Task:

Documentation level: `controlled`

## Plan-Mode Gate

- Before existing-behavior edits, bind the [BusinessChangeReview](../../engineering/rules.md#business-change-protection): accepted baseline, allowed delta and preserved invariants; reuse the task/Spec record.
- Plan level: `quick | standard | controlled`
- Task artifact for this run:
- Plan packet before first edit complete: `no | yes`
- Prior-task overlap decision:
- Documentation impact: `none-with-reason | task-only | project-current | requirement-canonical | global-rule | template-propagation`
- Required owners for first sync:
- Verification map: `<owner/row + freshness> | absent — dynamic analysis`
- Provisional `VerificationImpactTrace` completed before verification commands: `no | yes`
- Provisional changed/affected surfaces:
- Selected focused checks:
- Verification-command provenance: `impact-trace | independent-user-request | release-policy | incoming-plan-reconciled`
- Full-suite escalation trigger: `none | <trigger + wider check + decision value>`

An Agent-authored or Agent-expanded plan cannot create its own full-suite trigger. Approval, continuation or implementation of that plan does not become an independent user request; revise conflicting verification clauses before implementation.

## Summary

-

## Delegation Decision

- Interactive strategy: `main-only | native-agents`
- Automation lane: `not-applicable | explicit-cli`
- Reason:
- Root-owned decisions:
- Duplicate guard:
- Expected observable delegation benefit and metric:

## Execution Topology

| Work Unit | Owner | Surface | Agent/Profile | Mode | Depends On | Allowed / Excluded Scope | Output Contract | Verification Owner | Fallback |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  | app-root |  |  |  |  |  |  | app-root |  |

## Authority Packet And Documentation Impact

Use for repository-reading or implementation Work Units; otherwise write `not applicable`. Link, do not copy, the smallest relevant authorities.

| Work Unit | Authority Refs | Known Constraints | Question / Delta | Required Source Evidence | Provisional Document Impact |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  | `none-with-reason | task-only | project-current | requirement-canonical | global-rule | template-propagation` |

## Applied Project Matrix

Use only after any declared shadow/canary release gate passes and propagation is authorized. Before that, record `rollout-pending` without freezing or editing downstream roots. During propagation, seed discovery with the canonical project resolver's `--inventory --include-worktrees`, filter by governance, actual adoption, task scope and exclusions, then freeze the selected repository/Worktree inventory here. The index is not blanket propagation permission; never hard-code a permanent machine list in global rules.

| ID | Repository / Worktree | Adapter And Rule Surfaces | Baseline State | Local Mapping | Status | Exclusion Reason |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  | pending | not applicable |

## Changes

-

## Rule Application

- Global entry:
- Project entry:
- Requirement Manifest / active Spec:
- Requirement Change Review owner / scan scope / decision status:
- Required process docs:
- Process hub impact:
- DB boundary:
- Verification gates and `VerificationImpactTrace` owner:
- Plan verification-clause reconciliation and command provenance:
- Rule Task Trace admission (`global | shared | cross-project | template-propagation | project-local`) and parent identity/backlink:

## Knowledge Reconnaissance

- Project rules:
- Process hub:
- Neighboring task docs:
- Prior Task Overlap: relationship, document governance, execution logic/state verification, traceability and `reuse | delta-only | no-op | supersede | new-task` decision
- Current sync docs:
- Technical details / developer soul / error memory:

## Documentation Realization

Use for a durable runtime/rule correction; otherwise write `not applicable`. Reuse existing authorities rather than creating a raw operation log.

| Lane | Authority / Link | Required Evidence | Acceptance |
| --- | --- | --- | --- |
| Task and mechanism design |  | trigger/control flow, ownership, boundary and intended behavior | `pending` |
| Requirement evolution |  | raw/normalized delta, visible conflict scan, user decision, Spec revision and canonical merge | `pending` |
| Intermediate problems |  | symptom, failed route, root cause, verified alternative and verification | `pending` |

## Sidecar Strategy

- Start Explorer:
- Closeout Reviewer:
- Fallback:

## Evolution Candidate

| Evidence | Candidate | Target | Promotion Condition | Risk | Decision |
| --- | --- | --- | --- | --- | --- |
| none | none | no update | not applicable | none | no update |

## Memory Routing

- Requirement update:
- Business-logic update:
- Tech-stack update:
- Error record:
- DB/SQL:
- Project/global rule or soul:

## Risks

-

## Verification

- Source evidence and any `doc_drift`:
- Final document impact and synchronization owner:
