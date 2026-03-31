---
name: tt-ab-analysis-framework
description: Main entry skill for TT A/B experiment work. Use when you want to ingest experiment knowledge, generate an experiment report, or apply temporary metric/rule guidance for a single run.
---

# TT AB Analysis Framework

Use this as the main user-facing skill for TT-style A/B experiment work.

This skill supports three common modes:

1. knowledge ingestion
2. experiment report generation
3. report generation with temporary metric or rule guidance

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

### 2. Read

Read these files first:

1. `./references/core/index.md`
2. `./references/core/workflow.md`
3. `./references/core/rules.md`
4. `./references/core/memory.md`

### 3. Use

Then use one of these prompts:

- `Please use tt-ab-analysis-framework to ingest experiment knowledge.`
- `Please use tt-ab-analysis-framework to generate an experiment report.`
- `Please use tt-ab-analysis-framework to generate an experiment report with this temporary metric/rule guidance.`

### 4. Scenario Mapping

- Knowledge ingestion
  - for durable glossary, polarity, and business-note updates
- Experiment report generation
  - for full PRD + raw-data driven reporting
- Temporary metric / rule guidance
  - for one-run-only overrides that should not be written into the reusable knowledge store

Read these framework files first:

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
- Use live Libra extraction only when the task explicitly requires it or the docs are insufficient.
- Keep missing data missing.
- Keep global evidence as the main decision evidence.
- Use drilldown and slice evidence to explain why the global result holds.

## Mode 1: Knowledge Ingestion

Use this mode when the user wants to store reusable metric or business knowledge for future runs.

Examples:

- a new metric dictionary
- a new polarity rule
- a business-term explanation
- a domain note about how to read a metric family

Expected behavior:

- extract the durable knowledge only,
- write it into the appropriate knowledge file,
- keep the stored form compact and reusable,
- do not produce a long report unless the user asks for one.

What belongs in knowledge ingestion:

- metric name -> meaning
- metric name -> polarity
- metric group -> recall hint
- business term -> explanation
- product mechanism -> stable interpretation note

What does not belong in knowledge ingestion:

- one-off experiment conclusions
- temporary run-only clarifications
- finished A / B / C / D outputs

## Mode 2: Experiment Report Generation

Use this mode when the user wants a full experiment report.

Expected behavior:

1. read source materials,
2. consult stored knowledge,
3. identify targets, guardrails, and mechanism clues,
4. build the recall set,
5. extract or read Stage A facts from the relevant source,
6. write B,
7. write C,
8. run D when required.

## Mode 3: Temporary Metric / Rule Guidance

Use this mode when the user wants a one-run-only clarification.

Examples:

- a temporary polarity note
- a temporary interpretation note
- a one-off rule for this experiment only

Expected behavior:

- apply the temporary note to the current run only,
- do not write it into the reusable knowledge store unless the user explicitly asks to store it,
- make the precedence explicit when needed.

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

## Suggested user prompts

### Knowledge ingestion

`Please use tt-ab-analysis-framework to ingest experiment knowledge.`

### Report generation

`Please use tt-ab-analysis-framework to generate an experiment report.`

### Report generation with temporary guidance

`Please use tt-ab-analysis-framework to generate an experiment report with this temporary metric/rule guidance.`

## Guardrails

- Never fabricate metrics, setup fields, or conclusions.
- Never reuse an old experiment's finished outputs as evidence for a new one.
- Do not promote a single extreme slice into an independent conclusion.
- Do not let temporary guidance break hard evidence rules.
