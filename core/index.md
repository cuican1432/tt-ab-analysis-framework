# Core Index

Use this file as the navigation page for the framework.

如果你只是想快速理解这套框架，不需要一次把所有文件都读完。  
If you only want a quick understanding of the framework, you do not need to read every file end to end.

最简单的理解方式是：  
The simplest mental model is:

- `workflow.md` 讲“怎么跑”  
  `workflow.md` explains the workflow
- `rules.md` 讲“哪些不能破”  
  `rules.md` explains the rules you should not break
- `memory.md` 讲“哪些共识要长期记住”  
  `memory.md` explains the conventions worth keeping
- `runbook.md` 讲“落地时怎么做”  
  `runbook.md` explains how execution is typically done
- `tooling.md` 讲“工具和输入源怎么选”  
  `tooling.md` explains tooling and source-path choices

## Read Order

1. `workflow.md`
2. `rules.md`
3. `memory.md`
4. `runbook.md`
5. `tooling.md`

## File Roles

- `workflow.md`
  - the default A / B / C / D order
  - doc-first vs live Libra branch
- `rules.md`
  - hard rules and evidence discipline
  - what not to overclaim
- `memory.md`
  - stable operating memory and artifact conventions
  - long-lived shared conventions
- `runbook.md`
  - practical execution guidance
  - how work usually gets carried out
- `tooling.md`
  - tool preferences and browser guidance
  - when to use docs, exports, or browser reading

## Editing Boundary

Use this simple split:

- usually protected
  - `workflow.md`
  - `rules.md`
  - the main skill's guardrails
- safe to extend
  - `knowledge/metric_glossary.md`
  - `knowledge/business_kb.md`
- change with a short rationale
  - `runbook.md`
  - `tooling.md`
  - `README.md`

Practical reminder:

- update knowledge often,
- change rules carefully,
- and do not change source-truth or evidence-discipline rules casually.
