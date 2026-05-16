# rq-preflight-at-start — L2 design

**Parent**: [backlog/agent-improvements.md#rq-preflight-at-start](../agent-improvements.md) — L1 verdict `Pass`.

## Parent driver

At `/research-start`, require the user to fill in `Goal` + `Follow-up goal` + research questions before the topic is considered ready for `/research-gather` — refuse to gather against template placeholders. Health-longevity needed a retrofit to add RQs; methodical-innovation is currently blocking the primary lane on exactly this gap. `source-scout` already depends on RQs existing (step 2 treats them as coverage checklist).

## Open design questions (seeds for L2 DIVERGE)

- Where does the check live? (`research-start` finalization step? Precondition in `research-gather`? Both?)
- What counts as "filled in"? (Non-empty? At least N RQs? RQs that pass a triviality filter?)
- How does the user get prompted? (Refuse-with-message? Interactive elicitation? Suggest RQs from Goal text?)
- Should `templates/topic.md` mark fields explicitly required vs optional?
- What about existing topics with placeholder fields — do they get a migration warning?

## Candidates

*(Empty — populated by future L2 DIVERGE iteration.)*
