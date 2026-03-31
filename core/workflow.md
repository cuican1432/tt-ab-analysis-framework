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

## Live Libra Branch

Use live Libra extraction only when:

- the task explicitly requires live report reading,
- the available docs are insufficient,
- or a validation task requires DOM-backed extraction.

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
