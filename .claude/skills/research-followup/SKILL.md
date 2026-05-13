---
name: research-followup
description: Spawn a sub-research thread under an existing topic to go deep on a specific question. Use when the user runs `/research-followup <parent> <subtopic>` or asks to start a sub-research / drill into a sub-question.
---

# research-followup

Creates a new subtopic under an existing parent topic. Subtopics live at `topics/<parent>/subtopics/<sub-slug>/` and mirror the structure of a topic folder (topic.md, log.md, sources/, summaries/). They are researched with the same pipeline as a top-level topic, but their findings flow back up into the parent via the librarian.

## Arguments

- `<parent>` — slug of an existing topic folder
- `<subtopic>` — short slug for the new sub-research (e.g. `sleep`, `protein-targets`)

If either argument is missing, ask the user.

## Preconditions

- `topics/<parent>/topic.md` exists.
- `topics/<parent>/summaries/summary.md` exists — a subtopic should only spawn after the parent has at least one summary, so the follow-up has context. If no parent summary exists, stop and tell the user to run `/research-summarize` on the parent first.
- `topics/<parent>/subtopics/<sub-slug>/` does not already exist. If it does, tell the user to use `/research-gather` or `/research-summarize` on the existing subtopic instead.

## Process

1. **Scaffold the subtopic folder** from `templates/`:
   - `topics/<parent>/subtopics/<sub-slug>/topic.md` — seeded from the subtopic template (see below)
   - `topics/<parent>/subtopics/<sub-slug>/log.md` — empty with a `start` entry
   - `topics/<parent>/subtopics/<sub-slug>/sources/{web,user,transcripts}/` — empty
   - `topics/<parent>/subtopics/<sub-slug>/sources/index.json` — `{"sources": []}`
   - `topics/<parent>/subtopics/<sub-slug>/summaries/` — empty

2. **Seed `topic.md`.** The subtopic template has the same shape as a topic but adds a `parent` field and an `inherits_follow_up_goal_from` field defaulting to the parent. Ask the user to supply the research questions for the subtopic — do NOT invent them. Confirm with the user what the subtopic should answer before you exit the skill.

3. **Link from the parent.** Append an entry in parent `open-questions.md` (or note in parent `topic.md` under "Deep dives in progress") saying this subtopic is now active: `- [subtopics/<sub>/topic.md](subtopics/<sub>/topic.md) — active, <one-line scope>`.

4. **Append to parent log.md:**
   ```
   ## followup-spawned — <date>
   - subtopic: <sub-slug>
   - seeded research questions: N
   - next: run /research-gather on the subtopic
   ```

5. **Stop.** Tell the user:
   - Path to the new `subtopics/<sub>/topic.md` as a clickable link
   - Next command: `/research-gather <parent>/<sub>` to start gathering sources inside the subtopic
   - Reminder that they should review the seeded research questions in the subtopic's `topic.md` before gathering

## Subtopic topic.md template

```markdown
---
topic: "<parent human name> — <sub human name>"
slug: "<sub-slug>"
parent: "<parent-slug>"
inherits_follow_up_goal_from: "<parent-slug>"
created_at: "<date>"
status: "scoping"
source_target: 5
---

# <parent> / <sub> — Topic Scope

## Inherited follow-up goal

<copy verbatim from parent topic.md>

## Subtopic goal

<one paragraph — why this subtopic exists, what gap in the parent it's filling>

## Research questions

<numbered list supplied by the user — do not invent>

## Scope in

## Scope out

## Credibility filters

Same as parent unless noted.

## Notes
```

## Do not

- Do not start gathering sources in this skill. This skill only scaffolds and sets up the research questions.
- Do not invent research questions. Ask the user.
- Do not run without a parent summary — a subtopic with no parent context is just a topic, and should be scaffolded with `/research-start` instead.
