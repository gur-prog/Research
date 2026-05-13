---
generated_at: "2026-04-13"
trigger: auto-post-summarize
subtopics_scanned: ["sleep"]
proposal_counts:
  contradictions: 1
  promotions: 3
  supersessions: 0
  hygiene_flags: 1
  open_question_updates: 1
---

# Integration proposal — health-longevity

The sleep subtopic is done and contains several findings that refine or extend the parent synthesis. One soft contradiction with parent Layer-1 Idea 5, three promotable subtopic ideas, zero hard supersessions (subtopic effect sizes differ from parent Zhang 2025 numbers but both are valid meta-analyses of the same question — flag rather than supersede), one hygiene fix, and one resolved open question.

## Contradictions (review first)

### 1. Parent Layer-1 Idea 5 overstates the long-sleep risk

- **Parent (Layer 1, Idea 5):** "7–8 hours is the U-shaped optimum for cognitive decline, with both short (<7h) and long (>8h) sleep showing elevated risk [fact:28, fact:29, fact:30]."
- **Subtopic (Layer 1, Idea 2 + fact:7, fact:8):** The long-sleep arm of the U-curve is probably a disease marker or measurement artifact, not causal. Cognitive decline (the earlier phenotype) shows a null effect for long sleep, while only full dementia (the later phenotype) shows the association — a pattern more consistent with reverse causation. The 2025 meta-analysis authors explicitly refuse to claim causation and reframe the real variable as "disordered sleep," not duration.
- **Assessment:** Not a hard contradiction — parent fact 29 is still numerically correct, and parent Theme 3 prose already hedges that "reverse causation is plausible." The problem is that parent Layer-1 Idea 5 presents the U-shape as symmetric when the evidence strongly suggests it's asymmetric: short sleep is probably causal, long sleep is probably a marker.
- **Proposed resolution:** Rewrite parent Layer-1 Idea 5 to reflect the asymmetry and cite the subtopic's causal-uncertainty finding.

**Proposed replacement text for parent Idea 5:**

> **Idea 5 — Sleep is load-bearing for the cognition the studying is for, but the U-curve is asymmetric.**
>
> 7–8 hours is the population target, with short sleep (<7h) showing a robust ~27% increased risk of cognitive decline [fact:28, fact:30]. The often-cited long-sleep arm of the U-curve is weaker than it appears: only full dementia (not earlier cognitive decline) shows the association, the effect size shrinks under Bayesian meta-analysis (HR 1.29 vs the older RR 1.43), and the 2025 meta-analysis authors explicitly conclude that long sleep is probably a disease marker or reflection of poor sleep quality (more time in bed compensating for fragmented efficiency) rather than a causal driver [subtopic:sleep#fact:5, subtopic:sleep#fact:7, subtopic:sleep#fact:8]. Sleep quality (insomnia, fragmented sleep, sleep-disordered breathing) independently raises dementia risk on top of duration [fact:31]. For a student specifically, the energy-drink shortcut is a negative-ROI trap — each consumption cuts same-night sleep by ~24 minutes and the effect holds even for occasional users, creating a stimulation-sedation loop that compounds sleep debt [fact:40, fact:41, fact:42]. Sleep is not a variable you trade against study time without paying for it in the quality of the studying itself.
>
> `{author: librarian, from: subtopic:sleep, updated_at: 2026-04-13}`

## Promotions (new Layer-1 ideas for parent)

### Promotion 1 — "Sleep target is a population default with rare genetic exceptions"

- **Source:** `subtopic:sleep` Layer-1 Idea 1
- **Proposed placement:** New Layer-1 idea, inserted as parent Idea 7 (after the current Idea 6 on mindfulness)
- **Rationale:** The parent corpus treats 7–8 hours as a universal target. The subtopic adds important nuance — a small subset of humans with DEC2/ADRB1/NPSR1/GRM1 variants are genuinely fine on 4–6h — without weakening the default recommendation. This belongs in parent Layer-1 because it reshapes how a reader should interpret "optimal sleep" advice generally.

**Proposed block:**

> **Idea 7 — The 7–8 hour sleep target is a population default, not a universal.**
>
> A small subset of humans with rare mutations in DEC2, ADRB1, NPSR1, or GRM1 genuinely thrive on 4–6 hours per night with no cognitive or metabolic cost [subtopic:sleep#fact:1, subtopic:sleep#fact:2]. Critically, these variants are rare and the default remains 7–8 hours for anyone without the lifelong pattern, the absence of cognitive deficit, and the absence of rebound sleep on free days [subtopic:sleep#fact:4]. "I only need 5 hours" is almost always wrong unless all three of those conditions hold. The mechanism also clarifies what short-sleeping actually is — carriers have **enhanced wake-promoting signaling** rather than reduced sleep need, which is why the pattern can't be replicated by behavioral intervention in non-carriers.
>
> `{author: librarian, from: subtopic:sleep, updated_at: 2026-04-13}`

### Promotion 2 — "Wearables: trust sleep/wake, distrust stages (especially Apple Watch deep sleep)"

- **Source:** `subtopic:sleep` Layer-1 Idea 4
- **Proposed placement:** New Layer-1 idea, inserted as parent Idea 8
- **Rationale:** Self-assessment is a cross-cutting practical question that affects how the user acts on every sleep-related recommendation in the parent. This isn't just a sleep-theme detail — it's a behavior-measurement principle that belongs in the synthesis layer.

**Proposed block:**

> **Idea 8 — Consumer wearables are trustworthy for duration and timing, mediocre for sleep stages.**
>
> All three major wearables (Oura Ring, Fitbit Sense 2, Apple Watch Series 8) hit ≥95% sensitivity for the binary sleep/wake question vs. polysomnography — excellent for tracking sleep duration and wake-time consistency [subtopic:sleep#fact:9]. Sleep-stage accuracy is much weaker and device-dependent (Oura 76–80%, Fitbit 62–78%, Apple Watch 50–86% with wide variance), and Apple Watch specifically underestimates deep sleep by ~43 minutes, meaning users who worry about "not enough deep sleep" are often seeing a measurement artifact [subtopic:sleep#fact:10, subtopic:sleep#fact:11]. Complementary tool: the PSQI self-assessment correlates only weakly with polysomnography (r between −0.33 and 0.52) — subjective and objective sleep quality are **distinct constructs**, not interchangeable [subtopic:sleep#fact:14]. Use both, expect them to disagree, and don't optimize for a single number.
>
> `{author: librarian, from: subtopic:sleep, updated_at: 2026-04-13}`

### Promotion 3 — "Sleep interventions work in healthy people, with specific active ingredients"

- **Source:** `subtopic:sleep` Layer-1 Idea 5
- **Proposed placement:** New Layer-1 idea, inserted as parent Idea 9
- **Rationale:** Parent Layer-1 Idea 3 identifies diet as the highest-ROI first behavior for habit change, but the parent has no concrete guidance on *what specifically works* for sleep improvement. This promotion adds that missing lever.

**Proposed block:**

> **Idea 9 — Behavioral sleep interventions work in healthy people; hygiene alone does not.**
>
> Meta-analysis of 11 RCTs in adults *without* sleep disorders shows a medium effect (Hedge's g = −0.54) on sleep quality from cognitive-behavioral interventions — meaningfully helpful even for people whose sleep isn't clinically bad [subtopic:sleep#fact:16]. The four active ingredients across effective trials are **stress management/relaxation, stimulus control (bed only for sleep), sleep hygiene education, and exercise** — and hygiene alone (the advice most people get) is insufficient, underperforming the bundled approach in head-to-head comparisons [subtopic:sleep#fact:17, subtopic:sleep#fact:19]. The one significant moderator: worse baseline sleep → bigger improvement [subtopic:sleep#fact:18], so this is a high-ROI intervention specifically for the people who need it most.
>
> `{author: librarian, from: subtopic:sleep, updated_at: 2026-04-13}`

## Supersessions

None. Parent fact 29 (Zhang 2025 RR 1.43 dementia, RR 1.66 AD) and subtopic fact 5 (2025 Bayesian meta HR 1.29 dementia) are two different meta-analyses of the same question using different pooling methods. Both are valid; the newer Bayesian analysis is more conservative and comes with explicit causal uncertainty. **Proposed instead:** add a note to parent `facts.json` fact 29 under an optional `see_also` field: `"see_also": "subtopic:sleep#fact:5 — Bayesian meta-analysis with more conservative HR 1.29 and explicit reverse-causation discussion"`. No mutation of the original fact.

## Hygiene flags

### Flag 1 — Parent `open-questions.md` "Stress beyond mindfulness" remains valid

Not a defect — just confirming that the sleep subtopic did **not** resolve the broader stress landscape question. Leave in place.

## Open-questions updates

### Remove from parent `open-questions.md`:

- **"Sleep hygiene for students specifically — sources 006 and 010 cover cognitive effects and the caffeine-sleep loop, but not structured sleep hygiene protocols."** — Partially resolved by subtopic fact 16–19. The subtopic answers the question with "four-component CBT-I bundle, not hygiene alone." Propose replacing this entry with a pointer: *"Resolved by [subtopic:sleep](subtopics/sleep/summaries/summary.md) — see Theme 4. Deeper self-administered CBT-I protocols still open, tracked in subtopic's own open-questions."*

### No additions to parent open-questions.

The subtopic's new open questions (CBT-I protocols, circadian timing, wearable longitudinal validation, melatonin, etc.) are scoped within the sleep domain and should stay in the subtopic's own `open-questions.md`. If any of these are promoted to their own sub-subtopic via `/research-followup`, they will appear as a Layer-3 entry in the sleep subtopic's summary, not in the parent's.

## Deep dives update

Parent `summary.md` Layer-3 entry for sleep should change from *"Last integrated: pending"* to *"Last integrated: 2026-04-13"* once this integration is applied.

## Log entry to append on apply

```
## librarian-apply — 2026-04-13
- subtopic integrated: sleep
- Layer-1 ideas promoted: 3 (sleep target is population default, wearable caveats, sleep interventions work)
- Layer-1 ideas rewritten: 1 (Idea 5 — asymmetric U-curve)
- facts.json: added see_also on fact 29 pointing to subtopic:sleep#fact:5
- open-questions: replaced 1 entry with resolution pointer
- deep dives: sleep entry marked integrated
```

## Apply

To accept all proposals: `/research-integrate health-longevity --apply`

To accept a subset: edit this file to delete the sections you don't want, then run `--apply`.
