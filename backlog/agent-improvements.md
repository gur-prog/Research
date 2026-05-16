# Agent improvements — L1 (secondary lane)

Backlog of improvements to the research agent's tooling — skills, agents, templates, pipeline mechanics. `/progress` consumes this as the L1 candidate list for the secondary lane. Lower default priority than the research lane; touched when the user supplies notes or when every research topic is blocked.

State legend:
- `open` — surfaced, not yet acted on.
- `in-progress` — partial work landed; more pending.
- `done` — shipped and superseded by code.
- `archived` — decided against.

---

## source-block-fallback-policy

- **State**: `open`
- **Source**: progress-surfaced (DIVERGE — edge-case enumeration)
- **One-line summary**: Codify the source-substitution rules when a fetched URL returns 303 / 403 / timeout, so `source-scout` doesn't have to improvise per run.
- **Why it matters**: Health-longevity's gather rounds hit blocked sources twice (Nature Medicine 303, Wiley 403) and ad-hoc substitutions were logged. Every future gather will hit this. A written policy (max retries, when to swap to PMC, when to abandon a search lead, what to log) makes the substitution auditable rather than opaque.
- **Files likely affected**: `.claude/agents/source-scout.md`, `.claude/skills/research-gather/SKILL.md`, log format conventions.
- **Verdict**: Pass
- **Scoring**: Direct goal-alignment to **truth-and-trace** (substitutions decide what evidence reaches `facts.json`). High leverage — every gather hits blocked URLs sooner or later. Concrete and small: a written policy section in `source-scout.md` codifying retry budget, substitution preference order (PMC mirror, alternate journal mirror, abandon-and-replan), and the log line format. Low cost, every-topic benefit. Verified gap: `source-scout.md` says nothing about HTTP failure handling.
- **Evidence**: [topics/health-longevity/log.md](../topics/health-longevity/log.md) lines 12, 43 (`"Nature Medicine source blocked (303); substituted Science Advances 2026 cohort"`, `"Nature source blocked (303) → PMC substitute; Wiley 403 → PMC substitute"`).

## rq-preflight-at-start

- **State**: `open`
- **Source**: progress-surfaced (DIVERGE — first-principles from GOAL.md ambition "Knowledge accumulates and lands in real life")
- **One-line summary**: At `/research-start`, require the user to fill in `Goal` + `Follow-up goal` + `Research questions` before the topic is considered ready for `/research-gather` — refuse to gather against template placeholders.
- **Why it matters**: Health-longevity was started without RQs and needed a retrofit log entry to add 7 RQs covering its actual scope. Methodical-innovation is currently in the same state (topic.md still on placeholders, blocking the entire primary lane right now). A pre-flight check shifts this work to where it belongs — before gather, when the user is engaged with scoping.
- **Files likely affected**: `.claude/skills/research-start/SKILL.md`, `.claude/skills/research-gather/SKILL.md` (add a pre-flight readiness check), `templates/topic.md` (signal which fields are required vs optional).
- **Verdict**: Pass
- **Scoring**: Direct goal-alignment to **"knowledge accumulates and lands in real life"** — `methodical-innovation` is currently blocking the entire primary lane because of exactly this gap. High leverage (every new topic). Concrete: add a `topic.md` validation step in `research-start` (refuse to finish without filled-in `Goal` + `Follow-up goal` + ≥3 research questions) and a precondition check at the start of `research-gather`. Source-scout already depends on RQs existing as a coverage checklist (step 2), so refusing to gather without them is consistent with the rest of the pipeline. Small-medium cost.
- **Evidence**: [topics/health-longevity/log.md](../topics/health-longevity/log.md) lines 32-36 (`"retrofit — 2026-04-13 (follow-up goal + research questions)"`); [topics/methodical-innovation/topic.md](../topics/methodical-innovation/topic.md) currently on template placeholders.

## mechanism-sourcing-followup-loop

- **State**: `open`
- **Source**: progress-surfaced (DIVERGE — edge-case enumeration)
- **One-line summary**: Add an explicit skill (or sub-mode) to systematically re-research the agent-added mechanisms flagged in `open-questions.md` per topic, replacing them with sourced citations on a follow-up gather pass.
- **Why it matters**: When the synthesizer can't find a mechanism in cited evidence, it adds one and flags `mechanism_source: added-by-agent`. Health-longevity ended summarize-2 with 33 of 42 facts (78%) flagged this way — meaning most of the *why* in the summary is currently agent-inferred, not source-grounded. There is no skill that closes this loop, so the topic carries a long tail of unverified inferences in tension with the "Every claim is true and traceable" ambition.
- **Files likely affected**: New `.claude/skills/research-mechanisms/SKILL.md` (or fold into `research-gather` as a sub-mode), `.claude/agents/source-scout.md` (mechanism-targeted query mode), `.claude/agents/synthesizer.md` (replace `added-by-agent` mechanisms on incorporation).
- **Verdict**: Pass
- **Scoring**: Direct goal-alignment to the headline ambition **"Every claim is true and traceable"** — 78% agent-added mechanisms in `health-longevity` (33 of 42 facts) is the single largest visible violation of this ambition in the corpus. High leverage (every summarize creates this debt). Concreteness medium — the design has a real choice point: new `/research-mechanisms` skill vs. a `research-gather --mechanisms-only` sub-mode. Medium cost, but the impact justifies prioritizing the design pass over the smaller wins. This is the highest-impact candidate on the backlog.
- **Evidence**: [topics/health-longevity/log.md](../topics/health-longevity/log.md) lines 27-31, 52 (`"agent-added mechanisms: 33 of 42 facts (all logged in open-questions.md by mechanism family)"`); [topics/health-longevity/summaries/open-questions.md](../topics/health-longevity/summaries/open-questions.md) — "Agent-added mechanisms to source properly" section.

## product-readiness-checklist-in-summary

- **State**: `open`
- **Source**: progress-surfaced (DIVERGE — first-principles from GOAL.md value "No autonomy past human-review gates")
- **One-line summary**: Append an explicit "Review checklist" section to every `summary.md` so the user reviewing it has a structured way to judge whether it's ready for product generation.
- **Why it matters**: The `summarize → product` review gate is load-bearing for trust, but the user currently has no scaffold for what to check. A short checklist surfacing items like *(a) all RQs answered? (b) any weak-trust facts in load-bearing positions? (c) any agent-added mechanisms still unresolved? (d) any open questions material to the intended products?* makes the gate productive instead of vibes-based and cheap to honor consistently across all future topics.
- **Files likely affected**: `.claude/agents/synthesizer.md` (emit the checklist as the last section of `summary.md`), possibly new `templates/summary-review-checklist.md` for the schema.
- **Verdict**: Pass
- **Scoring**: Direct goal-alignment to **"No autonomy past human-review gates"** — the gate is currently vibes-based and the synthesizer already writes the ingredients needed for a structured gate (Coverage section, Trust breakdown, Conflicts-and-uncertainty, plus `open-questions.md`'s "Agent-added mechanisms" section). High leverage (every review). Concrete: consolidate the existing review signals into one explicit "## Ready for product?" section at the end of `summary.md` with named pass/fail criteria (all RQs at ≥1 strong-trust source; <X% weak-trust facts in Layer-1; agent-added mechanisms tracked). Small cost — a synthesizer spec update. Verified gap: `synthesizer.md` does not currently emit a consolidated review section.
- **Evidence**: GOAL.md value "No autonomy past human-review gates"; `.claude/agents/synthesizer.md` writes Coverage / Trust breakdown / Conflicts sections but no explicit review-gate checklist.

## coverage-vs-source-target-policy

- **State**: `open`
- **Source**: progress-surfaced (DIVERGE — edge-case enumeration)
- **One-line summary**: Define the relationship between `source_target` (a count) and research-question coverage (a checklist) so `/research-gather` has a single clear stop condition.
- **Why it matters**: Health-longevity's gather-2 stopped at 11/12 sources because RQ coverage was complete — but the decision to stop early was logged as ad-hoc judgment ("did not hit 12/12 but coverage-complete so stopped"). The policy could be: `source_target` is a floor *only when* RQ coverage isn't met; once every RQ has ≥1 strong-trust source, gather can stop. Either way it should be written down so `source-scout` doesn't relitigate it per topic.
- **Files likely affected**: `.claude/skills/research-gather/SKILL.md`, `.claude/agents/source-scout.md`, `templates/topic.md` (clarify what `source_target` means).
- **Verdict**: Pass
- **Scoring**: Indirect-but-real goal-alignment (clarifies a process used on every gather; touches truth-and-trace through coverage rigor). High leverage. The current spec in `source-scout.md` step 8 covers "target reached + coverage done" and "target reached + coverage incomplete" but does not define the case observed in health-longevity gather-2 (`"did not hit 12/12 but coverage-complete so stopped"`) — that decision was implicitly made by the agent and recorded only in the log. Small cost: extend the stop-condition spec to handle "below target, coverage complete" explicitly. Pure spec work.
- **Evidence**: [topics/health-longevity/log.md](../topics/health-longevity/log.md) line 45 (`"did not hit 12/12 but coverage-complete so stopped"`); `.claude/agents/source-scout.md` step 8 stop-condition is silent on the below-target + full-coverage case.

## trust-tier-weighting-in-synthesis

- **State**: `open`
- **Source**: progress-surfaced (DIVERGE — first-principles from GOAL.md ambition "Readability is load-bearing")
- **One-line summary**: Verify (and if needed, enforce) that the synthesizer weights strong-trust facts more heavily than moderate/weak ones when writing the Layer-1 Synthesis section — not just when displaying Grounded-in blocks.
- **Why it matters**: Facts already carry a `trust: strong | moderate | weak` field. Surfacing that field in the Grounded-in block (current behavior) is necessary but not sufficient — the synthesis prose at the top of the summary is the most-read part and should be driven mostly by strong-trust facts, with moderate-trust used only as supporting detail. Otherwise the headline narrative can be propped up by the weakest evidence without the reader noticing.
- **Files likely affected**: `.claude/agents/synthesizer.md` (Layer-1 prompt spec).
- **Verdict**: Borderline
- **Scoring**: Direct goal-alignment to **readability**. `synthesizer.md` already prefers higher trust during conflict resolution and renders trust tiers in Grounded-in blocks, but has no explicit Layer-1 weighting rule. Borderline because the *policy choice* is non-trivial and reserved for the user: framing A — "every Layer-1 idea must cite ≥1 strong-trust fact"; framing B — "Layer-1 must rest on ≥X% strong-trust facts"; framing C — "if no strong evidence supports an idea, the idea moves to Layer-2 or is deleted." All three are defensible. **Flagged for user** — needs the user to pick a framing before this can promote to Pass. The implementation itself is small once the rule is chosen.
- **Evidence**: [topics/health-longevity/log.md](../topics/health-longevity/log.md) lines 22-26, 49-50 — trust tiers exist and are displayed in Grounded-in; `.claude/agents/synthesizer.md` step 3 weights trust in conflict resolution but Layer-1 spec has no weighting rule.

## template-versioning-and-migration

- **State**: `open`
- **Source**: progress-surfaced (DIVERGE — first-principles from GOAL.md ambition "Tooling compounds")
- **One-line summary**: Stamp every topic created with the template version it was generated against, and provide a migration path when the template gains new fields.
- **Why it matters**: The topic.md template has already evolved once (Follow-up goal + Research questions were added after health-longevity was created). Today the only way to detect that drift is eyeballing each topic.md. A simple `template_version: <semver>` in the topic frontmatter plus a `/research-migrate-templates` skill would surface and resolve drift across all topics in one pass — exactly the kind of compounding improvement the secondary lane should prefer.
- **Files likely affected**: `templates/topic.md` (add version frontmatter field), `.claude/skills/research-start/SKILL.md` (stamp version on create), new `.claude/skills/research-migrate/SKILL.md`.
- **Verdict**: Borderline
- **Scoring**: Indirect goal-alignment (tooling-compounds, but mostly hygiene). Medium-low leverage today — only 2 topics exist and ad-hoc retrofits have worked so far. Medium-large cost (schema decision + new migration skill + invariant for already-created topics). Borderline rather than archive because the underlying need is real and will become acute when topic count grows — revisit after the next template-changing event or once topic count is ≥ 5. Premature now; not wrong.
- **Evidence**: [topics/health-longevity/log.md](../topics/health-longevity/log.md) lines 32-36 (retrofit adding new fields to an already-created topic).

## cross-topic-source-and-finding-linking

- **State**: `open`
- **Source**: progress-surfaced (DIVERGE — first-principles from GOAL.md ambition "Tooling compounds")
- **One-line summary**: Allow facts and sources to reference each other across topics (not just within a parent ↔ subtopic), so overlapping research (e.g., sleep showing up in both `health-longevity` and a future productivity topic) doesn't refetch or redocument the same evidence.
- **Why it matters**: As the topic count grows, evidence overlap will grow with it. The current librarian works within a topic tree; there is no concept of a shared evidence pool. Without one, the user pays the cost of duplicate gathers and risks divergent summaries of the same underlying source. A global sources index plus `see_also: <topic>#fact:N` cross-links would compound the value of every earlier topic's work into every later topic's gather.
- **Files likely affected**: New `sources/index-global.json` (or similar), `.claude/agents/librarian.md` (cross-topic mode), `.claude/agents/source-scout.md` (check global index before fetching).
- **Verdict**: Borderline
- **Scoring**: Direct long-run goal-alignment to **tooling-compounds**, with the highest possible upside as topic count grows. But zero leverage today — only one topic has real content, no observed overlap to dedupe. Large architectural cost: global index schema, librarian cross-topic mode, source-scout dedup-against-global. Verified gap: `librarian.md` is strictly scoped to one topic tree (parent + subtopics), no cross-topic affordance. Borderline rather than archive because the candidate is correct in principle — just out of phase. Re-evaluate when topic count ≥ 4 and at least one cross-topic overlap is observed.
- **Evidence**: Currently 0 topics share sources; `.claude/agents/librarian.md` inputs are scoped to `topics/<slug>/` + its `subtopics/*` only.

<!--
Template for a new entry — kept for future hand-authored additions:

## <short-slug>

- **State**: `open` | `in-progress` | `done` | `archived`
- **Source**: user-note | digest-promoted | progress-surfaced
- **One-line summary**: what the improvement is.
- **Why it matters**: which research-lane pain point this would relieve, or which value in GOAL.md it advances.
- **Files likely affected**: `.claude/skills/<skill>/SKILL.md`, `.claude/agents/<agent>.md`, `templates/<file>`.
- **Verdict**: Pending | Pass | Borderline | Archive
-->
