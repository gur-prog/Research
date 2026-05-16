# WORK_LOG

Chronological record of /progress invocations. Each entry: one invocation, one mode. Newest at the top.

The file has three sections: **Lessons & active feedback** (durable memory — consumed by /progress's PLAN step every iteration), **Recent iterations** (working memory — last ~5-10 full-detail entries), **Compressed history** (long-term memory — one-liner per older iteration, written by DIGEST passes).

---

## Lessons & active feedback

Curated by both user and /progress (via DIGEST or explicit promotion). Each lesson: short rule + why + when it applies. Append-only by the skill; the user can edit freely.

*(Empty — no iterations yet. Seed with cross-repo lessons you want enforced from day one, or let /progress accumulate them as iterations run.)*

---

## Recent iterations (full detail)

Newest at top. Capped at ~5-10 entries by DIGEST passes; older entries flow into Compressed history below.

## 2026-05-13T09:53Z — L2 DIVERGE — `mechanism-sourcing-followup-loop`: 7 design candidates

**Plan**: 0 design candidates against a per-parent floor of 3 → DIVERGE at L2 for the highest-leverage survivor. Span structural shapes (new skill / sub-mode / auto-spawn / inline / inversion / manual / passive) rather than variants of one shape.

**Method**: Three DIVERGE methods — structural enumeration (A/B/C/D), problem-inversion (E), and explicit keep-human-in-loop variant (F). Added G as a minimum-viable baseline so the trade-off conversation has a "do nearly nothing" floor.

**Files edited**: `backlog/agent-improvements/mechanism-sourcing-followup-loop.md`; `WORK_LOG.md`.

**Outcome**: 7 candidates, each with shape tag, source method, one-line summary, trade-off note, and `Pending` verdict. The 7 cover distinctly different design philosophies (resolution after the fact / prevention upstream / banning the feature / visibility-only) rather than near-duplicates.

**Flagged for human**: All 7 are `Pending` — no scoring this iteration (CONVERGE would be the next mode). Candidates **E (forbid)** and **G (passive)** are deliberately included as "options the user might reject for principled reasons" — surfacing them rather than archiving them keeps the trade-off space visible.

**Lessons surfaced**: One worth flagging — *"At DIVERGE, include at least one inversion candidate and at least one minimum-viable-baseline candidate, even if you expect both to lose, so the surviving candidates can be argued for instead of presumed."* Flagged for user approval.

**Next /progress would plan**: CONVERGE at L2 on `mechanism-sourcing-followup-loop` — score the 7 against goal-alignment / friction-cost / architectural-cost / reversibility. Likely to produce 1-2 Pass survivors that DROP LEVEL into implementation tasks.

---

## 2026-05-13T09:51Z — L1-secondary → L2 DROP LEVEL — opened L2 for 5 Pass survivors

**Plan**: 5 Pass survivors on L1 secondary, no L2 structure → protocol-correct next move is DROP LEVEL. Establish path convention `backlog/agent-improvements/<slug>.md` (mirroring `topics/<slug>/`), create one stub per survivor with parent driver + design-question seeds + empty `## Candidates` section.

**Method**: Wrote 5 stub files. Each cites its L1 parent, restates the driver in one paragraph, and surfaces 4-7 open design questions to seed the next L2 DIVERGE iteration (without committing to any one).

**Files edited**: 5 new files in `backlog/agent-improvements/`; `WORK_LOG.md`.

**Outcome**: L2 structure now exists for the 5 Pass survivors. `mechanism-sourcing-followup-loop.md` got extra design-question depth given its leverage. The other 4 got 4-6 questions each.

**Flagged for human**:
- New path convention established: `backlog/agent-improvements/<slug>.md`. If you'd prefer a folder-per-improvement (`backlog/agent-improvements/<slug>/design.md`, `<slug>/notes.md`, etc.), say so before the next DROP LEVEL — flatter is reversible into folders if needed.
- The 3 Borderlines have no L2 stubs because they're not survivors. They remain in the L1 file with their Borderline verdict.

**Lessons surfaced**: None new. Iter-1 lesson still flagged-but-unpromoted.

**Next /progress would plan**: DIVERGE at L2 on the highest-leverage survivor — `mechanism-sourcing-followup-loop` — generating 5-7 design candidates (e.g., "new dedicated skill", "sub-mode of `research-gather`", "synthesizer-auto-spawn", "delete the agent-added-mechanism feature entirely and force gather-2 to fill"). Other 4 L2s remain empty until their turn.

---

## 2026-05-13T09:50Z — L1-secondary CONVERGE — scored 8 candidates: 5 Pass, 3 Borderline

**Plan**: 8 unevaluated candidates on a never-scored level. Resolve the three "research pending" markers from iter 1 by reading the three referenced agent files, then score against goal-alignment × leverage × concreteness × cost. Verdict per candidate: pass / borderline / archive.

**Method**: Read `.claude/agents/synthesizer.md`, `.claude/agents/librarian.md`, `.claude/agents/source-scout.md` to ground verdicts in actual code. Scored each candidate with a 2-3 sentence rationale citing both GOAL.md ambitions and concrete file-level evidence.

**Files edited**: `backlog/agent-improvements.md` (8 verdict updates + scoring blocks), `WORK_LOG.md`.

**Outcome**:
- **Pass (5)**: `source-block-fallback-policy`, `rq-preflight-at-start`, `mechanism-sourcing-followup-loop`, `product-readiness-checklist-in-summary`, `coverage-vs-source-target-policy`. All have direct goal-alignment, high leverage, and small-to-medium implementation cost.
- **Borderline (3)**: `trust-tier-weighting-in-synthesis` (waiting on user policy choice — three framings flagged), `template-versioning-and-migration` (premature; revisit at topic-count ≥ 5), `cross-topic-source-and-finding-linking` (premature; revisit at topic-count ≥ 4 with observed overlap).
- **Archive (0)**.

**Flagged for human**:
- `trust-tier-weighting-in-synthesis` is borderline pending a user policy choice between three framings (every Layer-1 idea cites ≥1 strong-trust fact / Layer-1 rests on ≥X% strong / no-strong-evidence ideas demote). Surfaced rather than picked.
- The verified gap in `source-scout.md` step 8 is small but it implies that gather-2's actual stop call was outside the spec — worth a one-line confirmation that the user is OK with stopping when coverage is complete even below target.

**Lessons surfaced**: None new this iteration. The lesson surfaced in iter 1 (DIVERGE-secondary fallback when primary blocked) remains flagged-but-unpromoted.

**Highest-leverage Pass for an implementation pass next**: `mechanism-sourcing-followup-loop` (78% agent-added mechanisms is the biggest visible violation of the headline ambition) — but design choice ahead, so a DROP LEVEL into L2 design candidates would be the natural next move on this lane.

---

## 2026-05-13T09:45Z — L1-secondary DIVERGE — seeded agent-improvements backlog with 8 candidates

**Plan**: Primary lane fully blocked-on-user (health-longevity awaiting integration review; methodical-innovation awaiting scope edit). Both blockers are hard-rule-protected. Pivot to secondary lane; `backlog/agent-improvements.md` has 0 candidates against a floor of 5 → DIVERGE.

**Method**: Three DIVERGE methods mixed — first-principles re-derivation from GOAL.md's four ambitions; edge-case enumeration over `topics/health-longevity/log.md` retrofit entries (each retrofit is a signal of an upstream agent gap); structural-gap reading of the current pipeline (no shared evidence pool, no template-versioning, etc.).

**Files edited**: `backlog/agent-improvements.md`, `WORK_LOG.md`.

**Outcome**: 8 candidates landed, all `Pending`:
1. `source-block-fallback-policy` — codify substitution rules for 303/403/timeout sources.
2. `rq-preflight-at-start` — require RQs before gather; refuse to gather against placeholders.
3. `mechanism-sourcing-followup-loop` — close the loop on `added-by-agent` mechanism flags (78% of facts in health-longevity).
4. `product-readiness-checklist-in-summary` — give the review gate structured criteria.
5. `coverage-vs-source-target-policy` — define `source_target` vs RQ-coverage stop condition.
6. `trust-tier-weighting-in-synthesis` — verify/enforce trust-weighting in Layer-1 prose, not just Grounded-in blocks.
7. `template-versioning-and-migration` — stamp topics with template version; provide migration skill.
8. `cross-topic-source-and-finding-linking` — shared evidence pool across topics, not just within one tree.

**Flagged for human**: Three candidates contain "research pending" markers where current agent behavior wasn't verified by re-reading the agent files this iteration (`#4` summary tail, `#6` synthesizer weighting, `#8` librarian cross-topic affordance). Next CONVERGE pass on this level should verify each before scoring.

**Lessons surfaced**: One worth flagging for promotion — *"DIVERGE on the secondary lane is a legitimate fallback when the primary lane is fully blocked-on-user; the secondary lane should not be auto-suppressed by 'lower priority'."* Flagged for user approval before adding to `## Lessons & active feedback`.

---


---

## Compressed history

One-liner per past iteration. Pruned/edited only by DIGEST passes.

*(Empty — DIGEST has not yet run.)*
