---
name: research-product
description: Generate a product (meal-plan, workout-routine, rulebook, checklist, or other) from a topic's summary. Use when the user runs `/research-product <type>` or asks to build/generate a product. Reads only the summary — never re-fetches sources.
---

# research-product

Runs the product generation phase. Delegates to the `product-builder` subagent.

## Inputs

- Product type as an argument: `/research-product meal-plan`
- (Optional) topic slug as a second argument: `/research-product meal-plan health-longevity`

## Determining the active topic

Same rules as the other skills: argument → single topic → ask.

## Preconditions (refuse to run if any fail)

- `topics/<slug>/summaries/summary.md` must exist. If it doesn't, tell the user to run `/research-summarize` first — don't try to improvise.
- `topics/<slug>/summaries/facts.json` must exist and be non-empty.
- `templates/product/<product-type>.md` must exist. If not, tell the user which product types are available (glob `templates/product/*.md`) and offer to create a new template if they describe what they want.
- The product type should appear in `topic.md`'s "Intended products" list. If not, warn the user but proceed if they confirm — it's their repo.

## Process

1. **Flip `topic.md` status to `producing`.**

2. **Invoke `product-builder`** via the Agent tool:

   > Generate a `<product-type>` product for the topic at `topics/<slug>/`. Read `summaries/summary.md`, `summaries/facts.json`, and `topic.md` for user constraints. Fill `templates/product/<product-type>.md` and also write a structured JSON twin. Follow the rules in your agent definition: no re-fetching, every claim cited, honor user constraints. Report back with paths to the generated files.

3. **After the agent returns, verify citations.** Quick sanity check: grep the generated `.md` for `[fact:` — if there are zero citations, something went wrong. Tell the user and stop.

4. **Render PDF if possible.** Check if `pandoc` is on PATH (`pandoc --version`). If yes, run:
   ```
   pandoc topics/<slug>/products/<name>.md -o topics/<slug>/products/pdf/<name>.pdf
   ```
   If pandoc isn't available, skip silently and note it in the report.

5. **Flip `topic.md` status back to `ready`** — the topic stays in `ready` state so the user can build additional products without re-running summarize.

## Output

Tell the user:
- Path to the generated `.md` product as a clickable link
- Path to the `.json` twin as a clickable link
- Whether PDF was rendered
- Number of facts cited
- Any gaps the agent flagged ("summary doesn't cover X well")
- Suggestion to run `/research-product <another-type>` for other products listed in `topic.md`
