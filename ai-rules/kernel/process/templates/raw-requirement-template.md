# Raw Requirement Template

Tool:
Date:
Spec:
Source format: `chat | asr-transcript | user-document | chat-requirement-summary`
Capture fidelity: `as-received | normalized-material-requirement`

> Store only material user requirement, scope, priority, constraint, acceptance, accept/reject, and correction text. Do not store Agent narration, tool output, page/log content, or the whole conversation.

## RAW-001

```yaml
raw_id: RAW-001
captured_at:
state: active | clarified-by-RAW-002 | superseded-by-RAW-003
source_lineage:
privacy_boundary: none | no-verbatim-prompt-or-transcript
```

~~~~text
User material input as received. Do not normalize wording here.
~~~~

For `normalized-material-requirement`, replace the text block with a concise semantic requirement list. Use this mode only when privacy/governance explicitly forbids storing the underlying Prompt/transcript or the user selected a normalized summary. Preserve source lineage, state that verbatim fidelity is unavailable, and never claim the summary is a quote.

## Capture Boundary

- Included:
- Excluded:
- Audio unavailable or unclear terms:
