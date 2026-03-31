# TT AB Analysis Framework

TT A/B 实验分析框架。  
A portable framework for TT-style A/B experiment analysis.

这个仓库的目标是让团队可以用一套相对稳定的框架来做实验分析，同时持续更新业务知识和指标字典。  
This repository helps teams run experiment analysis with a stable framework while continuously updating business knowledge and metric definitions.

## Repository Structure | 仓库结构

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

## Design Principle | 设计原则

- `core/` 放稳定框架：流程、规则、运行约定。  
  `core/` contains the stable framework: workflow, rules, and operating conventions.
- `knowledge/` 放可持续补充的知识：指标字典、业务知识。  
  `knowledge/` contains updateable knowledge such as the metric glossary and business notes.
- `skills/` 放工具入口。  
  `skills/` contains tool-facing skill entry points.
- `tt-ab-analysis-framework` 是主入口 skill。  
  `tt-ab-analysis-framework` is the main user-facing skill.

## What Goes Into `core/` | `core/` 放什么

这里放不应该频繁变化的内容：  
Put stable content here:

- workflow order
- evidence discipline
- report-writing principles
- artifact conventions
- tooling guidance
- memory / navigation

## What Goes Into `knowledge/` | `knowledge/` 放什么

这里放可以持续补充的知识：  
Put updateable knowledge here:

- metric glossary
- business terminology
- product / domain knowledge
- interpretation notes

## Recommended Update Discipline | 推荐更新原则

- `knowledge/` 可以高频更新。  
  `knowledge/` can be updated frequently.
- `core/` 应谨慎更新。  
  `core/` should be updated carefully.
- 一个实验的 A / B / C / D 产物不能作为另一个实验的证据。  
  Completed A / B / C / D outputs from one experiment must not be reused as evidence for another experiment.

## Default Analysis Stance | 默认分析立场

- 优先读 PRD、raw data 文档、截图、表格。  
  Prefer PRD, raw-data docs, screenshots, and tables first.
- 只有明确需要时才做 live Libra 抽取。  
  Use live Libra extraction only when it is explicitly required.
- 缺失数据就保留缺失。  
  Keep missing data missing.
- Global 结果是主要决策证据。  
  Global results are the main decision evidence.
- 多维分析用于解释为什么 Global 成立。  
  Multi-dimensional evidence is used to explain why the global result holds.
- 单个极端 slice 不能单独升格成结论。  
  A single extreme slice should not become an independent conclusion.

## Suggested Adoption | 推荐使用顺序

1. Read `core/index.md`.
2. Read `core/workflow.md`.
3. Read `core/rules.md`.
4. Extend `knowledge/metric_glossary.md` and `knowledge/business_kb.md` as needed.
5. Use `skills/tt-ab-analysis-framework/SKILL.md` as the main user-facing entry point.
6. Use narrower helper skills only when needed.

## Quick Start | 快速开始

### 1. Install | 安装

把仓库 clone 到一个明确的分析工作目录，比如 `ab-workspace`：  
Clone the repository into a clearly named analysis workspace such as `ab-workspace`:

```bash
mkdir -p ~/ab-workspace
cd ~/ab-workspace
git clone https://github.com/cuican1432/tt-ab-analysis-framework.git
cd tt-ab-analysis-framework
```

如果你是 Codex 风格本地 skill 环境，可以这样安装主 skill：  
For a Codex-style local skill setup, install the main skill like this:

```bash
mkdir -p ~/.codex/skills/tt-ab-analysis-framework
cp -R skills/tt-ab-analysis-framework/* ~/.codex/skills/tt-ab-analysis-framework/
```

如果你也想安装辅助 skill：  
If you also want the helper skills:

```bash
mkdir -p ~/.codex/skills/ab-experiment-analyst
cp -R skills/ab-experiment-analyst/* ~/.codex/skills/ab-experiment-analyst/

mkdir -p ~/.codex/skills/ab-metric-glossary
cp -R skills/ab-metric-glossary/* ~/.codex/skills/ab-metric-glossary/
```

建议先读这三个文件：  
Start by reading these three files:

1. `README.md`
2. `core/index.md`
3. `skills/tt-ab-analysis-framework/SKILL.md`

### 2. Use | 调用

主 skill 支持三类典型任务：  
The main skill supports three common tasks:

- knowledge ingestion
- report generation
- report generation with temporary rule guidance

示例 prompts：  
Example prompts:

- `Please use tt-ab-analysis-framework to ingest experiment knowledge.`
- `Please use tt-ab-analysis-framework to generate an experiment report.`
- `Please use tt-ab-analysis-framework to generate an experiment report with this temporary metric/rule guidance.`

### 3. Typical Scenarios | 典型场景

- Knowledge ingestion  
  用于沉淀可复用的指标含义、极性规则、业务知识。  
  Store reusable metric meanings, polarity rules, and business notes.

- Report generation  
  用于基于 PRD + raw data 文档 + 辅助材料生成完整实验报告。  
  Generate a full experiment report from PRD + raw data docs + supporting materials.

- Report generation with temporary guidance  
  用于本次实验临时加一条解释或规则，但不写回知识库。  
  Apply a one-run-only metric explanation or rule without updating stored knowledge.
