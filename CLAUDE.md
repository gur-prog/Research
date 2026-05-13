# CLAUDE.md — Research

*Project-level instructions for AI working in this repo. Loaded automatically by Claude Code on every session here. Cross-machine / cross-repo rules live in the user-level `~/.claude/CLAUDE.md`.*

## What this repo is for

A personal research agent built on Claude Code. Two intertwined purposes: (1) accumulate well-sourced understanding on topics the user cares about, (2) strengthen the tooling as we learn what works. The current binding constraint is **trust** — every claim must trace to a source, every product must be actually useful, and every decision the user reserves stays with the user.

See [GOAL.md](GOAL.md) for ambitions, locked-in decisions, and decision-tree shape.

## Reading scope — what to load when

**Default first read**: [GOAL.md](GOAL.md), [WORK_LOG.md](WORK_LOG.md) (specifically `## Lessons & active feedback`), [roadmap/topics.md](roadmap/topics.md).

**Expand to other files when**:
- Question about a specific topic's state → `topics/<slug>/topic.md`, `topics/<slug>/log.md`, and any `pending-integration.md`.
- Question about a topic's findings → `topics/<slug>/summaries/summary.md` (not the raw sources unless tracing a citation).
- Question about tooling → `backlog/agent-improvements.md`, then the relevant `.claude/skills/<skill>/SKILL.md` or `.claude/agents/<agent>.md`.

**Never load by default** (heavy; only when chasing a specific reference):
- `topics/<slug>/sources/web/*.md` — raw scraped sources. Read one only when verifying a specific citation.
- `topics/<slug>/summaries/facts.json` — load only when tracing facts to sources.

## Hard rules

Non-negotiable. The `/progress` skill and any other autonomous behavior must respect them.

- **Never cross the `summarize → product` review gate autonomously.** A topic with a fresh `summaries/summary.md` and no user signal that review is complete is **not** ready for `/research-product`. Surface readiness, do not auto-produce.
- **Never apply librarian integration proposals autonomously.** When `pending-integration.md` exists in a topic, that file is a proposal awaiting user review. `/progress` must surface it and stop — never run `/research-integrate <topic> --apply` without explicit instruction.
- **Never fabricate sources, citations, or facts.** If a claim lacks a citation, mark it "research pending" and surface. Every URL, paper, author, and date must come from an actual fetched source, never from training data.
- **Never auto-cold a topic.** Topics move from `hot` → `cold` only when the user explicitly says so. A stalled topic stays `hot` and gets surfaced as blocked.
- **Never auto-edit `GOAL.md`.** Re-drafting the goal is a deliberate-conversation event.
- **Never auto-edit a topic's `topic.md`** in its scope / goal / research-questions sections after creation. The user owns the scope; the agent owns gathering / summarizing / producing.
- **Never push to git** without explicit user confirmation.

## Decision tree shape

Two parallel lanes:

- **L1 — Research roster**: [roadmap/topics.md](roadmap/topics.md). One entry per topic with state, current phase, and next action.
- **L2 — Per-topic state**: `topics/<slug>/topic.md` (scope) + `topics/<slug>/log.md` (history) + `pending-integration.md` if present.
- **L3 — Subtopics**: `topics/<slug>/subtopics/<sub>/...` (same structure recursively).
- **Side lane — Agent improvements**: [backlog/agent-improvements.md](backlog/agent-improvements.md). L1 of the secondary lane.

`/progress` discovers the tree from these paths.

## Soft preferences

- Prefer terse, actionable updates in chat over verbose narration.
- Cite source-ids (`fact:N`, `subtopic:<slug>#fact:N`) when discussing findings, so the user can chase the chain back.
- When unsure whether an improvement is "research progress" or "agent improvement", default to research progress.

## Skills available in this repo

Under `.claude/skills/`: `research-start`, `research-gather`, `research-summarize`, `research-product`, `research-followup`, `research-integrate`, `lock`, `unlock`.

Under `.claude/agents/`: `source-scout`, `source-reader`, `synthesizer`, `librarian`, `product-builder`.

User-level skills (`/progress`, `/loop`, `/schedule`, etc.) are listed in `~/.claude/CLAUDE.md`.

## When in doubt

- If a request would cross a review gate the user reserves — stop, surface, ask.
- If evidence for a load-bearing claim is missing — mark "research pending" rather than guess.
- If you're about to write to a file you've never read — read it first.
