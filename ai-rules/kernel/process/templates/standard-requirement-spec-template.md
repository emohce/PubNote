# Standard Requirement Spec: <task>

关键词：需求增量、实施选择、验收条件、来源追溯

正式文档按[关键词通则](../rules.md#document-keywords)从本篇正文重新提取；拆成多篇时各篇自有摘要。

> Legacy layout remains supported. New role-based tasks use [task-roles-template](task-roles-template.md); declared role mappings take precedence over filename/count guidance in this template.
Tool: <tool-name>
Date: YYYY-MM-DD
Status: `draft | needs-confirmation | confirmed | integrated | closed-no-change | superseded`（取值由[需求状态 owner](../requirement-versioning.md#5-spec-delta-contract)维护；历史 rework 记录不批量改写）
Documentation level: `standard requirement`

Raw source: `raw-requirement.md`
Canonical target: `<project Requirement Manifest / canonical member>`

> This `spec.md` is the single Standard requirement process owner. Do not add a Task Card or reuse the Controlled Spec template unless risk promotes the task to Controlled.

## Task Documentation Sync Group

- Group key: `dsg:<repository-key>:<work-unit-key>`
- Group owner: this `spec.md`
- Git document prefixes:
- Durable document members, including raw/canonical and clean consulted owners:
- Declared code/config dependencies:
- Linked current/rule/memory authorities:
- Excluded unrelated dirty documents:
- Lookup contract: follow [Task Documentation Sync Group](../rules.md#243-task-documentation-sync-group).
- In-progress archive: declare the group; the closeout executor owns checkpoint.
- Active-group lifecycle: one active manifest; a new Work Unit replaces key/members in place.
- Shared-file stage ownership: membership is not hunk ownership; record any patch-stage boundary.

```json documentation-sync-group-v1
{
  "schema": "documentation-sync-group-v1",
  "group_key": "dsg:<repository-key>:<work-unit-key>",
  "group_owner": "<repository-relative-path>/spec.md",
  "documents": ["<repository-relative-document>"],
  "dependencies": ["<repository-relative-code-or-config>"],
  "validators": ["<repository-relative-validator>"],
  "git_scope_prefixes": ["<repository-relative-document-root>"]
}
```

## Requirement Delta

- Add / modify / remove / clarify:
- Confirmed facts:
- Pending decisions:
- Acceptance criteria:

## Requirement Change Review

- For existing-behavior changes, include the [BusinessChangeReview](../../engineering/rules.md#business-change-protection) and reuse its invariant/evidence mapping in VerificationImpactTrace.
- Scan scope / owners: current request → active raw/Spec → affected canonical → direct decision/status/pending owners → affected derived/design/current-logic → shared contracts when crossed.
- Visible changes: added / changed / removed / superseded.
- Conflict classification: `no-conflict | compatible-update | supersede | remove | direct-conflict | ambiguous-impact`.
- Conflict evidence and affected owners:
- Decision status: `explicit-current-request | selected-option | pending`.
- Decision source / selected branch:
- User-facing review shown:
- Post-sync rescan: `pass | unresolved`; unresolved keeps canonical unchanged and blocks `integrated`.

## Prior Task Overlap

- Relationship: `none | reference-only | partial-overlap | continuation | supersedes`
- Document governance:
- Execution logic verification:
- Traceability and decision: `reuse | delta-only | no-op | supersede | new-task`

## Canonical Merge

- Base project version:
- Result project version:
- Target sections and backlinks:
- Merge status / missing target:

The Spec cannot be `integrated` until every confirmed canonical target and backlink is synchronized.

The Spec also cannot be `integrated` until the Requirement Change Review is visible, its user decision is resolved, and the post-sync bounded rescan has no material conflict.

When the project declares `serialized-acceptance-v1`, keep canonical at the base version through implementing/verifying, record switch-ready after the full pre-switch gate, switch every canonical/current projection together, and require a fresh exact receipt before `integrated`.

## Implementation Sync

- Changed logic / desired behavior:
- Authoritative current document:
- Entry-to-module/storage/integration mapping:
- Verification evidence:
- Gap / follow-up / not applicable:

## Verification

### Verification Decision

- Route: `live-ui | static | sql-static-handoff | focused-automated | user-owned | not-required`
- Reason:
- Impact source and freshness:
- Provisional trace completed before verification commands: `yes | no — rework`
- Verification-command provenance: `impact-trace | independent-user-request | release-policy | incoming-plan-reconciled`
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

| Check | Evidence | Result | Remaining Manual Path |
| --- | --- | --- | --- |
| requirement/raw/canonical parity | <link or command> | pass/fail/unverified | none / <owner> |

## Documentation Impact

- Classification: `none-with-reason | task-only | project-current | requirement-canonical | global-rule | template-propagation`
- Central Rule Task admission: `global | shared | cross-project | template-propagation | project-local / no central row`
- Parent identity or local parent backlink:
- `doc_drift`:
- Affected authoritative documents:
- Root acceptance gate:

## Execution Journal

Record only material steering, correction, failure/fallback, verification or acceptance events. Write `none` when no material event occurred.

| Event | Trigger / Evidence | State Change | Root Decision |
| --- | --- | --- | --- |
| none | routine work omitted | none | none |

## Efficiency / Token Evidence

Optional unless delegation, fallback, interruption or governance optimization materially changed execution.

- Baseline / observed / delta:
- Confidence / source:
- Usage: `usage unavailable | <observed counter>`

## Closeout

- Requirement Manifest / project version:
- Canonical merge:
- Verification:
- Documentation and memory/error routing:
- Open gate / owner:
