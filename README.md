# TT AB Analysis Framework

This repository is a portable framework for TikTok / TT-style A/B experiment analysis.

It is designed to help teams:

- run experiment analysis with a shared structure,
- update business knowledge over time,
- keep rules stable while allowing glossary and knowledge expansion,
- reuse the framework across local tools such as Codex or Trae.

## Repository Structure

```text
tt-ab-analysis-framework/
  README.md
  core/
    workflow.md
    rules.md
    memory.md
    runbook.md
    tooling.md
    index.md
  knowledge/
    metric_glossary.md
    business_kb.md
  skills/
    tt-ab-analysis-framework/
      SKILL.md
    ab-experiment-analyst/
      SKILL.md
    ab-metric-glossary/
      SKILL.md
```

## Design Principle

Keep the repository simple:

- `core/` holds the stable framework.
- `knowledge/` holds the updateable business knowledge.
- `skills/` holds tool-facing skill wrappers that point back to `core/` and `knowledge/`.
- `tt-ab-analysis-framework` is the main user-facing skill.
- The other skills can stay as narrower internal or advanced helpers.

## What Goes Into `core/`

Put stable, shared rules here:

- workflow order,
- evidence discipline,
- report-writing principles,
- artifact conventions,
- tooling guidance,
- summary memory and navigation.

These files should change slowly and intentionally.

## What Goes Into `knowledge/`

Put updateable content here:

- metric glossary,
- business terminology,
- product/domain knowledge,
- interpretation notes that help analysis.

These files can be updated much more frequently than `core/`.

## Recommended Update Discipline

- Update `knowledge/` freely when the team learns new metric meanings or business context.
- Update `core/` carefully when changing workflow, evidence rules, or reporting standards.
- Do not treat completed A / B / C / D outputs from one experiment as reusable evidence for another experiment.

## Default Analysis Stance

- Prefer PRD, raw-data docs, screenshots, and tables first.
- Use live Libra extraction only when the task explicitly requires it.
- Keep missing data missing.
- Keep global results as the main decision evidence.
- Use multi-dimensional evidence to explain why global holds.
- Do not promote a single extreme slice into an independent conclusion.

## Suggested Adoption

1. Read `core/index.md`.
2. Read `core/workflow.md`.
3. Read `core/rules.md`.
4. Extend `knowledge/metric_glossary.md` and `knowledge/business_kb.md` as needed.
5. Use `skills/tt-ab-analysis-framework/SKILL.md` as the main user-facing entry point.
6. Use the narrower skills only when a tool or team needs a more specialized wrapper.

## Quick Start

### 1. Install

Clone the repository to a local workspace:

```bash
mkdir -p ~/workspace
cd ~/workspace
git clone <YOUR_GITHUB_URL>/tt-ab-analysis-framework.git
cd tt-ab-analysis-framework
```

For a Codex-style local skill setup, install the main skill by copying it into the local skill directory:

```bash
mkdir -p ~/.codex/skills/tt-ab-analysis-framework
cp -R skills/tt-ab-analysis-framework/* ~/.codex/skills/tt-ab-analysis-framework/
```

If you also want the narrower helper skills available:

```bash
mkdir -p ~/.codex/skills/ab-experiment-analyst
cp -R skills/ab-experiment-analyst/* ~/.codex/skills/ab-experiment-analyst/

mkdir -p ~/.codex/skills/ab-metric-glossary
cp -R skills/ab-metric-glossary/* ~/.codex/skills/ab-metric-glossary/
```

First read:

1. `README.md`
2. `core/index.md`
3. `skills/tt-ab-analysis-framework/SKILL.md`

### 2. Use

Use the main skill with one of these intents:

- knowledge ingestion
- report generation
- report generation with temporary rule guidance

Example prompts:

- `Please use tt-ab-analysis-framework to ingest experiment knowledge.`
- `Please use tt-ab-analysis-framework to generate an experiment report.`
- `Please use tt-ab-analysis-framework to generate an experiment report with this temporary metric/rule guidance.`

### 3. Typical Scenarios

- Knowledge ingestion
  - store reusable metric meanings, polarity rules, and business notes
- Report generation
  - generate a full experiment report from PRD + raw data docs + supporting materials
- Report generation with temporary guidance
  - apply a one-run-only metric explanation or polarity rule without changing stored knowledge
