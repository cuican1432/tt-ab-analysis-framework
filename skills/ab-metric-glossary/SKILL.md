---
name: ab-metric-glossary
description: Metric glossary and interpretation helper for A/B experiments. Use when you need metric definitions, safe plain-language meanings, confusing-neighbor disambiguation, or group-level recall support.
---

# AB Metric Glossary

Use this skill when the task involves:

- understanding a metric name,
- distinguishing similar metrics,
- mapping a metric to its likely business meaning,
- deciding whether a metric group should be recalled,
- or supporting Stage B / C interpretation with safer metric language.

Read these framework files first:

- `../../core/index.md`
- `../../core/rules.md`

Use these knowledge files as the primary source:

- `../../knowledge/metric_glossary.md`
- `../../knowledge/business_kb.md`

## Core role

- Clarify metric meanings.
- Separate near-neighbor metrics.
- Support group-level recall decisions.
- Help convert raw metric labels into safe, plain-language explanations.

## Usage rules

1. Start from the exact metric name shown in the source.
2. Prefer literal meaning first.
3. Then use glossary knowledge and business knowledge to refine the meaning.
4. If two metrics look similar, keep them separate unless the source explicitly proves they are the same row.
5. If the meaning is still uncertain, keep the explanation conservative.

## Recall rules

- `P0` metrics are must-recall.
- `P1` and `P2` metrics are business-aware recall items.
- Group-level recall should not override explicit PRD facts.
- Glossary hints support recall; they do not replace the experiment source of truth.

## Output style

- Prefer short, safe definitions.
- Prefer plain language over jargon when the meaning is stable.
- If the metric meaning is uncertain, say what can be confirmed and what remains ambiguous.

## Guardrails

- Do not invent product-specific meaning that is not supported by the metric name or glossary entry.
- Do not collapse different metrics into one interpretation just because they sound related.
- Do not treat glossary guidance as stronger than source data.
