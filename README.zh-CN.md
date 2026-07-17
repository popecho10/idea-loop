# IdeaLoop

**一个与 AI Agent 无关的想法管理框架：随手收集想法，由 AI 每周定时评审。**

[English](./README.md)

大多数想法死在笔记软件里——记下来、堆积、然后不了了之。IdeaLoop 把这个环闭上：你收集的每个想法都会在固定的每周评审中被 AI 处理，并以一个明确的决定回到你面前——**立项、继续探索、或带激活条件暂存**。

它兼容任何能读文件、能定时运行的 AI Agent：Claude（Cowork / Claude Code）、OpenAI Codex、Cursor，或一个调用 LLM API 的普通 cron 任务。

## 工作原理

1. **收集** — 想法冒出来时，往 `ideas/inbox.md` 追加一条。十秒钟，不需要任何格式。
2. **评审** — 每周一次，Agent 用 [`prompts/weekly-review.md`](./prompts/weekly-review.md) 处理收件箱：对每个想法做调研（网络检索、可行性、已有方案），然后分类：
   - **立项（START）** — 值得现在做；Agent 附上一个最小实验方案（≤4 周、最小可验证版本）
   - **继续探索（EXPLORE）** — 有潜力但定义不清；Agent 列出待回答的问题
   - **暂存（SHELVE）** — 暂时不做；Agent 写明*激活条件*，确保想法不会永久丢失
3. **决定** — 评审以一份"只有你能做的决定"清单结尾。Agent 绝不擅自归档、删除或修改你的收件箱——硬规则见 [`prompts/triage-rules.md`](./prompts/triage-rules.md)。

## 快速开始

### 使用 Claude（Cowork 或 Claude Code）

1. 克隆本仓库（或把目录结构复制到 Agent 能访问的任意文件夹）。
2. 对 Claude 说：*"每周四早上 9 点，用 `prompts/weekly-review.md` 评审 `ideas/inbox.md`，结果写入 `reviews/`。"*
3. Claude 会创建定时任务。完成。

### 使用 OpenAI Codex / 其他 Agent

把 Agent（或 cron 任务）指向同一个 prompt 文件：

```
codex exec "$(cat prompts/weekly-review.md)"
```

### 手动运行

不需要任何自动化也能开始——每周把 `prompts/weekly-review.md` 和你的收件箱一起粘贴给任意对话式 LLM 即可。

## 目录结构

```
idea-loop/
├── ideas/
│   └── inbox.md          # 想法收件箱（对人类只追加）
├── reviews/
│   └── 2026-W29.md       # 每周评审输出示例
├── prompts/
│   ├── weekly-review.md  # 评审 prompt（与 Agent 无关）
│   └── triage-rules.md   # 硬规则：Agent 能做什么、不能做什么
└── examples/
    └── self-observation/ # 一个从这个循环里"毕业"的真实想法
```

## 设计原则

**Agent 提议，人来决定。** 评审只是建议。移动文件、启动项目、归档都需要人在决定清单上确认。这让你能放心地让它无人值守运行。

**每个"暂存"都带激活条件。** "现在不做"是合法结论，但必须记录*什么情况会改变你的想法*（例如"若 X 变得合法/便宜/可得则重新评估"）。暂存的想法是休眠，不是死亡。

**"立项"意味着最小实验，而非承诺。** Agent 必须给出 4 周内能产生证据的最小版本。参见 [examples/self-observation](./examples/self-observation)。

**评审记录只增不改。** 每周一个文件，写完不再编辑。几个月后，它会成为一份可检索的、关于你自己判断力的历史记录。

## 示例

[`reviews/2026-W29.md`](./reviews/2026-W29.md) 是一份真实（已脱敏）的评审：输入 4 个想法，1 个立项（附 4 周实验方案）、2 个继续探索、1 个暂存（附完整的网络调研依据和激活条件）。

## 参与贡献

欢迎 Issue 和 PR——尤其是其他 Agent/调度器的适配方案，以及 prompt 的多语言翻译。

## 许可证

[MIT](./LICENSE)
