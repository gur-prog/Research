---
name: research-start
description: Scaffold a new research topic folder. Use when the user runs `/research-start <topic-name>` or asks to start researching a new topic. Creates the topic folder from templates and prompts the user to edit topic.md before gathering.
---

# research-start

Scaffolds a new topic folder under `topics/<slug>/` and leaves the user with a `topic.md` to edit before the next phase.

## Inputs

The user provides a topic name as an argument — e.g. `/research-start health and longevity`. Derive a slug: lowercase, spaces and punctuation → hyphens, strip non-alphanumerics.

Example: `"Health and Longevity"` → `health-and-longevity`.

## Process

1. **Validate.** If `topics/<slug>/` already exists, stop and tell the user — don't overwrite. Ask whether they want to resume (no action needed) or pick a new slug.

2. **Create the folder structure:**
   ```
   topics/<slug>/
     sources/
       web/
       user/
       transcripts/
     summaries/
     products/
       checklists/
       pdf/
   ```
   Since git and most tools don't track empty folders, drop a `.gitkeep` file in each empty leaf folder.

3. **Create `topic.md`** by copying `templates/topic.md` and replacing the placeholders:
   - `{{TOPIC_NAME}}` → the human-readable topic name the user gave
   - `{{TOPIC_SLUG}}` → the slug
   - `{{CREATED_AT}}` → today's date in `YYYY-MM-DD` format

4. **Create an empty `log.md`** in the topic folder with a single header:
   ```
   # Log — <Topic Name>
   ```

5. **Initialize `sources/index.json`** as:
   ```json
   { "sources": [] }
   ```

6. **Append to `log.md`:**
   ```
   ## start — <timestamp>
   - slug: <slug>
   - created folder structure
   ```

## Output

Tell the user:
- Path to the new `topic.md` as a clickable link
- That they should edit it to set Goal, Scope, Intended products, and (optionally) Seed queries/URLs before running `/research-gather`
- Remind them they can drop URLs or PDFs into `topics/<slug>/sources/user/` for the agent to consume

Do NOT run `/research-gather` automatically — the user needs to review scope first. That's the point of the staged workflow.
