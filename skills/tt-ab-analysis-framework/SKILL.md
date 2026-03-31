---
name: tt-ab-analysis-framework
description: Main entry skill for TT A/B experiment work. Use when you want to ingest experiment knowledge, generate an experiment report, or apply temporary metric/rule guidance for a single run.
---

# TT AB Analysis Framework

Use this as the main user-facing skill for TT-style A/B experiment work.

Think of this skill as the single front door for three common jobs:

1. generate an experiment report
2. generate an experiment report with temporary metric / rule guidance
3. ingest reusable knowledge into the glossary / business knowledge layer

## Quick Start

### 1. Install

Clone the framework locally:

```bash
mkdir -p ~/ab-workspace
cd ~/ab-workspace
git clone https://github.com/cuican1432/tt-ab-analysis-framework.git
cd tt-ab-analysis-framework
```

For a Codex-style local install:

```bash
mkdir -p ~/.codex/skills/tt-ab-analysis-framework
cp -R skills/tt-ab-analysis-framework/. ~/.codex/skills/tt-ab-analysis-framework/
```

### 2. Optional Reading

Most users do not need to read the framework files first. If you want a little more context, skim these:

1. `./references/core/index.md`
2. `./references/core/workflow.md`
3. `./references/core/rules.md`

### 3. Use

Treat this skill like a product entry point. Users should describe the job directly instead of trying to call internal sub-skills by name.

You can say:

```text
Please use tt-ab-analysis-framework to generate an experiment report.
```

```text
Please use tt-ab-analysis-framework to generate an experiment report with this temporary metric/rule guidance.
```

```text
Please use tt-ab-analysis-framework to ingest experiment knowledge.
```

### 4. Scenario Mapping

#### Primary Scenario: Experiment report generation

Use this for a full PRD + raw-data driven report.

You can say:

```text
Please use tt-ab-analysis-framework to generate an experiment report.
Experiment name (optional): [example: DM Personalized Bubble]
PRD link: [URL]
Raw Data link: [URL]
Optional screenshots or tables: [URL or pasted content]
```

What the system will do:

- run the doc-first analysis workflow,
- consult stored knowledge silently,
- perform attribution, guardrail review, and evidence-boundary checks,
- generate a structured report that answers the decision question first.

#### Secondary Scenario: Temporary metric / rule guidance

Use this for one-run-only overrides that should not be written into the reusable knowledge store.

You can say:

```text
Please use tt-ab-analysis-framework to generate an experiment report with this temporary metric/rule guidance.
Experiment name (optional): [xxx]
PRD link: [URL]
Raw Data link: [URL]
Temporary metric guidance: [example: click_report increasing means worsening risk in this experiment]
```

What the system will do:

- apply the temporary note for the current run only,
- let it override stored knowledge for this run,
- never let it override hard framework rules,
- avoid writing it into long-term knowledge unless explicitly requested.

#### Optional Scenario: Knowledge ingestion

Use this for durable glossary, polarity, and business-note updates.

You can say:

```text
Please use tt-ab-analysis-framework to ingest experiment knowledge.
Metric glossary / knowledge input: [Feishu URL or pasted text]
Optional polarity hint: [example: block/user decreasing is good]
```

For a long knowledge-base document, you can also say:

```text
Please use tt-ab-analysis-framework to organize a glossary draft from this knowledge base.
Knowledge source: [Feishu URL or pasted text]
Requirements:
1. Split the draft into metric groups / metrics / dimensions.
2. Fill what can be confirmed.
3. Leave uncertain fields blank.
4. List the questions I still need to confirm.
```

What the system will do:

- extract durable knowledge only,
- keep the stored form compact,
- update the reusable knowledge layer,
- return a short confirmation by default instead of a long write-up,
- never treat old experiment tables, conclusions, or reports as reusable knowledge,
- and, for long knowledge-base docs, default to a two-pass workflow:
  - first turn the raw source into a structured glossary draft,
  - then present a clear `to confirm` list instead of making the user find gaps manually,
  - then let the user review / correct missing or ambiguous fields,
  - then consolidate the confirmed version into the reusable glossary.

If more context is needed, read these framework files:

- `./references/core/index.md`
- `./references/core/workflow.md`
- `./references/core/rules.md`
- `./references/core/memory.md`
- `./references/core/runbook.md`
- `./references/core/tooling.md`

Use these knowledge files as the main reusable knowledge store:

- `./references/knowledge/metric_glossary.md`
- `./references/knowledge/business_kb.md`

## Main behavior

- Prefer doc-first analysis.
- Read PRD, raw-data docs, screenshots, and tables before considering live browser extraction.
- When a Lark doc is provided, prefer the built-in Lark reading path first, for example `mcp__proxy___mira_py__read_lark_content`.
- Treat live Libra extraction through direct browser reading of a Libra link/page as a beta path; it is useful but not fully stable.
- Prefer Libra `conclusion report -> switch template -> export document` as the normal path when a Libra source is involved.
- Use live Libra extraction only when a Libra link/page is explicitly provided or required, or when the available docs are insufficient.
- If the Lark tool is unavailable or cannot read the needed body content, fall back to browser reading.
- When browser reading is needed, default to the Playwright MCP browser path and use tools such as `browser_navigate`, `browser_snapshot`, and `browser_click` to read and operate the page.
- Keep missing data missing.
- Keep global evidence as the main decision evidence.
- Use drilldown and slice evidence to explain why the global result holds.
- If the PRD contains product images, UI mocks, or annotated screenshots, read them as part of the PRD whenever the model/runtime has image-reading ability.
- When reading PRD changes or arm differences, do not stop at one-line summaries; read down to concrete product deltas such as entry points, triggers, page flow, permissions, supported objects, interaction changes, and effect scope.
- When knowledge ingestion is requested, organize raw knowledge into a structured draft first if the source is long, mixed, or incomplete.
- For glossary drafts, do not make the user inspect the whole draft blindly; always surface a short `to confirm` list that says exactly what still needs review.

## Storage Boundaries

Reusable knowledge may include:

- metric name -> meaning
- metric name -> polarity
- metric group -> recall hint
- business term -> explanation
- product mechanism -> stable interpretation note

Do not store these as reusable knowledge by default:

- one-off experiment conclusions
- temporary run-only clarifications
- finished tables, conclusions, or reports from an old experiment

## Precedence

Use this order:

1. hard framework rules
2. temporary run-only instructions
3. stored knowledge
4. default inference

This means:

- temporary instructions can override stored knowledge for the current run,
- temporary instructions cannot override hard framework rules,
- stored knowledge should guide interpretation when no temporary rule is given.

## Guardrails

- Never fabricate metrics, setup fields, or conclusions.
- Never reuse an old experiment's finished outputs as evidence for a new one.
- For smoke tests and fresh case runs, always reread the currently provided source links.
- Do not use historical files, prior reports, or existing intermediate artifacts as substitutes for the current source input.
- Do not promote a single extreme slice into an independent conclusion.
- Do not let temporary guidance break hard evidence rules.
- If an experiment has multiple treatment arms, the report must not stop at separate arm summaries.
- For multi-arm experiments, the report must explicitly compare the arms and state which arm is better overall, which arm is weaker overall, and what that means for the decision.
- For multi-arm experiments, include a dedicated comparison section instead of leaving the comparison implicit across separate sections.
- Do not write fine-grained product-mechanism differences across arms unless the source explicitly shows the relevant config or description differences.
- If the PRD includes product screenshots, mocks, or visual diff tables that clarify arm differences, treat them as source evidence and read them before writing mechanism comparisons.
- If a glossary or knowledge-base source is incomplete, fill only what can be confirmed and leave the rest blank for user review.
- For glossary ingestion, the expected collaboration loop is:
  - source knowledge in,
  - structured draft out,
  - explicit `to confirm` list,
  - user confirmation,
  - formal glossary update.
