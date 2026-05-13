---
name: research-summarize
description: Extract facts from gathered sources and synthesize a summary. Use when the user runs `/research-summarize` or asks to summarize / synthesize a topic's research. Stops for user review before products are built.
---

# research-summarize

Runs the summarization phase. Three sub-steps, all delegated to subagents:

1. **Fact extraction** — `source-reader` agent runs once per source to fill `summaries/facts.json`.
2. **Synthesis** — `synthesizer` agent reads all facts and writes the three-layer `summary.md` (Synthesis → Themes+Grounded-in → Deep dives) + `open-questions.md`.
3. **Auto-integration** — `librarian` agent runs automatically against the parent topic after synthesis and writes `pending-integration.md` at the topic root if integration is needed, or deletes any stale one if not. Librarian is proposal-only; it never mutates.

This skill **stops for user review** after step 3. Do not proceed to product generation.

## Parent vs. subtopic runs

- **Parent topic run** (`/research-summarize health-longevity`): operates on `topics/health-longevity/`. Librarian scans all of its subtopics for integration back into the parent.
- **Subtopic run** (`/research-summarize health-longevity/sleep`): operates on `topics/health-longevity/subtopics/sleep/`. After synthesis, librarian runs against the **parent** (`health-longevity`) to integrate the new subtopic findings upward.

## Determining the active topic

Same rules as `research-gather`: argument → single topic → ask.

## Preconditions

- `sources/index.json` exists and has at least one source.
- `topic.md` exists.
- If `summaries/summary.md` already exists, ask the user: overwrite, or stop? Re-running summarize means existing facts may be re-processed, which is fine, but the old `summary.md` will be replaced.

## Process

1. **Flip `topic.md` status to `summarizing`.**

2. **Enumerate sources.** List every file under `sources/web/`, `sources/user/`, and `sources/transcripts/` that appears in `sources/index.json` and isn't already fully processed. (A source is "processed" if `facts.json` contains at least one fact whose `source_ids` includes this source's id.)

3. **For each unprocessed source, invoke `source-reader`** via the Agent tool:

   > Read `topics/<slug>/sources/<path>/<file>` and extract factual claims as structured records. Append to `topics/<slug>/summaries/facts.json`. Follow the rules in your agent definition. Report facts added and any claims you skipped as too vague.

   These invocations can be run in parallel when there are many sources — each reader touches the same `facts.json` file, so if you parallelize, serialize the writes by reading-appending-writing carefully, or run them sequentially for safety. **Default to sequential** unless you're confident in the concurrency behavior.

4. **Once all sources are processed, invoke `synthesizer`:**

   > Synthesize `<path>/summaries/facts.json` into the three-layer `summary.md` and `open-questions.md`. Read `topic.md` for follow-up goal + research questions. Preserve any existing layer-1 paragraphs stamped `author: librarian` or `from: subtopic:*`. Cite every claim.

5. **Auto-chain the librarian.** After synthesis completes, invoke `librarian` in proposal mode against the parent topic:

   > Run an integration pass on `topics/<parent-slug>`. Scan all subtopics under `subtopics/` against parent synthesis and facts. Write proposals to `topics/<parent-slug>/pending-integration.md`, or delete any stale file if nothing needs integrating. Proposal-only — do not mutate.

6. **Flip `topic.md` status to `ready`.**

7. **Stop for user review.** Do not proceed to `/research-product`. Your final message must tell the user to read `summary.md`, and — if `pending-integration.md` exists — to review it and run `/research-integrate <parent> --apply` or edit the file first to accept a subset.

## Output

Tell the user:
- Number of sources processed
- Number of facts extracted
- Path to `summary.md` as a clickable link
- Path to `open-questions.md` as a clickable link
- **Explicit instruction to review `summary.md` before running `/research-product`.** If they see gaps, they can re-run `/research-gather` with more sources or edit `topic.md` scope.
