# Open Questions — Health and Longevity

Gaps the current 11 sources don't resolve. Each question is specific — re-run `/research-gather` with targeted seed queries to address any of these.

## Agent-added mechanisms to source properly

The highest-priority gap: 33 of the 42 facts in `facts.json` have mechanisms labeled *(added by agent)*. Each one should be replaced with a primary-source citation from a physiology textbook or mechanistic review. Grouped by mechanism family:

### Nutrition → cardiometabolic & brain
- **[fact:1, 3, 4]** Fiber → gut SCFAs → inflammation reduction; unsaturated-fat lipid effects; polyphenol oxidative-stress effects. *Needs:* mechanistic review on diet quality and systemic inflammation (IL-6, CRP).
- **[fact:4]** High-GI → postprandial glucose/insulin spikes → de novo lipogenesis → insulin resistance. *Needs:* metabolism textbook citation or GI/glycemic-load mechanistic review.
- **[fact:5]** Diet pathways are orthogonal to longevity-gene pathways. *Needs:* review on gene-diet interaction and epistasis in longevity.
- **[fact:17, 18, 20]** Mediterranean/MIND, saturated fat, whole grains → cerebrovascular and cognitive effects. *Needs:* neuronutrition mechanistic review.
- **[fact:19]** Epicatechin → cerebral blood flow via endothelial NO signaling. *Needs:* flavonoid pharmacology review.
- **[fact:21]** Bundled mechanism of the WHO dietary targets. *Needs:* single review tying fiber/fat/sugar targets to outcomes.

### Exercise → cardiometabolic & musculoskeletal
- **[fact:7]** Aerobic training → cardiac output, endothelial function, mitochondrial density, BP, insulin resistance. *Needs:* exercise physiology review of aerobic training adaptations.
- **[fact:8, 25]** Resistance training → mTOR protein synthesis, type-II fiber preservation, BMD. *Needs:* resistance training physiology review.
- **[fact:10, 22, 23]** Curvilinear dose-response mechanism (why early exercise corrects biggest deficits). *Needs:* review on VO2max/insulin-sensitivity gain curves.
- **[fact:24]** Why benefits plateau at 1–2 strength sessions/week and disappear at 7+. *Needs:* overtraining / recovery-window review.
- **[fact:26]** Total weekly volume drives adaptation independent of frequency. *Needs:* primary mechanistic citation for volume-equating.
- **[fact:27]** Time-efficient options each sum to same total weekly stimulus. *Needs:* head-to-head RCT or review.

### Sleep & cognition
- **[fact:28, 30]** Glymphatic clearance of beta-amyloid during slow-wave sleep; memory consolidation during SWS + REM. *Needs:* glymphatic system review (e.g. Iliff/Nedergaard) and Walker-group memory consolidation review.
- **[fact:29]** Long sleep: causal vs reverse-causation mechanism. *Needs:* review specifically on the long-sleep tail.
- **[fact:31]** Sleep-disordered breathing → intermittent hypoxia → cerebrovascular damage. *Needs:* OSA/vascular cognitive impairment review.

### Sedentary behavior & desk work
- **[fact:9, 32, 33]** Prolonged sitting → LPL suppression → impaired triglyceride clearance and postprandial glucose handling. *Needs:* Hamilton lab mechanistic work on inactivity physiology (the canonical citation for this mechanism).

### Mindfulness
- **[fact:36]** Brief programs ≈ long programs because early practice effects saturate the attention-regulation benefit. *Needs:* neuroimaging dose-response study.

### Lifestyle bundling
- **[fact:12, 13, 14, 15]** Why five lifestyle factors act on independent pathways and why effects compound. *Needs:* integrative review on multi-factor mortality risk additivity.
- **[fact:37, 38, 39]** Behavior-change mechanism: shared self-monitoring/goal-setting infrastructure; diet being smaller decision surface than PA; nicotine dependence requiring targeted support. *Needs:* behavioral economics / habit-formation review.

### Caffeine / energy drinks
- **[fact:40, 41]** Adenosine-receptor blockade → sleep onset delay + reduced SWS density; tolerance does not eliminate the effect. *Needs:* caffeine pharmacology review.

## Content gaps still open

- **Sleep hygiene for students specifically** — sources 006 and 010 cover cognitive effects and the caffeine-sleep loop, but not structured sleep hygiene protocols (fixed wake time, light exposure, cool room, blue-light management, pre-sleep wind-down). *Needs:* targeted search for student/young-adult sleep hygiene RCTs.
- **Q7 student pitfalls beyond energy drinks** — alcohol / binge drinking (Patrick 2016 mentioned but not extracted), vaping/nicotine, all-nighters, delayed sleep phase, chronic stress from course load. *Needs:* targeted search.
- **Stress beyond mindfulness** — sleep as a stress buffer, exercise as an acute stress reducer, social support effects on HPA axis. Source 008 covers mindfulness RCTs but not the broader stress landscape. *Needs:* stress physiology or HPA-axis review.
- **Alcohol dose-response** — fact 14 mentions "moderate/no alcohol" but no single source in the corpus quantifies the dose-response curve or addresses the recent "no safe amount" re-analyses. *Needs:* up-to-date alcohol-mortality meta-analysis (the Zhu 2022 / GBD 2022 line of work).
- **Time-of-day and circadian effects** — when to eat, when to train, when to study for cognitive/metabolic performance. Not covered at all. *Needs:* targeted search on chrononutrition / chronotraining.
- **Protein targets** — no source in the corpus gives a protein-per-kg recommendation for healthy adults engaged in resistance training. *Needs:* protein/leucine review (Phillips, Morton).
- **Cognitive effects of acute exercise** — Q2 was framed as "exercise for cognitive performance" but the corpus only covers long-term cognitive decline prevention. The acute "exercise → 30 minutes of sharper focus" literature is not covered. *Needs:* acute-exercise cognition review.

## Scope decisions deferred

- **Specific meal examples for affordable student budgets** — the research corpus gives principles, not dishes. This is a product-generation task, not a research gap.
- **Specific gym vs home vs bodyweight choices** — the exercise corpus gives dose, not modality selection. Product-generation task.
- **Time-blocking for an EE course load** — follow-up goal specific; belongs in the product-builder phase.
