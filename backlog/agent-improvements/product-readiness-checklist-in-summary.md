# product-readiness-checklist-in-summary — L2 design

**Parent**: [backlog/agent-improvements.md#product-readiness-checklist-in-summary](../agent-improvements.md) — L1 verdict `Pass`.

## Parent driver

Append an explicit "Ready for product?" section to every `summary.md` so the review gate has structured pass/fail criteria instead of being vibes-based. The ingredients already exist — `synthesizer.md` emits Coverage / Trust breakdown / Conflicts sections, and `open-questions.md` lists agent-added mechanisms. The improvement is consolidation into one explicit gate.

## Open design questions (seeds for L2 DIVERGE)

- What criteria belong in the checklist? (All RQs at ≥1 strong-trust source? <X% weak-trust facts in Layer-1? Agent-added mechanisms count? No unresolved Layer-1 contradictions? Coverage of all intended products' needs?)
- Pass/fail per criterion, or a weighted score?
- Where in `summary.md` does it live — top (TL;DR), bottom (verdict), or both?
- Does it block `/research-product` programmatically, or just inform the user?
- How does it interact with the existing librarian's hygiene flags?
- Per-product variant? (Meal-plan and rulebook may need different evidence depth.)

## Candidates

*(Empty — populated by future L2 DIVERGE iteration.)*
