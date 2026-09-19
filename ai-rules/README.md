# Portable AI Rules

> A portable version of an AI coding-assistant rule system: short-entry injection + on-demand contract routing, not one giant prompt. `kernel/` holds verbatim rule snapshots, `distilled/` holds sanitized mechanism rewrites, `LOADER.md` explains the model and reading order. Docs are in Chinese; kernel rule files are in English.

一套 AI 编码助手规则体系的可移植版本：面向**没有源仓访问权限**的使用者。

它不是一份"提示词大全"，而是一套**按需加载的规则架构**——短入口注入基线，任务信号决定再加载哪些契约。本目录同时包含这套架构的脱敏说明和可直接采用的核心规则原文。

## 目录结构

| 位置 | 内容 | 性质 |
| --- | --- | --- |
| `README.md` | 本文件 | 入口 |
| `LOADER.md` | 体系模型、阅读/加载顺序、文件地图 | 必读 |
| `kernel/` | 核心规则文件的**原文快照**（基线、工程、测试、安全、Git、任务模板等） | 可直接采用或改写 |
| `distilled/` | 含项目细节的规则的**脱敏改写**（加载模型、守卫、过程、记忆、发布/DB、Skill、UI、宿主适配、项目骨架） | 读机制，按需落地 |
| `SOURCES.md` | 每个 distilled 文件 ← 源规则 + sha256 | 溯源/更新用 |
| `UPDATE.md` | 本目录怎么迭代、新版怎么合并 | 维护 |

## 怎么用起来

1. 先读 `LOADER.md` 理解模型：这套体系靠"短入口 + 契约路由"工作，不是把所有规则塞进上下文。
2. 选一个落地姿势：
   - **全量采用**：把 `kernel/` 放到你的规则目录（如 `~/ai-rules/` 或仓内 `ai-rules/`），按 `LOADER.md` 写两个短入口文件（全局一个、项目一个）。
   - **部分采用**：只挑需要的域。`kernel/VibeAi.md` + `kernel/engineering/` + `kernel/testing/` 是最小有价值组合。
   - **只读机制**：不落地文件，把 `distilled/` 当设计参考，融进你自己的规则。
3. 按 `distilled/skeleton.md` 的项目骨架给你的仓库建 `AGENTS.md` 之类的短入口。

## 边界

- 这是**快照投影**，不是源规则的活文档；源仓才是权威。版本对齐靠 git 历史（仓库分发）或 `PACK-VERSION`/`MANIFEST.json`（zip 构建产物）。
- `kernel/` 文件里可能有指向源仓其他文件的链接——那些文件不在本目录属预期，`LOADER.md` 的文件地图会说明每个域的脱敏替代是哪个 distilled 文件。
- 规则里的示例日期/任务编号均为虚构示例。
- 不要把这份内容当作"第二套可编辑母版"去集体维护——它的设计目标是分发，回写流走 `SOURCES.md`。

## 完整性

- 仓库分发：git 历史即完整性记录。
- zip 构建产物附 `MANIFEST.json`（全部文件 sha256），可按其中 `files` 表逐条 `shasum -a 256` 比对。
