# GOAL — Research

*Last updated: 2026-05-13. Re-draft this file whenever the binding objective shifts.*

## What we're trying to do

This repo is a personal research agent built on Claude Code, used as a tool for the user to learn about things that matter to them. Two intertwined purposes: (1) accumulate genuine, well-sourced understanding on topics worth understanding, (2) strengthen the tooling (skills, agents, templates) as we learn what works. The first is the headline output; the second is the substrate that makes future research better. There are no deadlines — this is continuous work, focus shifts based on the user's interest, and any progress on any active topic is beneficial.

## Ambitions — what "correct" looks like

- **Every claim is true and traceable.** Products → summary citations → facts.json → source file. No fabricated papers, URLs, dates, or quotes. If evidence is missing, mark "research pending" rather than guess.
- **Readability is load-bearing.** A summary that's complex or irrelevant is useless. Products must be genuinely usable by the user — not neutral encyclopedias.
- **Tooling compounds.** Improvements to skills, agents, and templates carry across all future topics. A small upgrade that touches every topic going forward usually beats a one-off win on a single topic.
- **Knowledge accumulates and lands in real life.** Each active topic should reach the point where products are actually adopted (rulebooks read, meal plans followed, habits changed) — not just sit as written summaries.

## Values and constraints — what we will not trade

- **No hallucinations, ever.** Citations are not optional and never generated when convenient.
- **No autonomy past human-review gates.** The pipeline includes deliberate review points (notably between `summarize` and `product`, and at librarian integration proposals). `/progress` must not auto-cross these gates.
- **Summaries are the source of truth for products.** Products derive purely from `topics/<slug>/summaries/`; gather/summarize are not re-run on product regeneration.
- **No silent decision-making.** Which topic to retire, whether to promote a borderline source, whether to apply a librarian proposal — all surface and stop.

## Decisions already committed — the locked-in part of the goal

- **D000 (2026-04-12)** — **Four-phase pipeline: `start → gather → summarize → product`**, with explicit human review between `summarize` and `product`. Each phase is a slash command. The review gate prevents bad research from becoming bad products.
- **D001 (2026-04-12)** — **Summaries are the source of truth for products.** Products derive purely from `topics/<slug>/summaries/`. Tweaking a product template and regenerating does not re-fetch the web.
- **D002 (2026-04-12)** — **Reproducibility invariant.** Every product claim traces: `product → summary citation → facts.json entry → source file`. If any link is missing, the claim is broken.

## How this goal is pursued

This repo has two parallel lanes with a clear priority:

- **Primary lane — Research progression.** L1 = `roadmap/topics.md`, a roster of active research topics with state (`hot` / `blocked-on-user` / `cold` / `done`) and next action. L2 = each topic's own `topics/<slug>/topic.md` and pipeline state (sources gathered, summary present, products generated, subtopics spawned). L3 = subtopics under `topics/<slug>/subtopics/<sub>/`.
- **Secondary lane — Agent improvements.** L1 = `backlog/agent-improvements.md`. Touched when the user supplies notes, or when every research topic is blocked on user input. Lower default priority.

`/progress` picks the highest-leverage actionable iteration. If everything is blocked on the user, it surfaces the blockers and stops rather than inventing work.

## When this file changes

Changes when:
- A new committed decision shifts the locked-in part of the goal.
- An ambition or value statement is revised through deliberate conversation — not silent drift.
- The balance of lanes changes (e.g., "agent improvements are now primary for a while").

Does NOT change when:
- A topic is started, advanced, or retired → updates `roadmap/topics.md`.
- A topic's summary is regenerated → updates `topics/<slug>/summaries/`.
- A skill or agent is added → updates `.claude/skills/` or `.claude/agents/`.
