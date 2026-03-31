# Workflow

## Default Order

Use this default order for experiment analysis:

1. Read the experiment inputs first.
   - Prefer PRD, raw-data docs, screenshots, and tables.
2. Consult the glossary.
   - Disambiguate metric names and metric groups.
3. Read the PRD carefully.
   - Identify experiment object, target metrics, guardrails, and mechanism clues.
4. Build the recall set.
   - Keep explicit targets.
   - Keep mechanism-implied metrics.
   - Keep core guardrails.
   - Keep important significant groups.
5. Write Stage B logic.
6. Write Stage C report.
7. Run Stage D evaluation when required.

## Knowledge Ingestion Loop

Use this default order for glossary / knowledge-base maintenance:

1. Read the raw knowledge source first.
   - Prefer a Lark knowledge base, glossary doc, table, or pasted text.
2. Organize it into a structured draft.
   - Split into metric groups, metrics, dimensions, and business notes when possible.
   - Treat business knowledge as index-first: locate the relevant topic first, then pull only the needed content.
3. Fill only what can be confirmed from the source.
4. Leave uncertain fields blank.
5. Print a `to confirm` list for the user.
   - Do not make the user discover gaps manually.
6. After user confirmation, partially ingest the confirmed parts.
   - Stable entries can move into the formal glossary / business knowledge files.
   - Unstable or incomplete entries should remain in `knowledge/drafts/`.
7. Repeat the loop as needed.
   - Knowledge ingestion is iterative, not all-or-nothing.

## Live Libra Branch

Use live Libra extraction only when:

- the task explicitly requires live report reading,
- a Libra link/page is explicitly provided,
- the available docs are insufficient,
- or a validation task requires DOM-backed extraction.

Treat live Libra extraction as a beta path. When a Libra source is involved, prefer this normal flow first:

1. open Libra `conclusion report`,
2. switch to the appropriate template,
3. export the document,
4. analyze the exported doc as the primary source.

When live Libra extraction is needed:

1. Open the browser in the same session.
2. Reuse the same stable tab when possible.
3. Prefer browser MCP / Playwright first.
4. Fall back to direct CDP only when the browser is already open but the gateway is unstable.

## Stage Boundaries

- `A`: extract facts from the source.
- `B`: organize logic and decision structure.
- `C`: write the final report.
- `D`: evaluate output against an eval set or checklist.

## Rerun Rule

- Do not rerun A casually.
- Only rerun A when the source facts, extraction output, or metric caliber are proven wrong.
- If A reruns, rebuild downstream stages from the new A.
- Never patch an old A with backfill numbers.
