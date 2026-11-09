# Tasks Template

关键词：执行计划、实际进展、用户决定、剩余事项

正式文档按[关键词通则](../rules.md#document-keywords)从本篇正文重新提取；拆成多篇时各篇自有摘要。

> Legacy layout remains supported. New role-based tasks use [task-roles-template](task-roles-template.md); declared role mappings take precedence over filename/count guidance in this template.
Tool:
Date:
Task:

Documentation level: `controlled`

## Task State

`planned`

## Work Unit Ledger

| Work Unit | Work-order Version | Attempt | Surface | Runtime ID | State | Last Evidence | Blocker | Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  | 1 | 1 | main | app-root | pending |  |  |  |

## Execution Journal

Persist only material state, steering, interruption, failure/fallback, acceptance, metric, or durable-promotion events. Do not copy raw prompts, routine tool calls, or full child transcripts.

| Event ID | Local Time | Work Unit / Attempt | Actor / Surface | Event | Prior -> Resulting State | Trigger / Evidence | Root Decision / Next Action |
| --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |  |

## Checklist

- [ ] Inspect current implementation and rules.
- [ ] Apply scoped changes.
- [ ] Reconcile all `reported` results and record Root acceptance decisions.
- [ ] Verify behavior.
- [ ] Sync memory and process docs.
- [ ] Record final `document_impact`, resolve or retain `doc_drift`, and keep the task below `accepted` until affected authorities are synchronized.
- [ ] For a durable runtime/rule correction, synchronize task/mechanism design, requirement evolution and intermediate-problem/verified-alternative/verification records.
