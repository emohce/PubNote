# Controlled Spec Template

> Use only with the Controlled five-file ledger. Standard requirement work uses [standard-requirement-spec-template.md](standard-requirement-spec-template.md).

Tool:
Date:
Task:

Documentation level: `controlled`

## Task Documentation Sync Group

- Group key: `dsg:<repository-key>:<work-unit-key>`
- Group owner: this `spec.md`
- Task-root discovery prefix for the five-file ledger:
- Durable document members, including clean external authorities:
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
  "group_owner": "<repository-relative-path>/spec.md",
  "documents": ["<repository-relative-document>"],
  "dependencies": ["<repository-relative-code-or-config>"],
  "validators": ["<repository-relative-validator>"],
  "git_scope_prefixes": ["<repository-relative-document-root>"]
}
```

## Requirement

-

## Success Criteria

- Existing-behavior changes use the [BusinessChangeReview](../../engineering/rules.md#business-change-protection); preserve sourced invariants outside the authorized delta and review changed test expectations.
-

## Constraints

-

## Prior Task Overlap

Use when the requirement is similar, repeated, resumed or recovery-sensitive; otherwise write `none`.

- Relationship: `none | reference-only | partial-overlap | continuation | supersedes`
- Prior authority and verified state:
- Document governance:
- Execution logic verification / residual gates:
- Traceability and net-new delta:

## Requirement Versioning

Use only for requirement-bearing work; otherwise write `not applicable`.

```yaml
spec_id:
spec_revision:
status: draft | needs-confirmation | confirmed |
        integrated | closed-no-change | superseded
active_version_protocol: serialized-acceptance-v1 # optional; required only for a declared serialized switch
execution_reservation: WO<n>/W<n> # optional; exact adjacent execution pair explicitly allocated before the semantic pair
raw_sources: []
targets:
  - canonical_manifest:
    base_full_version:
    result_full_version:
delta:
  - requirement_id:
    operation: add | modify | remove | clarify
    before:
    after:
    raw_refs: []
    confirmation: explicit | unambiguous | pending
    canonical_location:
memory_used: []
memory_updates: []
open_questions: []
```

For `serialized-acceptance-v1`, add one `rule-kernel-current-state-v1`-style closed state block owned by this Spec, keep canonical at the base version through target/verifying, record switch-ready in verification, then switch all projections and issue a fresh exact receipt before acceptance.

- Raw requirement:
- Canonical Manifest / affected members:
- Merge status / missing target:
- Actual surface: `actual | mock | planned | not available`
- Requirement-runtime gap:

## Requirement Change Review

Use for requirement-bearing work; otherwise write `not applicable`.

- Bounded scan scope / owners:
- Visible added / changed / removed / superseded facts:
- Classification: `no-conflict | compatible-update | supersede | remove | direct-conflict | ambiguous-impact`.
- Conflict evidence and affected owners:
- Decision status: `explicit-current-request | selected-option | pending`.
- Decision source / selected branch:
- User-facing review shown:
- Post-sync rescan: `pass | unresolved`; unresolved keeps accepted projections unchanged and blocks `integrated` / `accepted`.

## Execution Authority

- Control plane: `app-root`
- Sole decision owner: App Root Thread
- Allowed interactive execution surfaces: `main`, `native-thread`
- Automation lane: `not-applicable | explicit-cli`
- Surface-to-surface delegation: forbidden
- Main-owned decisions: scope, user communication, risk approval, reconciliation, final acceptance
- Documentation synchronization owner: App Root Thread
- Acceptance gate: affected authoritative documents synchronized and verified

## Execution Constraints

- Write isolation:
- High-risk gates:
- DB/SQL boundary:
- Fallback:

## Evidence

-

## TaskExperienceObservation

Optional for a material Standard requirement-task experience/evolution signal. Keep only the closed task-local evaluator result; no raw interaction content or inferred Token saving.

- Result / coverage:
- Failed / unavailable dimensions:
- Persistence or promotion route:
