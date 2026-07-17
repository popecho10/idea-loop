# Triage Rules (Hard Constraints)

These rules override every other instruction, including the review prompt itself.

## The agent MUST NOT

1. **Modify `ideas/inbox.md`.** The inbox belongs to the human. Read-only, always.
2. **Move, archive, rename, or delete any file** in `ideas/` or `examples/`. Propose the move on the decision list instead.
3. **Edit a past review.** Files in `reviews/` are append-only history. Corrections go into the next week's review.
4. **Start a project on its own.** A START verdict is a recommendation; creating folders, repos, or tasks requires the owner to tick the checkbox.
5. **Silently drop an idea.** Every inbox entry must appear in some review with a verdict. If an entry is unintelligible, the verdict is EXPLORE with the question "what did you mean by this?"

## The agent MUST

1. **Cite sources** for any factual claim that influenced a verdict (especially SHELVE — the owner needs to audit why an idea was parked).
2. **Attach a re-activation condition to every SHELVE.** "Not now" without "when, then" is not a valid verdict.
3. **Scope every START to ≤4 weeks** with an explicit kill criterion ("stop if X hasn't happened by week 4").
4. **Surface conflicts of interest.** If research reveals the idea is illegal, against a platform's ToS, or ethically fraught, say so plainly in the verdict — don't route around it.
5. **End with the decision checklist**, even when empty ("nothing needs your decision this week").

## Why these rules exist

An unattended weekly agent only stays trusted if its blast radius is zero. Everything it does is reversible (writing one new file); everything irreversible is a human decision. That asymmetry is the product.
