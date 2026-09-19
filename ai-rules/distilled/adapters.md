# 宿主适配模式

> 蒸馏自：host adapter 族（devin/claude/grok/opencode/codex 等）与 host-forms owner。具体的实测能力表和 launcher 登记表是源仓证据，不携带——你要给自己的宿主实测一份。

## 1. Adapter 是什么

每个宿主一个**短**适配文件，只含两块：

1. **Always-load 表**：本宿主读哪些入口文件（全局 + 项目）、注入形式、作用域。
2. **能力清单（capability manifest）**：本宿主已确认的能力及状态。

Adapter **绝不复述政策**——政策在共享 owner，adapter 只链接。同一政策被两个 adapter 复制 = 漂移起点。

## 2. 能力清单的字段语义

| 字段 | 含义 |
| --- | --- |
| `capability_id` | 能力名：instruction-loading / session-rename / execution-mode / hooks / file-navigation / guard-delivery / scheduled-automation / usage-counters … |
| `state` | `observed`（实测见过）/ `configured`（配置了未实测）/ `supported`（文档声称）/ `unmeasured`（存在但没测）/ `unavailable`（确认没有） |
| `values` | 可选值集 |
| `default` | 默认路由 |

纪律：

- **configured ≠ 接受**：配置写了不代表新会话真的吃——状态如实标注，不接受的能力回退 `main-only`。
- **能力归 launcher 不归 binary**：同一 binary 不同启动器（桌面壳、终端包装、IDE 嵌入）能力不同——这是"form 差异"，不是"unmeasured"。
- 未登记的 form 报 `unmeasured-form`，不猜 API。
- 兄弟 launcher 缺的 API 不等于本 form 缺。

## 3. Host-form 解析顺序

1. 解析当前 launcher → form key（`binary-launcher`，如 `<agent>-terminal`、`<agent>-desktop`、`<agent>-ide`）。
2. 按 form 的能力清单路由；缺能力 → 该能力的守卫降级或 `unmeasured-form`。
3. 能力变更（升级/新装插件）→ 重测受影响行，更新清单。

## 4. 守卫交付（guard-delivery）

宿主能不能被"注入规则"决定两个固定守卫怎么交付：

- 支持会话改名 → 标题守卫走实测 API；
- 不支持 → 降级为首轮回复给出建议标题。
- 回复结构守卫是纯指令行为（`instruction-only`），任何宿主都能交付。

## 5. 写你自己的 adapter（模板）

```markdown
# <Host> Rule Loading Adapter

## Always Load
| load_id | load_type | source | scope |
| --- | --- | --- | --- |
| injected-entry | always-once | ~/.<host>/<entry-file> + 仓内 AGENTS.md 等价物 | task |

## Host Capability Manifest
| capability_id | state | values | default |
| --- | --- | --- | --- |
| instruction-loading | observed | global-entry, project-entry | global-entry |
| session-rename | unmeasured | - | - |
| execution-mode | configured | main-only, native-agents | main-only |
| hooks | unmeasured | - | - |
| usage-counters | unavailable | - | - |
```

然后按 `distilled/skeleton.md` 的清单把入口文件接上。实测一行更新一行——清单是活证据不是宣称。

## 6. 多宿主共存的推论

- 共享政策文件被 N 个宿主入口同时指针引用是**设计内**；每个入口只是指针不是 owner。
- 某宿主不能加载 Markdown 入口时，用该宿主的注入机制（rules 目录、frontmatter、globs）放**指针文本**，内容仍指向共享 owner。
- 同一时刻只用当前 form 的能力集；不要把别的宿主的能力当默认。
