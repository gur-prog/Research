# coverage-vs-source-target-policy — L2 design

**Parent**: [backlog/agent-improvements.md#coverage-vs-source-target-policy](../agent-improvements.md) — L1 verdict `Pass`.

## Parent driver

Define the relationship between `source_target` (a count in topic frontmatter) and research-question coverage (a checklist derived from the RQs) so `/research-gather` has a single clear stop condition. The current spec in `source-scout.md` step 8 covers two cases (target reached + coverage done; target reached + coverage incomplete) but is silent on the case observed in health-longevity gather-2 ("below target, coverage complete"). The agent stopped anyway — the rule should match the practice or the practice should change.

## Open design questions (seeds for L2 DIVERGE)

- Which is the primary stop condition — `source_target` (count) or full RQ coverage (quality)? Or some product of both?
- If coverage is the primary, what does `source_target` mean? (A floor? A budget cap? A hint?)
- What's "full coverage"? (≥1 source per RQ? ≥1 strong-trust source per RQ? Each RQ has at least one source AND the source actually answers the question?)
- What if a RQ is unanswerable from available sources — gather-stops? Or surfaces as open-question and continues?
- Does the policy interact with `mechanism-sourcing-followup-loop`? (A mechanism follow-up round may push past `source_target` legitimately.)
- Per-topic override allowed? (Some topics need way more sources than the default.)

## Candidates

*(Empty — populated by future L2 DIVERGE iteration.)*
