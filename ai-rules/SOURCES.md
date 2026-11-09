# SOURCES — distilled ↔ 源规则溯源

每个 distilled 文件的源 owner 与打包时 sha256。源文件变更后重算 hash 与本表比对：**hash 没变 → 不用重蒸馏**；变了 → 只重蒸馏受影响的 distilled 文件。

源根：`<REPO>/AiRef/VibePractice/Vibe_Rules/`（下表路径相对该根）。

| distilled 文件 | 源 owner（相对路径） | sha256@2026-11-09 |
| --- | --- | --- |
| `distilled/model.md` | `routing/README.md` | `526d47c1…` |
|  | `routing/catalog.md` | `7d2e9dc8…` |
|  | `README.md`（Contract Registry） | `be756a0e…` |
| `distilled/guards.md` | `adapters/session-title.md` | `f67ddf40…` |
|  | `adapters/session-title-details.md` | `347e3ca3…` |
|  | `adapters/host-forms.md` | `73b1b48b…` |
|  | `process/communication-primary-response.md` | `a8ce0f33…` |
|  | `process/communication-primary-response-details.md` | `a4d41389…` |
| `distilled/process.md` | `process/rules.md` | `fa0d05c7…` |
|  | `process/documentation-impact.md` | `ea0601e2…` |
|  | `process/worktree-tasks.md` | `0f3d1a8c…` |
|  | `process/requirement-versioning.md` | `3a29576f…` |
|  | `process/checkpoint-resume.md` | `cc47b084…` |
|  | `process/requirements-hub.md` | `655d6920…` |
|  | `process/feature-map.md` | `daee667a…` |
|  | `process/intent-notes.md` | `401797a9…` |
|  | `process/dialogue-guided-execution.md` | `39b9b819…` |
| `distilled/memory.md` | `memory/rules.md` | `f0e5280d…` |
|  | `memory/auto-memory/README.md` | `8fddb0e6…` |
|  | `design-preferences/README.md` | `345587bc…` |
| `distilled/ops-db.md` | `ops/rules.md` | `a87fc38c…` |
|  | `ops/project-runtime.md` | `08694eaa…` |
| `distilled/skills.md` | `skills/rules.md` | `833efa3b…` |
| `distilled/ui.md` | `ui/rules.md` | `4e09f689…` |
|  | `memory/browser-routing-memory.md` | `621c5077…` |
| `distilled/adapters.md` | `adapters/host-forms.md` | `73b1b48b…` |
|  | `adapters/devin.md` | `dec39dda…` |
|  | `adapters/claude.md` | `1731bc32…` |
|  | `adapters/grok.md` | `6b7b0328…` |
|  | `adapters/opencode.md` | `4e9f1fcd…` |
| `distilled/skeleton.md` | `starter-kit/AI_RULES.md` | `28731abd…` |
|  | `starter-kit/documentation-template.md` | `d818362c…` |
|  | `starter-kit/repository-ai-todo.md` | `c7982937…` |

另：`VibeAi.md`（`2b5c3e54…`）与 `developer-soul.md`（`79c4fe09…`）已 verbatim 进 `kernel/`，distilled 各文件对它们的引用不重抄。

完整 sha256 见 zip 内 `MANIFEST.json`；此处记前 8 位足够做漂移比对（`shasum -a 256 <源文件> | cut -c1-8`）。
