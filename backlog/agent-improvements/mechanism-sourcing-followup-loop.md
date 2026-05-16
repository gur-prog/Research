# mechanism-sourcing-followup-loop — L2 design

**Parent**: [backlog/agent-improvements.md#mechanism-sourcing-followup-loop](../agent-improvements.md) — L1 verdict `Pass`. **Highest-impact survivor on the backlog.**

## Parent driver

Close the loop on `mechanism_source: added-by-agent` facts. When the synthesizer can't find a mechanism in cited evidence, it adds one and flags it. Health-longevity ended summarize-2 with 33 of 42 facts (78%) flagged this way — meaning most of the *why* in the summary is currently agent-inferred, not source-grounded. This is the single largest visible violation of the headline ambition "Every claim is true and traceable."

## Open design questions (seeds for L2 DIVERGE)

- **Shape of the loop**: New skill (`/research-mechanisms`)? Sub-mode of existing skill (`/research-gather --mechanisms-only`)? Auto-spawned by synthesizer when threshold exceeded?
- **Trigger**: User-initiated? Auto-triggered when `added-by-agent` count crosses a threshold? Periodic?
- **Query construction**: How does source-scout target a query at a specific mechanism claim? (Use the mechanism text itself? Extract keywords? Pair with parent fact's domain?)
- **Replacement protocol**: When a sourced mechanism is found, who rewrites the fact — synthesizer? librarian? a new agent?
- **What if no source found**: Promote to open-question? Keep `added-by-agent` flag? Demote the fact's trust?
- **Cross-topic implications**: Some mechanisms (e.g., glucose metabolism) will recur across topics — does this loop interact with cross-topic source pooling?
- **Cost**: Each agent-added mechanism is one extra gather. 33 in health-longevity — feasible? Batched?

## Candidates

### A — Dedicated `/research-mechanisms` skill

- **Shape**: New top-level skill, invoked manually by the user between `summarize` and `product`.
- **Source method**: DIVERGE — structural enumeration.
- **One-line summary**: Reads `open-questions.md`'s "Agent-added mechanisms" section, builds mechanism-targeted queries (pairing the parent fact's domain with the mechanism claim), runs a focused mini-gather, then re-invokes synthesizer to rewrite mechanism fields from sourced citations.
- **Trade-offs**: (+) Clear, auditable phase — user opts in, knows exactly what's happening. (+) Reuses existing source-scout + synthesizer machinery without sub-modes. (–) Adds another command and another review point; pipeline goes from 4 to 5 phases. (–) Easy to forget to run; debt accumulates if user skips.
- **Verdict**: Pending

### B — `research-gather --mechanisms-only` sub-mode

- **Shape**: Sub-mode of an existing skill.
- **Source method**: DIVERGE — structural enumeration.
- **One-line summary**: Same loop as A, but lives inside `/research-gather` as a flag. Pipeline stays 4 phases; the same skill does both initial gather and follow-up mechanism gather.
- **Trade-offs**: (+) No new skill to learn. (+) Logging stays in the same `log.md` entry shape ("gather-N — mechanisms-only"). (–) Mixes two semantically different jobs in one skill — initial coverage gather vs. targeted mechanism re-search. (–) `source-scout`'s query-planning step would need a branch for mechanism mode.
- **Verdict**: Pending

### C — Synthesizer auto-spawn at threshold

- **Shape**: Automation triggered by the synthesizer.
- **Source method**: DIVERGE — structural enumeration.
- **One-line summary**: When synthesizer detects `added-by-agent` ratio above a threshold (e.g., >20%), it automatically spawns a follow-up `research-gather --mechanisms-only` round before writing `summary.md`. User sees one summarize action that takes longer.
- **Trade-offs**: (+) Zero user friction — the debt never reaches `open-questions.md` in the first place. (+) The headline ambition gets enforced as a precondition for a "ready" summary. (–) Auto-spawning a gather inside summarize complicates failure modes and budget tracking. (–) Crosses the autonomy line — user no longer reviews mechanism sourcing decisions individually.
- **Verdict**: Pending

### D — Inline at fact-extraction time (source-reader)

- **Shape**: Move resolution upstream, before mechanisms get marked agent-added at all.
- **Source method**: DIVERGE — structural enumeration.
- **One-line summary**: When `source-reader` extracts a fact and can't find a mechanism in the source, it immediately queries `source-scout` for one targeted source covering that mechanism before finalizing the fact. The fact gets a sourced mechanism or no mechanism — never agent-added.
- **Trade-offs**: (+) Eliminates the debt category entirely. (+) Mechanism evidence ends up cited from the start. (–) Couples source-reader (fact-extractor) to source-scout (fetcher) — current architecture keeps them clean. (–) Per-fact extra fetch cost during initial summarize is large; for health-longevity's 33 missing mechanisms, that's 33 extra fetches at summarize time.
- **Verdict**: Pending

### E — Forbid agent-added mechanisms (inversion)

- **Shape**: Policy change, not a new mechanism for resolution.
- **Source method**: DIVERGE — problem-inversion of the current default.
- **One-line summary**: Disallow `mechanism_source: added-by-agent` entirely. Synthesizer must either find a mechanism in cited evidence or leave the mechanism field null (`no mechanism stated`). The follow-up question is whether the user wants the mechanism field at all when un-sourced.
- **Trade-offs**: (+) Strongest possible enforcement of the truth-and-trace ambition. (+) Zero new code — just a removal. (–) Many facts become mechanism-less, which weakens the "why it should work" narrative readers expect under each Grounded-in entry. (–) Loses the "agent inference is at least visible" benefit of the current flag — the inferences disappear instead of being tracked.
- **Verdict**: Pending

### F — Librarian batch resolution (`--resolve-mechanisms`)

- **Shape**: New librarian sub-mode, user-driven.
- **Source method**: DIVERGE — keep-human-in-the-loop variant.
- **One-line summary**: Librarian gains a `--resolve-mechanisms` apply mode that walks the user through each agent-added mechanism interactively — "accept current inference / search for source / mark as unsourced / demote fact to weak trust." Decisions are recorded and applied as a batch.
- **Trade-offs**: (+) Strongest user-control alignment — every inference gets an explicit human verdict. (+) Sits naturally in librarian (which already does proposal-then-apply). (–) High per-topic friction — 33 prompts for health-longevity. (–) Doesn't actually find new sources unless paired with B or A; the user picks between three already-bad options.
- **Verdict**: Pending

### G — Passive visibility (threshold-triggered demotion)

- **Shape**: No fix; visibility only.
- **Source method**: DIVERGE — minimum-viable baseline option.
- **One-line summary**: If a topic ends summarize with `added-by-agent` ratio above threshold, every agent-added mechanism's parent fact is auto-demoted to `trust: weak` (with original trust preserved as `original_trust`), and a "⚠ Mechanism debt" section is added to `summary.md` listing affected facts. No new gather; user can act on the visibility however they like.
- **Trade-offs**: (+) Tiny cost, ships immediately. (+) Makes the existing debt visible to downstream product-builder (which can avoid relying on demoted facts). (–) Doesn't actually solve the underlying problem — the corpus stays under-sourced. (–) Treating a missing mechanism as evidence that the *parent fact* is weak is technically wrong (the fact may have strong direct evidence; only the mechanism is inferred).
- **Verdict**: Pending
