# Prior Task Overlap Gate

<!-- rule-contracts: prior-task-overlap -->

This file is the sole normative owner of the Prior Task Overlap gate. `process/rules.md` keeps the gate heading and a link-only stub for anchor compatibility; hubs, routers, templates and project adapters route here and must not restate the algorithm.

For similar, repeated, resumed or recovery-sensitive work, inspect the current hub, owner and registry before creating identity or rerunning evidence. Record:

- Document governance: existing Task/canonical/status owners and whether the new request belongs to them.
- Execution logic verification: actual running/closed state, accepted evidence, current Git view and whether prior logic still applies.
- Traceability: stable parent identity, superseded versions, remaining gate and net delta.

Reuse the same parent identity when the objective, allowed scope and output contract are stable. Continue only the net delta; stale or conflicting work is steered, superseded or explicitly separated.

## Continuity discovery

On task start/resume, Worktree attachment, material requirement change and delivery-state change, inspect the declared repository inventory and accessible host metadata. Use [portal-discover or task-view discover](task-views.md#interfaces) for the declared catalog/family. A catalog checks explicit task identity first, then keyword candidates; an incomplete or unavailable catalog returns unknown rather than concluding a new theme. Distinguish continuing a task, a possible child of an existing theme, a possible new theme and unresolved ambiguity. Existing decision evidence suppresses unchanged suggestions. For an explicit match with a lifecycle declaration, discovery invokes its read-only resume check; stale projections or missing registrations remain visible. This is event-driven reading, not a scheduler or permission to message other chats.

- Exact task identity, an explicit derivation or a documented handoff can retain the parent. Titles/keywords/code overlap produce candidates only; carried old task files do not establish ownership. Inventory includes unregistered/detached Worktrees in declared repositories and reports inaccessible scope.
- Surface related uncommitted work, committed but unintegrated work and integrated but unreleased scope; preserve the original checkout. Propose association and the remaining delivery boundary. Association never performs Git integration, commit, push, deployment, service or database actions.
- Multiple/weak candidates require a user choice before association. Persist accepted/separate/rejected/deferred decisions with their basis; do not repeat unchanged suggestions. Existing paused or closed decisions stay intact.
- Publication covers explicit requirements and repositories. Partial/failed releases remain visible. A later explanation/evidence correction continues the existing theme; a new fix/enhancement uses a delivery cycle, with a branch page when independently scoped. Preserve the released snapshot.
- Mark unavailable conversation/workspace coverage. Summarize material inputs only; never persist raw prompts/transcripts. The generated HTML is the last checked snapshot, and a new host session still requires its own observed invocation evidence.
