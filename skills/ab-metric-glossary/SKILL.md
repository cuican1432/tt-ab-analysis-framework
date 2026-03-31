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

If you want more context, read these framework files:

- `./references/core/index.md`
- `./references/core/rules.md`

Use these knowledge files as the primary source:

- `./references/knowledge/metric_glossary.md`
- `./references/knowledge/business_kb.md`

## Core role

- Clarify metric meanings.
- Separate near-neighbor metrics.
- Support group-level recall decisions.
- Help convert raw metric labels into safe, plain-language explanations.
- Organize messy source knowledge into a reusable glossary draft.

## Usage rules

1. Start from the exact metric name shown in the source.
2. Prefer literal meaning first.
3. Then use glossary knowledge and business knowledge to refine the meaning.
4. If two metrics look similar, keep them separate unless the source explicitly proves they are the same row.
5. If the meaning is still uncertain, keep the explanation conservative.
6. If the user provides a large knowledge-base doc instead of a clean dictionary, first organize it into a structured glossary draft.
7. Leave uncertain fields blank instead of guessing, and show the user which fields still need confirmation.
8. After user review, merge the confirmed content into the formal glossary.
9. Do not expect the user to discover all gaps alone; print a short, explicit `to confirm` list.

## Draft structure

When building or updating a glossary draft, prefer this structure:

1. metric group index
2. metric index
3. dimension index
4. optional dimension value index

Keep the levels separate. Do not mix group descriptions, metric meanings, and dimension definitions into one flat block unless the source itself is too small to justify structure.

## Recall rules

- `P0` metrics are must-recall.
- `P1` and `P2` metrics are business-aware recall items.
- Group-level recall should not override explicit PRD facts.
- Glossary hints support recall; they do not replace the experiment source of truth.

## Output style

- Prefer short, safe definitions.
- Prefer plain language over jargon when the meaning is stable.
- If the metric meaning is uncertain, say what can be confirmed and what remains ambiguous.
- For long knowledge-source cleanups, return:
  - the structured draft,
  - the fields intentionally left blank,
  - and a short `to confirm` list for the user.
- Prefer grouping `to confirm` items into:
  - must confirm,
  - should confirm,
  - optional follow-up,
  when that makes the review easier.

## Guardrails

- Do not invent product-specific meaning that is not supported by the metric name or glossary entry.
- Do not collapse different metrics into one interpretation just because they sound related.
- Do not treat glossary guidance as stronger than source data.
- Do not force every field to be filled. Blank is better than guessed.
- Do not hide uncertainty inside the draft; surface it as a review list.
