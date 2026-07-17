# IdeaLoop

**An agent-agnostic framework for capturing ideas and reviewing them weekly with an AI agent.**

[中文文档](./README.zh-CN.md)

Most ideas die in note apps. You capture them, they pile up, and nothing happens. IdeaLoop closes the loop: every idea you capture gets triaged by an AI agent on a fixed weekly schedule, and comes back to you as a concrete decision — **start it, keep exploring it, or shelve it with a re-activation condition**.

It works with any AI agent that can read files and run on a schedule: Claude (Cowork / Claude Code), OpenAI Codex, Cursor, or a plain cron job calling an LLM API.

## How it works

```
┌─────────────┐     weekly      ┌──────────────┐     you decide    ┌───────────┐
│ ideas/       │  ────────────▶ │ AI review    │  ───────────────▶ │ archive / │
│ inbox.md    │   (scheduled)   │ reviews/     │   (checklist)     │ projects  │
└─────────────┘                 └──────────────┘                   └───────────┘
```

1. **Capture** — whenever an idea strikes, append one entry to `ideas/inbox.md`. Ten seconds, no formatting pressure.
2. **Review** — once a week, your agent runs [`prompts/weekly-review.md`](./prompts/weekly-review.md) against the inbox. It researches each idea (web search, feasibility, prior art), then classifies it:
   - **START** — worth doing now; the agent attaches a minimal experiment (≤4 weeks, smallest testable version)
   - **EXPLORE** — promising but underdefined; the agent lists the open questions
   - **SHELVE** — not now; the agent writes down the *re-activation condition* so it isn't lost forever
3. **Decide** — the review ends with a short checklist of decisions only you can make. The agent never archives, deletes, or modifies your inbox on its own — see [`prompts/triage-rules.md`](./prompts/triage-rules.md).

## Quick start

### With Claude (Cowork or Claude Code)

1. Clone this repo (or copy the structure into any folder your agent can access).
2. Ask Claude: *"Every Thursday at 9am, run the weekly review in `prompts/weekly-review.md` against `ideas/inbox.md` and write the result to `reviews/`."*
3. Claude sets up a scheduled task. Done.

### With OpenAI Codex / other agents

Point your agent (or a cron job) at the same prompt file:

```
codex exec "$(cat prompts/weekly-review.md)"
```

### Manually

No automation needed to start — just paste `prompts/weekly-review.md` into any chat LLM along with your inbox once a week.

## Repository structure

```
idea-loop/
├── ideas/
│   └── inbox.md          # your capture inbox (append-only for humans)
├── reviews/
│   └── 2026-W29.md       # example weekly review output
├── prompts/
│   ├── weekly-review.md  # the review prompt (agent-agnostic)
│   └── triage-rules.md   # hard rules: what the agent may and may not do
└── examples/
    └── self-observation/ # a real idea that graduated from the loop
```

## Design principles

**The agent proposes, you decide.** The review is advisory. File moves, project kickoffs, and archiving all require a human check on the decision list. This keeps trust high enough that you'll actually let it run unattended.

**Every SHELVE has a re-activation condition.** "Not now" is a valid outcome, but only if it records *what would change your mind* (e.g. "revisit if X becomes legal / cheap / available"). Shelved ideas are dormant, not dead.

**START means a minimal experiment, not a commitment.** The agent must scope the smallest version that produces evidence within 4 weeks. See [examples/self-observation](./examples/self-observation) for what that looks like.

**Reviews are append-only history.** One file per week in `reviews/`, never edited afterwards. Over months this becomes a searchable record of your own judgment.

## Example

See [`reviews/2026-W29.md`](./reviews/2026-W29.md) for a real (anonymized) review: 4 ideas in, 1 START with a 4-week experiment plan, 2 EXPLORE, 1 SHELVE with a documented re-activation condition — including the web research that justified shelving it.

## Contributing

Issues and PRs welcome — especially adapters for other agents/schedulers, and translations of the prompts.

## License

[MIT](./LICENSE)
