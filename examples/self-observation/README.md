# Example: Self-Observation System

The first idea to graduate from the loop with a **START** verdict ([2026-W29 review](../../reviews/2026-W29.md)). Kept here as a worked example of what a "minimal experiment" attachment should look like.

## The idea

A lightweight daily self-log, analyzed monthly by an AI agent to surface patterns the author can't see from inside their own head — energy cycles, decision quality vs. context, recurring triggers.

## Why it passed triage

- **Capture tools exist; review loops don't.** Mood trackers optimize data entry, then leave you a chart. The valuable half — interpretation, pattern-finding, falsifiable predictions — is exactly what an LLM adds cheaply.
- **Minimal version is genuinely minimal.** Three fields a day, one file, one monthly prompt. No app to build.
- **Clear kill criterion.** If the habit doesn't survive 4 weeks at <2 min/day, the design is wrong — that's a result, not a failure.

## The 4-week experiment

**Daily (target: under 2 minutes):** append one line to `log.md`:

```
2026-07-17 | energy 4/5 | decision: declined the side project | context: slept 7h, heavy meeting day
```

**Week 4:** run the analysis prompt below against the full log.

**Success criterion:** the analysis produces at least one pattern that is (a) not obvious to the author and (b) testable in week 5.

**Kill criterion:** >8 missed days out of 28, or daily logging exceeding 2 minutes — stop, shrink the format, restart.

## Analysis prompt

```
You are reviewing 4 weeks of a daily self-observation log (energy, one decision,
one line of context per day). Find:
1. Patterns across energy, decision quality, and context — cite specific dates.
2. One thing the author likely believes about themselves that the data contradicts.
3. One falsifiable prediction about next week, checkable from next week's log.
Do not flatter. Missing days are data too.
```
