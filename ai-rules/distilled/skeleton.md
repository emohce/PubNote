# 项目接入骨架

> 蒸馏自：starter-kit（AI_RULES / documentation-template / repository-ai-todo）与项目入口约定。`kernel/starter-kit/PROJECT_STATUS-template.md` verbatim 随包。

## 1. 最小骨架

```text
<project>/
  AGENTS.md                # 项目短入口（指针，见 §2）
  vibe/rules/README.md     # 项目规则 hub：路径映射 + 项目门禁
  vibe/knowledge/          # 项目可复用知识（glossary/adr/error-memory/…）
  vibe/specs/PROJECT_STATUS.md   # 过程枢纽（有多任务/跨仓/长周期工作时才建）
```

可选增强：

```text
  CLAUDE.md / GEMINI.md / .github/copilot-instructions.md / .cursor/rules/*.mdc
  vibe/ai-db/              # 仅 DB/数据项目；变更 SQL 交付走这里的 sql.md
  vibe/specs/<yyMM>/<yyMMdd>/<HHmm-task-id>/   # 任务文档目录（Standard+ 用）
```

非 DB 项目不建空 `vibe/ai-db/`；无活动记录不建空登记表。

## 2. 项目短入口（`AGENTS.md`）模板

```markdown
# <Project> route

Load <RULES_ROOT>/VibeAi.md, <RULES_ROOT>/routing/README.md, the applicable
host adapter and vibe/rules/README.md once per task. Reuse on continuation;
reload only relevant authority changes or fresh handoff.

Apply both baseline guards: session title and numbered structured replies.
Other guards and details are conditional; omit empty modules.
```

要点：入口是**指针不是政策**——规则本体在 `<RULES_ROOT>`（本包 kernel/ 或你的规则目录），项目入口只指路 + 声明项目特有的东西在哪。

## 3. 项目规则 hub（`vibe/rules/README.md`）承载什么

- 本项目的路径映射：知识在哪、任务文档在哪、DB 工作区在哪、状态枢纽在哪。
- 项目特有门禁：本项目的部署/权限/数据边界（不重复全局政策）。
- 文档分级约定：什么时候写 `vibe/rules/documentation.md`（有遗留文档、DB/数据、跨仓、发布门、持续 Controlled 工作时）。

## 4. 采纳清单（从 repository-ai-todo 泛化）

```text
[ ] 项目有短 AGENTS.md 主入口；其他宿主入口仅在有用时建
[ ] 项目规则在 vibe/rules/（或声明的等价目录）
[ ] 有遗留文档/DB/跨仓/发布门/Controlled 工作时建 documentation.md
[ ] 可复用知识进 vibe/knowledge/（或声明的 canonical 源）
[ ] 任务文档用最小足够级：Quick 无文件 / Standard 非需求 task-card /
    Standard 需求 raw+spec / Controlled 五件套
[ ] 多任务/跨仓/DB/发布门/长周期 → 建 PROJECT_STATUS.md 枢纽
    （模板：kernel/starter-kit/PROJECT_STATUS-template.md）
[ ] DB 项目才有 vibe/ai-db/；变更 SQL 走 sql.md 交付不直接执行
[ ] 全局入口（~/.<host>/<entry>）指向共享基线，不复述政策
[ ] 相似/重复/恢复工作先跑 prior-task-overlap 再开新文档
[ ] 每次实现收尾分类 document_impact；受影响 owner 同轮同步
[ ] 规则变更带验证证据
```

## 5. 接入顺序建议

1. 先把 `kernel/` 放到你的规则目录（`~/ai-rules/` 或团队仓 `ai-rules/`）。
2. 写全局短入口（一个文件、纯指针）接入基线。
3. 在首个项目写 `AGENTS.md` + `vibe/rules/README.md`。
4. 跑一个真实任务验证：标题守卫能否交付（决定 §adapters 实测表）、回复结构是否被遵守。
5. 按需补 `vibe/rules/documentation.md`、`PROJECT_STATUS.md`、项目 adapter（ops-db §2 的运行时契约）。
