# Engineering Tool Selection Reference

Conditional reference for an explicit MCP/tool or delegated-runner task; ordinary coding uses existing repository tools. The engineering owner and current user authority govern selection.

## 6. MCP And Agent Tool Selection

Use MCP tools by engineering job:

| Tool | Use When | Install / Enable | Avoid When |
| --- | --- | --- | --- |
| `context7` | Current library/API docs, version-specific examples, setup/config questions | Codex MCP: `npx -y @upstash/context7-mcp@latest`; use API key only via env/header, never in notes | Business/domain facts, project-local behavior, or security decisions without primary validation |
| `inspector` | Developing or debugging MCP servers, checking tools/resources/prompts and transport behavior | Run ad hoc: `npx -y @modelcontextprotocol/inspector <server-command>` | Normal app debugging or production MCP exposure |
| `fastapi_mcp` | Existing FastAPI services that should expose selected endpoints as MCP tools | Project dependency only: `uv add fastapi-mcp` or `pip install fastapi-mcp`; mount with `FastApiMCP(app).mount()` after auth review | Non-FastAPI projects, broad public API exposure, endpoints with unsafe side effects |
| `nuxt-mcp-dev` / `vite-plugin-mcp` | Local Nuxt/Vite dev-server introspection for resolved config, plugins, module graph | Project dev dependency only; enable in Nuxt/Vite config and keep experimental status visible | Production MCP server needs; use `@nuxtjs/mcp-toolkit` or official Nuxt docs MCP for different goals |
| `coderunner` | Running generated code against local files inside a sandbox when privacy matters | Install only on compatible Apple Silicon/macOS with Apple container support; expose remote MCP URL only after sandbox verification | Ordinary shell/test commands, hosts without container support, untrusted code needing network/filesystem isolation not configured |

Selection rules:

- Prefer built-in repo tools (`rg`, tests, shell, project docs) before adding MCP.
- When the user asks Codex to let Devin execute a task, use `devin-cli` rather than the Devin Desktop launcher. If the `devin-cli` skill path has already succeeded in the current environment, reuse it without repeated prompts or preflight checks; re-run `devin-cli skills paths`, `devin-cli skills list`, or `devin-cli skills show <skill-name>` only after failure, CLI/config changes, cwd changes that affect project skills, or missing-skill symptoms. Pass the relevant skill context or slash skill name to Devin. Use Codex sub-agents only as a fallback when Devin CLI is unavailable or the user explicitly wants Codex-local delegation.
- Before asking Devin to execute, Codex must create an operation plan that lists direct files expected to change, indirect files or search methods needed to discover them, intended operations, verification commands, risk gates, and task progress state. Codex-generated caller artifacts such as plans, prompts, task-split records, supervision notes, handoff notes, and verification records, plus Devin-generated or updated files, must follow the existing project and global path, naming, `Tool: <tool-name>`, relative Markdown link, and duplicate-document rules in [process/rules.md](../process/rules.md) and [memory/rules.md](../memory/rules.md). Devin must follow the plan, update progress continuously, report changed files and verification evidence, and pause before high-risk actions.
- Codex owns Devin task orchestration: split independent work into parallel Devin tasks only when their file scopes and state do not interfere; record each thread's scope, startup command, expected outputs, and conflict boundaries; verify every thread actually started; monitor progress in a loop; resume or reissue interrupted tasks with the latest plan/progress context; reconcile outputs before local integration. Use a `goal`-style objective for Codex-managed Devin work so completion is evaluated against the requested outcome, not just command exit.
- For Devin CLI task execution, prefer non-interactive `devin-cli --sandbox -p --permission-mode auto` with a temporary config that grants only the needed `Read(...)`, `Write(...)`, and safe `Exec(...)` scopes. Plain `devin-cli -p --permission-mode auto` may reject writes in non-interactive mode; verify file contents after Devin reports success. Do not use `--permission-mode dangerous`, external writes, production changes, deletes, credentials, or publish/deploy actions without explicit confirmation.
- Project dependencies are never global defaults. Add `fastapi-mcp`, `nuxt-mcp-dev`, or `vite-plugin-mcp` only inside matching projects and document dependency impact.
- For generated code execution, prefer existing test runners or a verified sandbox. Do not use host shell execution as a substitute for CodeRunner-style isolation when the code is untrusted.
