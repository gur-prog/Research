---
name: research-gather
description: Gather sources for an existing research topic. Use when the user runs `/research-gather` or asks to collect/fetch sources for a topic. Delegates to the source-scout subagent to hit the source_target set in topic.md.
---

# research-gather

Runs the source-gathering phase for a topic. The heavy lifting is done by the `source-scout` subagent — this skill's job is to identify the active topic, check preconditions, invoke the agent, and report results.

## Determining the active topic

In priority order:
1. If the user passed a slug as an argument (`/research-gather health-longevity`), use that.
2. If there's exactly one folder under `topics/`, use it.
3. Otherwise, list existing topics under `topics/` and ask the user which one.

## Preconditions (refuse to run if any fail)

- `topics/<slug>/topic.md` must exist.
- Its `status` frontmatter should be `scoping` or `gathering`. If it's further along (`summarizing`, `ready`, etc.), ask the user to confirm they really want to add more sources — re-gathering mid-summary can invalidate existing facts.
- The Goal section in `topic.md` must be filled (not still the placeholder). If it looks like the template text, stop and tell the user to edit `topic.md` first.

## Process

1. **Flip status to `gathering`** in `topic.md` frontmatter.

2. **Invoke `source-scout`** via the Agent tool with this prompt (adapt as needed):

   > Gather sources for the topic at `topics/<slug>/`. Read its `topic.md` for scope, source target, seed queries, seed URLs, and credibility floor. Dedupe against `sources/index.json`. Respect the source target — do not exceed it. Save each source to `sources/web/<id>.md` using `templates/source.md`, update `sources/index.json`, and append a gather entry to `log.md`. Report back with the new total vs. target and any warnings.

3. **Wait for the agent to finish.** Read its report.

4. **If the agent couldn't reach the target:** relay that to the user verbatim — don't paper over it. Suggest options (widen scope, add seed URLs, raise credibility floor allowances).

5. **If the target was reached:** flip `topic.md` status to `ready-to-summarize` and tell the user to run `/research-summarize` next.

## Output

A short report to the user:
- Sources added this run / total / target
- Credibility breakdown
- Any warnings from the agent
- Next step: `/research-summarize`
