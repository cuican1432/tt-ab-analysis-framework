---
name: tt-ab-analysis-framework
description: Main entry skill for TT A/B experiment work. Use when you want to ingest experiment knowledge, generate an experiment report, or apply temporary metric/rule guidance for a single run.
---

# TT AB Analysis Framework

Use this as the main user-facing skill for TT-style A/B experiment work.

This skill supports three common modes:

1. experiment report generation
2. report generation with temporary metric or rule guidance
3. knowledge ingestion

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

Treat this skill like a product entry point. Users should describe their scenario directly instead of trying to call internal sub-skills by name.

Use one of these patterns:

- `Please use tt-ab-analysis-framework to ingest experiment knowledge.`
- `Please use tt-ab-analysis-framework to generate an experiment report.`
- `Please use tt-ab-analysis-framework to generate an experiment report with this temporary metric/rule guidance.`

### 4. Scenario Mapping

#### Primary Scenario: Experiment report generation

Use this for a full PRD + raw-data driven report.

Typical user input:

- `Please use tt-ab-analysis-framework to generate an experiment report.`
- `Experiment name (optional): [example: DM Personalized Bubble]`
- `PRD link: [URL]`
- `Raw Data link: [URL]`
- `Optional screenshots or tables: [URL or pasted content]`

System behavior:

- run the doc-first analysis workflow,
- consult stored knowledge silently,
- perform drill-down attribution and risk review when needed,
- generate a structured experiment report with gains, risks, and evidence boundaries visible.

#### Secondary Scenario: Temporary metric / rule guidance

Use this for one-run-only overrides that should not be written into the reusable knowledge store.

Typical user input:

- `Please use tt-ab-analysis-framework to generate an experiment report with this temporary metric/rule guidance.`
- `Experiment name (optional): [xxx]`
- `PRD link: [URL]`
- `Raw Data link: [URL]`
- `Temporary metric guidance: [example: click_report increasing means worsening risk in this experiment]`

System behavior:

- apply the temporary note for the current run only,
- let it override stored knowledge for this run,
- never let it override hard framework rules,
- avoid writing it into the long-term knowledge base unless explicitly requested.

#### Optional Scenario: Knowledge ingestion

Use this for durable glossary, polarity, and business-note updates.

Typical user input:

- `Please use tt-ab-analysis-framework to ingest experiment knowledge.`
- `Metric glossary / knowledge input: [Feishu URL or pasted text]`
- `Optional polarity hint: [example: block/user decreasing is good]`

System behavior:

- extract durable knowledge only,
- keep the stored form compact,
- update the reusable knowledge layer,
- return a short confirmation by default instead of a long write-up.
- do not treat old experiment tables, conclusions, or reports as reusable knowledge.

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
