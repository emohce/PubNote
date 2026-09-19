# PubNote route

<!-- compact-project-bootstrap:v1 -->

Load [VibeAi](ai-rules/kernel/VibeAi.md), the short [router](ai-rules/kernel/routing/README.md), and [LOADER](ai-rules/LOADER.md) once per task. Reuse on continuation; reload only relevant authority changes or fresh handoff.

Apply both baseline guards: session title format and concise numbered replies ([guards](ai-rules/distilled/guards.md)). Other guards and details are conditional; omit empty modules.
