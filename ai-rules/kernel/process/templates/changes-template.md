# Changes：<任务名> 变更清单

关键词：变更清单、文件职责、实施范围

正式文档按[关键词通则](../rules.md#document-keywords)从本篇正文重新提取；拆成多篇时各篇自有摘要。

> Legacy layout remains supported. New role-based tasks use [task-roles-template](task-roles-template.md); declared role mappings take precedence over filename/count guidance in this template.
> Inventory only. Judgement lives in `tasks.md`, evidence in `verify.md`, plan in `plan.md`; this file answers
> **which files changed and what each change was**, and links to the others rather than restating them.
> **Every list row carries a core-description cell** — a bare path list still forces the reader to open each file.
> Rows come from measured facts (Git diff, scanner output, real counts), never recollection.

## 1. 概览

| 批次 | 提交 | 文件数 | 核心说明 |
| --- | --- | --- | --- |
| <批次> | `<sha>` | <n> | <一句话：这批干了什么> |

## 2. 交付物清单

| 对象 | 类型 | 核心说明 |
| --- | --- | --- |
| `<repo-relative-path>` | 新增 / 改动 / 删除 | <这个文件是什么、为什么动它> |

## 3. 逐批清单

### <批次> `<sha>`

| 文件 | 核心说明 |
| --- | --- |
| `<repo-relative-path>` | <改了什么，一句话说清> |

## 4. 明确没做的（分流，不是遗漏）

| 对象 | 数量 | 核心说明 |
| --- | --- | --- |
| <对象> | <n> | <为什么不做、归到哪里> |

## 5. 用户可见行为变化

| 位置 | 变化 | 核心说明 |
| --- | --- | --- |
| `<repo-relative-path>` | <前 → 后> | <为什么会变、用户怎么应对> |

省略本节的前提是**确认没有**行为变化，而不是没检查。

## 6. 顺手发现但未处理

| 位置 | 现象 | 核心说明 |
| --- | --- | --- |
| `<repo-relative-path>` | <现象> | <为什么不在本轮修、需要什么授权> |

## 7. 回归数字

| 批次 | 测试 | 构建 | 静态检查 |
| --- | --- | --- | --- |
| <批次> | <文件/用例> | <exit / 规模> | <与基线对比> |
