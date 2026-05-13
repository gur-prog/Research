# Research

A personal research agent built on Claude Code. You name a topic, it gathers credible sources, produces a reviewed summary, and turns that summary into usable products (meal plans, workout routines, rule books, checklists).

## How it works

Research runs in four staged phases. Each phase is a slash command. You review between phases so bad research never becomes bad products.

```
/research-start <topic>    → scaffold topic folder, edit scope
/research-gather           → collect sources (web, user files, transcripts)
/research-summarize        → extract facts and synthesize a summary  ◀ REVIEW HERE
/research-product <type>   → generate a product from the summary
```

**Summaries are the source of truth.** Products are derived purely from [topics/<topic>/summaries/](topics/) — you can tweak a product template and regenerate without re-fetching the web.

## Layout

```
topics/<topic>/
  topic.md             scope, intended products, source target
  log.md               timeline of actions
  sources/
    web/               fetched web pages (one .md per source)
    user/              URLs and PDFs you drop in manually
    transcripts/       YouTube / podcast transcripts
    index.json         catalog of all sources
  summaries/
    summary.md         synthesis with citations like [fact:42]
    facts.json         structured claims linked back to source ids
    open-questions.md  gaps the agent couldn't resolve
  products/
    <name>.md          markdown product
    <name>.json        machine-readable twin
    checklists/        daily/weekly trackers
    pdf/               rendered PDFs (if pandoc is installed)
```

## Quickstart

1. `/research-start health-longevity`
2. Open [topics/health-longevity/topic.md](topics/) and edit scope, `source_target`, and intended products.
3. (Optional) Drop URLs or PDFs into `topics/health-longevity/sources/user/`.
4. `/research-gather`
5. `/research-summarize` — then **read `summary.md` and decide if it's good enough**.
6. `/research-product meal-plan` (and any others you listed in `topic.md`).

## Reproducibility invariant

Every claim in a product traces: `product → summary citation → facts.json entry → source file`. If you ever ask "why does this plan recommend X?", you can follow the citation all the way back to the page it came from.
