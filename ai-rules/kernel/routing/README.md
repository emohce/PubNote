# Rule Kernel Router

<!-- rule-contracts: rule-routing -->

Hosts: any

## Shared Always-Load Baseline

|load_id|contract_id|load_type|source|scope|
|---|---|---|---|---|
|routing-authority|rule-routing|always-once|this router|task|
|global-baseline|rule-priority-hot-route|always-once|[VibeAi](../VibeAi.md)|task|
|project-entry|project-entry-loading|always-once|project entry / not-applicable|project or `not-applicable`|

## Host-Agnostic Auto-Load Paradigm

First read [catalog](catalog.md)/matches; reselect changed triggers, reuse unchanged reads. Pointers ≠ reads. Enabled [telemetry](../skills/rules.md#invocation-observations): shared producer, ancillary failure, no host claim.

## Fixed Guards

Read [reply](../process/communication-primary-response.md) and [title](../adapters/session-title.md); [registry](../README.md#contract-ownership-registry): sole_owner.

|contract_id|activation|trigger_ids|
|---|---|---|
|prior-task-overlap|context|continuation,repeated-failure,overlap-check|
|sidecar|context|orchestration,cross-project|
|documentation-impact|context|rule-change,cross-project,document-sync|
| `communication-primary-response` | always-once | - |
|task-outcome-and-evidence-stop|context|scope-conflict,acceptance-conflict|
|stable-developer-taste|context|architecture,ui,design,performance|
|intent-note-overlay|project-marker|intent-note-gate:enabled|
| `session-title` | always-once | - |
|task-skill-reminder|context|skill-list-request|

## Guard Delivery

Carriers select by semantics; context IDs only transport. Enabled Intent Notes load owner for `intent-note-command`/matched `intent-note-active`; enabling creates nothing.

## Deterministic Resolution

[Catalog](catalog.md).

## Persistence Boundary

No prompts/secrets. Budget: [limits](context-budget.md); keep semantics, report excess.
