# Rule Kernel Router

<!-- rule-contracts: rule-routing -->

Hosts: any

## Shared Always-Load Baseline

| load_id | contract_id | load_type | source | scope |
| --- | --- | --- | --- | --- |
| routing-authority | `rule-routing` | `always-once` | this router | task |
| global-baseline | `rule-priority-hot-route` | `always-once` | [VibeAi](../VibeAi.md) | task |
| project-entry | `project-entry-loading` | `always-once` | project entry / `not-applicable` | project or `not-applicable` |

## Host-Agnostic Auto-Load Paradigm

Apply this baseline on every host. Before domain work, read the [catalog](catalog.md) and its matched owners. Re-evaluate triggers when the task changes; a pointer is not a completed read.

Applying a Skill follows the enabled [invocation declaration](../skills/rules.md#invocation-observations) through the shared producer. Reuse loaded text; telemetry failure stays ancillary. This route adds no automatic host coverage.

## Fixed Guards

Always read [reply](../process/communication-primary-response.md) and [title](../adapters/session-title.md). Resolve other matched sole_owner paths through the [registry](../README.md#contract-ownership-registry).

| contract_id | activation | trigger_ids |
| --- | --- | --- |
| `prior-task-overlap` | context | continuation,repeated-failure,overlap-check |
| `sidecar` | context | orchestration,cross-project |
| `documentation-impact` | context | rule-change,cross-project,document-sync |
| `communication-primary-response` | always-once | - |
| `task-outcome-and-evidence-stop` | context | scope-conflict,acceptance-conflict |
| `stable-developer-taste` | context | architecture,ui,design,performance |
| `intent-note-overlay` | project-marker | intent-note-gate:enabled |
| `session-title` | always-once | - |
| `task-skill-reminder` | context | skill-list-request |

## Guard Delivery

Measured channels emit short baseline carriers. Task semantics select conditional rules; transport context IDs do not replace this decision. In enabled projects, an explicit Intent Note command (`intent-note-command`) or matching active note (`intent-note-active`) requires its owner; enabling alone creates nothing.

## Deterministic Resolution

[Catalog](catalog.md).

## Persistence Boundary

No prompts/secrets. Report full UTF-8: 16 KiB baseline, 4 KiB each for core and project, 2.5 KiB for always-once guard owners; separate Skills/Hooks/built-ins. Preserve required semantics before optimizing size; report any excess instead of dropping rules.
