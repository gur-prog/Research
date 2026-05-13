---
name: research-integrate
description: Run the librarian agent to propose or apply integration of subtopic findings into a parent topic. Use when the user runs `/research-integrate <topic>` or `/research-integrate <topic> --apply`.
---

# research-integrate

Thin wrapper around the `librarian` agent. Two modes:

- **Proposal mode** (`/research-integrate <topic>`): run the librarian, which scans the tree and writes `topics/<topic>/pending-integration.md` with proposed contradictions, promotions, supersessions, hygiene flags, and open-questions updates. If there is nothing to integrate, the librarian deletes any stale `pending-integration.md` and you tell the user "tree is already coherent".

- **Apply mode** (`/research-integrate <topic> --apply`): run the librarian in apply mode. It reads `pending-integration.md` (which the user may have pruned), executes the surviving proposals by mutating `summary.md`, `facts.json`, and `open-questions.md`, appends a log entry, and deletes `pending-integration.md`.

## Arguments

- `<topic>` — slug of an existing top-level topic. If missing and there's only one topic in the repo, default to it; else ask.
- `--apply` — optional flag to execute the pending proposals.

## Preconditions

- `topics/<topic>/summaries/summary.md` exists.
- For `--apply`: `topics/<topic>/pending-integration.md` exists. If it doesn't, stop and tell the user there is nothing to apply.

## Process — proposal mode

1. **Invoke `librarian` in proposal mode** via the Agent tool:

   > Run an integration pass on `topics/<topic>`. Scan subtopics, flag contradictions, propose promotions/supersessions/hygiene flags, and write `topics/<topic>/pending-integration.md`. Proposal-only — do not mutate.

2. **Report to the user:**
   - "Proposal written" with clickable link to `pending-integration.md`, OR "Tree is coherent — nothing to integrate"
   - Proposal counts (contradictions, promotions, supersessions, hygiene flags, open-question updates)
   - Next command: review `pending-integration.md`, optionally prune proposals you don't want, then run `/research-integrate <topic> --apply`

## Process — apply mode

1. **Confirm `pending-integration.md` exists.** If not, stop.

2. **Invoke `librarian` in apply mode:**

   > Apply proposals in `topics/<topic>/pending-integration.md`. Mutate `summary.md`, `facts.json`, and `open-questions.md` according to the surviving proposals. Append a log entry documenting every change. Delete `pending-integration.md` on success.

3. **Report to the user:**
   - Count of each change type actually applied
   - Clickable link to updated `summary.md`
   - Reminder that subtopic files were not touched (subtopic coherence is the subtopic's own pass)

## Do not

- Do not bypass the librarian. This skill is a thin orchestrator; all scan/mutate logic belongs to the agent.
- Do not apply without an existing `pending-integration.md`. The approval artifact is the pruned file.
- Do not run on a subtopic directly — integration is always against a parent topic, and a subtopic's findings flow upward via the parent's integration pass.
