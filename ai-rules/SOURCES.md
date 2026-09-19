# SOURCES — distilled ↔ 源规则溯源

每个 distilled 文件的源 owner 与打包时 sha256。源文件变更后重算 hash 与本表比对：**hash 没变 → 不用重蒸馏**；变了 → 只重蒸馏受影响的 distilled 文件。

源根：`<REPO>/AiRef/VibePractice/Vibe_Rules/`（下表路径相对该根）。

| distilled 文件 | 源 owner（相对路径） | sha256@2026-09-18 |
| --- | --- | --- |
| `distilled/model.md` | `routing/README.md` | `cfa8d5a0…` |
| | `routing/catalog.md` | `fe5ac9b6…` |
| | `README.md`（Contract Registry） | `7614ae68…` |
| `distilled/guards.md` | `adapters/session-title.md` | `b758343a…` |
| | `adapters/session-title-details.md` | `0db1e45a…` |
| | `adapters/host-forms.md` | `73b1b48b…` |
| | `process/communication-primary-response.md` | `7f2feb94…` |
| | `process/communication-primary-response-details.md` | `56b7391e…` |
| `distilled/process.md` | `process/rules.md` | `7dbe59f2…` |
| | `process/documentation-impact.md` | `74f40387…` |
| | `process/worktree-tasks.md` | `55d4b563…` |
| | `process/requirement-versioning.md` | `819af6c7…` |
| | `process/checkpoint-resume.md` | `cc47b084…` |
| | `process/requirements-hub.md` | `a69ba0bd…` |
| | `process/feature-map.md` | `0ecceb2e…` |
| | `process/intent-notes.md` | `401797a9…` |
| | `process/dialogue-guided-execution.md` | `39b9b819…` |
| `distilled/memory.md` | `memory/rules.md` | `f5855167…` |
| | `memory/auto-memory/README.md` | `8fddb0e6…` |
| | `design-preferences/README.md` | `345587bc…` |
| `distilled/ops-db.md` | `ops/rules.md` | `50098fc5…` |
| | `ops/project-runtime.md` | `b0604851…` |
| `distilled/skills.md` | `skills/rules.md` | `f623ae6b…` |
| `distilled/ui.md` | `ui/rules.md` | `d1c71079…` |
| `distilled/adapters.md` | `adapters/host-forms.md` | `73b1b48b…` |
| | `adapters/devin.md` | `dec39dda…` |
| | `adapters/claude.md` | `87c47ce7…` |
| | `adapters/grok.md` | `00f7d482…` |
| | `adapters/opencode.md` | `4e9f1fcd…` |
| `distilled/skeleton.md` | `starter-kit/AI_RULES.md` | `7b91d76b…` |
| | `starter-kit/documentation-template.md` | `d818362c…` |
| | `starter-kit/repository-ai-todo.md` | `fa58513a…` |

另：`VibeAi.md`（`a21babbe…`）与 `developer-soul.md`（`0e9b387f…`）已 verbatim 进 `kernel/`，distilled 各文件对它们的引用不重抄。

完整 sha256 见 zip 内 `MANIFEST.json`；此处记前 8 位足够做漂移比对（`shasum -a 256 <源文件> | cut -c1-8`）。
