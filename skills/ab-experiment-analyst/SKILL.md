---
name: ab-experiment-analyst
description: Rigorous A/B experiment analyst for doc-sourced or live-report A/B cases, PRDs, report drafting, and evals. Use when you need strict experiment analysis, report writing, or D-style evaluation.
---

# AB Experiment Analyst

Use this skill for A/B experiments when the task is to read a PRD or raw-data document, extract report facts, write an experiment report, or evaluate a draft against an eval set.

If you want more context, read these framework files:

- `./references/core/index.md`
- `./references/core/workflow.md`
- `./references/core/rules.md`
- `./references/core/memory.md`
- `./references/core/runbook.md`
- `./references/core/tooling.md`

Use these knowledge files as needed:

- `./references/knowledge/metric_glossary.md`
- `./references/knowledge/business_kb.md`

## Core posture

- Be strict and conservative.
- Never invent missing metrics, setup fields, or conclusions.
- If a metric is not significant, keep the wording directional.
- If data is missing, write `[missing]` or `data missing`.
- Treat PRD facts as the source of truth for experiment object and metric priority.
- Finished tables, conclusions, and reports from one experiment belong to that experiment only.
- Prefer telling the user clearly what can be confirmed, what cannot be confirmed, and what remains directional.

## Standard workflow

1. Read the experiment inputs first.
   - Prefer PRD, raw-data document, and any user-provided tables or screenshots.
   - If the source is a Lark doc, prefer the built-in Lark reading path first, for example `mcp__proxy___mira_py__read_lark_content`.
   - If the Lark tool cannot read the needed body content, fall back to browser reading.
   - If browser reading is needed, default to the Playwright MCP browser path.
   - If live report access is explicitly required, keep that as a separate extraction branch rather than the default path.
   - If the PRD includes product images, UI mocks, or visual diff tables and the runtime can read images, include them in source reading.
2. Consult the glossary.
3. Read the PRD.
4. Build the metric recall set.
5. Extract Stage A only from the relevant source.
6. Write Stage B.
7. Write Stage C.
8. Evaluate Stage D when required.

## Deliverable expectations

- Stage A should stay source-faithful and fresh.
- Stage B should convert raw source into a clean analysis skeleton.
- Stage C should answer the decision question first, then show evidence, risks, attribution, and boundaries.
- Stage D should score the current report against the requested eval set without backfilling missing source data.

## Evidence discipline

- Global evidence should drive the decision.
- Multi-dimensional evidence should explain why the global result holds.
- A single extreme slice should only be used as supporting evidence.
- Keep risk and benefit at the same level of visibility.
- For segment judgment, prefer consistency over isolated significance.
- When a clear `A -> B -> C` path exists, it is usually the easiest attribution chain to close cleanly.

## Report writing spirit

- Answer the decision question first, then show the evidence.
- Organize by business meaning, not by mechanically replaying source sections.
- Treat the report as a decision memo:
  - what happened,
  - why it matters,
  - what risks remain,
  - what action is reasonable now.
- For multi-arm experiments, do not stop at arm-by-arm summaries; add an explicit comparison section that states which arm is better overall, which is weaker, and why.
