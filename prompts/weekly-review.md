# Weekly Ideas Review — Agent Prompt

> Run this once a week against `ideas/inbox.md`. Output goes to `reviews/<ISO-year>-W<week>.md` (e.g. `reviews/2026-W29.md`). Read `prompts/triage-rules.md` first — those rules override anything here.

## Your task

You are reviewing the owner's idea inbox. For every entry added since the last review (compare against the most recent file in `reviews/`):

### 1. Research each idea

- Search the web for prior art: does this already exist? Who does it best?
- Check feasibility: technical, legal, and cost constraints as of today.
- Estimate effort for a minimal version (days/weeks, not months).
- If the idea depends on a factual claim, verify it and cite sources.

### 2. Classify each idea

| Verdict | Meaning | Required attachments |
|---|---|---|
| **START** | Worth doing now | A minimal experiment: smallest testable version, ≤4 weeks, with a success/kill criterion |
| **EXPLORE** | Promising but underdefined | The 2–3 open questions that block a verdict, and how to answer them |
| **SHELVE** | Not now | The reason, plus an explicit **re-activation condition** ("revisit if/when …") |

Be decisive. "EXPLORE" is not a dumping ground — if an idea has been EXPLORE for 3+ consecutive reviews, force it to START or SHELVE.

### 3. Write the review file

Structure:

```markdown
# <year>-W<week> Ideas Review

## Summary
<one paragraph: N new ideas, verdicts at a glance>

## Verdicts
### <idea-id / title> — START | EXPLORE | SHELVE
<research findings, reasoning, sources>
<required attachment per the table above>

## Decisions needed from the owner
- [ ] <each irreversible action, one checkbox per item>
```

### 4. End with the decision list

Everything irreversible goes on the owner's checklist, not into action. Typical items: archive idea X to `ideas/archive/`, create a project folder for idea Y, update the re-activation watch-list.

## Cadence contract

- One review file per week, even if the inbox is empty (write "no new ideas").
- Never edit a past review file.
- Keep the whole review under ~1500 words. Density over completeness.
