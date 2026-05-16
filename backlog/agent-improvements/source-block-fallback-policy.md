# source-block-fallback-policy — L2 design

**Parent**: [backlog/agent-improvements.md#source-block-fallback-policy](../agent-improvements.md) — L1 verdict `Pass`.

## Parent driver

Codify the source-substitution rules when a fetched URL returns 303 / 403 / timeout, so `source-scout` doesn't have to improvise per run. Every gather hits blocked URLs eventually — health-longevity hit two in two rounds. The fix lives in `.claude/agents/source-scout.md` (no HTTP-failure handling spec today) and `.claude/skills/research-gather/SKILL.md`.

## Open design questions (seeds for L2 DIVERGE)

- What's the retry budget per URL? (0 retries? 1 retry after backoff?)
- What's the substitution preference order? (PMC mirror first? Alternate journal mirror? Author preprint? Abandon and re-search?)
- When do we abandon a search lead vs. swap source? (Block count threshold?)
- What goes in the log when a substitution happens? (Original URL, substitute URL, HTTP code, reason — schema?)
- Does this differ by credibility tier? (Peer-reviewed gets more retries than blog?)

## Candidates

*(Empty — populated by future L2 DIVERGE iteration.)*
