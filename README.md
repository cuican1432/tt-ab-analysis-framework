# TT AB Analysis Framework

TT A/B 实验分析框架。  
A portable framework for TT-style A/B experiment analysis.

这个仓库的目标是让团队可以用一套相对稳定的框架来做实验分析，同时持续更新业务知识和指标字典。  
This repository helps teams run experiment analysis with a stable framework while continuously updating business knowledge and metric definitions.

## Quick Start | 快速开始

### 1. Clone the Repo | 下载仓库

把仓库 clone 到一个明确的分析工作目录，比如 `ab-workspace`：  
Clone the repository into a clearly named analysis workspace such as `ab-workspace`:

```bash
mkdir -p ~/ab-workspace
cd ~/ab-workspace
git clone https://github.com/cuican1432/tt-ab-analysis-framework.git
cd tt-ab-analysis-framework
```

### 2. Install the Main Skill | 安装主 Skill

如果你是 Codex 风格本地 skill 环境，可以这样安装主 skill：  
For a Codex-style local skill setup, install the main skill like this:

```bash
mkdir -p ~/.codex/skills/tt-ab-analysis-framework
cp -R skills/tt-ab-analysis-framework/. ~/.codex/skills/tt-ab-analysis-framework/
```

主 skill 当前已经是自包含结构，复制这个目录时会一并带上它依赖的 `references/`。  
The main skill is self-contained, so copying this directory also copies the `references/` files it depends on.

如果你也想安装辅助 skill：  
If you also want the helper skills:

```bash
mkdir -p ~/.codex/skills/ab-experiment-analyst
cp -R skills/ab-experiment-analyst/. ~/.codex/skills/ab-experiment-analyst/

mkdir -p ~/.codex/skills/ab-metric-glossary
cp -R skills/ab-metric-glossary/. ~/.codex/skills/ab-metric-glossary/
```

### 3. Start Using It | 直接开始用

对大多数使用者来说，到这里就可以直接开始用了，不需要先读一堆框架文档。  
For most users, you can start here directly without reading a stack of framework files first.

如果你想先看最短说明，再看这两个文件就够了：  
If you want a very short orientation first, these two files are enough:

1. `README.md`
2. `skills/tt-ab-analysis-framework/SKILL.md`

### 4. Product Guide | 产品使用指南

这个主 skill 更适合被当成一个“实验分析产品入口”来用，而不是一个抽象工具名。  
Think of this main skill as a product-style entry point for experiment analysis rather than an abstract tool name.

它主要支持三类任务：  
It mainly supports three task types:

- 实验报告生成 | experiment report generation
- 带临时规则的实验报告生成 | experiment report generation with temporary guidance
- 知识入库 | knowledge ingestion

你不需要记内部子 skill。大多数情况下，直接调用 `tt-ab-analysis-framework` 就够了。  
You do not need to remember the internal helper skills. In most cases, calling `tt-ab-analysis-framework` directly is enough.

### 5. Usage Guide | 使用指南

#### Scenario 2: Report Generation | 场景二：一键生成实验报告

适用场景：  
Use this when:

- 实验观测期结束，数据已经就绪  
  the experiment observation window has ended and data is ready
- 需要基于 PRD + raw data 文档快速生成标准化实验报告  
  you want a standardized report from PRD + raw data documents

你可以直接这样说 👇  
You can say:

```text
Please use tt-ab-analysis-framework to generate an experiment report.
Experiment name (optional): [example: DM Personalized Bubble]
PRD link: [URL]
Raw Data link: [URL]
```

系统会这样处理：  
What the system will do:

- 串行执行 doc-first 分析流程  
  run the doc-first analysis workflow
- 静默优先读取已入库的指标字典和业务知识  
  silently prioritize stored metric glossary and business knowledge
- 在需要时做多维归因、风险梳理和证据边界标注  
  perform drill-down attribution, risk review, and evidence-boundary labeling when needed
- 输出结构化实验报告，而不是零散分析片段  
  output a structured experiment report rather than scattered analysis fragments

#### Scenario 3: Report Generation with Temporary Guidance | 场景三：带临时指标说明的实验报告

适用场景：  
Use this when:

- 本期实验有临时监控指标  
  this experiment includes a temporary monitoring metric
- 本次需要一个临时极性或解释规则  
  this run needs a temporary polarity or interpretation rule
- 你不希望把它永久写入知识库  
  you do not want to save it permanently into the knowledge base

你可以直接这样说 👇  
You can say:

```text
Please use tt-ab-analysis-framework to generate an experiment report with this temporary metric/rule guidance.
Experiment name (optional): [xxx]
PRD link: [URL]
Raw Data link: [URL]
Temporary metric guidance: [example: click_report increasing means worsening risk in this experiment]
```

系统会这样处理：  
What the system will do:

- 只在当前运行中应用这条临时说明  
  apply the temporary instruction for the current run only
- 在归因和极性判断中优先使用该临时说明  
  prioritize it during attribution and polarity judgment
- 不自动写回长期知识库  
  do not write it back into the long-term knowledge base unless explicitly asked
- 仍然遵守框架硬规则，不会因为临时说明而放宽数据纪律  
  still obey hard framework rules and never relax data discipline because of a temporary note

#### Scenario 1: Knowledge Ingestion | 场景一：纯知识入库（防瞎猜备用）

适用场景：  
Use this when:

- 刚整理好新版指标字典，想提前存入知识库  
  you have a new metric dictionary and want to store it for future runs
- 想把某些指标的极性提前定好，比如 `block/user` 下降代表更好  
  you want to fix metric polarity in advance, for example `block/user` decreasing is good
- 想把业务术语、口径说明、召回提示沉淀下来  
  you want to store business terms, metric-caliber notes, or recall hints

你可以直接这样说 👇  
You can say:

```text
Please use tt-ab-analysis-framework to ingest experiment knowledge.
Metric glossary / knowledge input: [Feishu URL or pasted text]
```

系统会这样处理：  
What the system will do:

- 在后台做轻量知识萃取  
  perform lightweight knowledge extraction in the background
- 提取可复用的 `<metric name -> meaning / polarity / note>` 信息  
  extract reusable `<metric name -> meaning / polarity / note>` mappings
- 写入本地知识层，供后续实验报告自动优先调用  
  write them into the local knowledge layer so future reports can reuse them automatically
- 默认只回一个简短确认，而不是长篇输出  
  return a short confirmation by default instead of a long write-up

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

## How A / B / C / D Fit Together | A / B / C / D 架构说明

这个框架内部虽然会分成 A / B / C / D 四个阶段，但你可以把它理解成一条很直观的流水线：  
Internally the framework uses A / B / C / D stages, but you can think of it as one simple pipeline.

- `A`
  - 负责把源信息读干净，形成“事实底稿”。  
    This stage reads the source materials and produces a clean fact base.
  - 输入可以是 PRD、raw data 文档、截图、表格，必要时也可以是 Libra 页面。  
    Inputs can be PRDs, raw-data docs, screenshots, tables, and only when needed, live Libra pages.
- `B`
  - 负责把这些事实整理成分析逻辑。  
    This stage organizes the facts into analysis logic.
  - 例如：哪些是主指标、哪些是护栏、哪些风险需要放到结论里。  
    For example: which metrics are primary, which are guardrails, and which risks need to appear in the conclusion.
- `C`
  - 负责把分析逻辑写成正式报告。  
    This stage turns the analysis logic into the final report.
  - 输出应该是可读、可复核、可以直接拿去同步或汇报的版本。  
    The output should be readable, reviewable, and ready to share.
- `D`
  - 负责做质检或评测。  
    This stage handles quality checks or evaluation.
  - 它不替代正文写作，而是检查：有没有漏指标、有没有方向写反、有没有越界结论。  
    It does not replace report writing; it checks for omissions, direction mistakes, and overclaims.

简单理解就是：  
In short:

- `A` 读事实  
  `A` reads the facts
- `B` 理逻辑  
  `B` builds the logic
- `C` 出报告  
  `C` writes the report
- `D` 做检查  
  `D` checks the output

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

- `core/index.md`
  - 总入口和导航页，帮助你快速找到该先读什么、不同文档分别负责什么。  
    The navigation entry that tells you what to read first and what each core file is for.
- `core/workflow.md`
  - 讲默认分析流程怎么跑，例如先读文档、什么时候才进入 live Libra 分支、A/B/C/D 的基本顺序。  
    Defines the default workflow order, including when to stay doc-first and when to use the live Libra branch.
- `core/rules.md`
  - 讲硬规则和证据纪律，例如不能编造数据、Global 与 slice 的关系、临时规则不能覆盖硬规则。  
    Defines hard rules and evidence discipline, including no fabrication and global-over-slice logic.
- `core/memory.md`
  - 讲需要长期记住的共识、默认分析立场和跨案例稳定约定。  
    Stores durable working memory, shared stances, and cross-case conventions.
- `core/runbook.md`
  - 讲具体执行时怎么落地，偏操作手册，比如常见步骤、边界处理和交付习惯。  
    Acts as the practical runbook for execution details, common steps, and delivery habits.
- `core/tooling.md`
  - 讲工具怎么用、什么时候用哪条路径，例如文档优先、浏览器读取、导出文档优先等。  
    Explains tooling choices and when to use each path, such as doc-first vs browser-based reading.

## What Goes Into `knowledge/` | `knowledge/` 放什么

这里放可以持续补充的知识：  
Put updateable knowledge here:

- `metric glossary`
  - 例如：`block/user` 下降代表更好、`Finish Playing/Play` 是完播比例、某些 `uv/au` 指标应按多天平均看。  
    For example: `block/user` decreasing is good, `Finish Playing/Play` means completion rate, and some `uv/au` metrics should be read as multi-day averages.
- `business terminology`
  - 例如：`MUF`、`Pair`、`FirstComment/U`、`DM Camera`、`Voice Message` 这些术语分别是什么意思。  
    For example: what terms like `MUF`, `Pair`, `FirstComment/U`, `DM Camera`, and `Voice Message` mean.
- `product / domain knowledge`
  - 例如：某个 PRD 的机制链路、功能入口位置、什么算主场景、什么属于护栏风险。  
    For example: a PRD's mechanism flow, where the feature entry lives, what counts as the main scenario, and what should be treated as a guardrail risk.
- `interpretation notes`
  - 例如：某类指标上升通常代表收益还是风险、哪些切片只能做补充解释、哪些现象只能写成待验证假设。  
    For example: whether an increase in a metric family usually means gain or risk, which slices should stay auxiliary, and which observations should remain hypotheses.

## Recommended Update Discipline | 推荐更新原则

- `knowledge/` 可以高频更新。  
  `knowledge/` can be updated frequently.
- `core/` 应谨慎更新。  
  `core/` should be updated carefully.
- 旧实验里产出的表格、结论、报告，只能用于那个实验本身；不能直接拿来证明另一个新实验。  
  Tables, conclusions, and reports produced for an old experiment should stay with that experiment and must not be reused as proof for a new one.

## Default Analysis Stance | 默认分析立场

- 优先读 PRD、raw data 文档、截图、表格。  
  Prefer PRD, raw-data docs, screenshots, and tables first.
- 通过 Libra 链接在浏览器里直接读取页面的 live Libra 抽取，目前是 `beta` 版本，能力仍不稳定；默认不作为首选输入源。  
  Live Libra extraction through direct browser reading of a Libra link/page is currently in `beta` and is not fully stable; it should not be the default input path.
- 更推荐的路径是：先在 Libra 平台进入“结论报告”，切换到合适模板后导出文档，再基于导出文档做分析。  
  The recommended path is to open Libra `conclusion report`, switch to the appropriate template, export the document, and analyze the exported document instead.
- 你可以把这条路径理解成两步：  
  You can think of this path in two steps:
  - 第一步：在 Libra 里打开“结论报告”页面，并切到合适模板。  
    Step 1: open Libra `conclusion report` and switch to the right template.
    - 示例链接：[Libra 结论报告示例](https://libra-sg.tiktok-row.net/libra/flight/70831448/conclusion-report?category=defense&target_active_tab=defense&template_id=backup-582)  
      Example link: [Sample Libra conclusion report](https://libra-sg.tiktok-row.net/libra/flight/70831448/conclusion-report?category=defense&target_active_tab=defense&template_id=backup-582)
  - 第二步：导出文档后，以导出的文档作为主要分析输入。  
    Step 2: export the document and use the exported doc as the primary analysis input.
    - 示例文档：[导出文档示例](https://bytedance.larkoffice.com/docx/L2kwdjvt5oLCwsxbB7Wc6uMRnud)  
      Example exported doc: [Sample exported document](https://bytedance.larkoffice.com/docx/L2kwdjvt5oLCwsxbB7Wc6uMRnud)
- 只有明确提供了 Libra 链接、明确要求读取 Libra 页面，或现有文档不足以支撑分析时，才做 live Libra 抽取。  
  Use live Libra extraction only when a Libra link/page is explicitly provided or required, or when the available docs are not sufficient for the analysis.
- 缺失数据就保留缺失。  
  Keep missing data missing.
- Global 结果是主要决策证据。  
  Global results are the main decision evidence.
- 多维分析用于解释为什么 Global 成立。  
  Multi-dimensional evidence is used to explain why the global result holds.
- 单个极端 slice 不能单独升格成结论。  
  A single extreme slice should not become an independent conclusion.

## Getting Started | 怎么开始

如果你是普通使用者，直接这样开始：  
If you are a normal user, start like this:

1. 安装主 skill `tt-ab-analysis-framework`。  
   Install the main skill `tt-ab-analysis-framework`.
2. 直接用主 skill 提需求，比如“生成实验报告”或“知识入库”。  
   Use the main skill directly for tasks like report generation or knowledge ingestion.
3. 只有在你确实需要更细的控制时，再去看 helper skills。  
   Only look at helper skills when you truly need finer control.

如果你是维护者或想继续扩框架，再看这些文档：  
If you are a maintainer or want to extend the framework, then read these files:

1. `core/index.md`
2. `core/workflow.md`
3. `core/rules.md`
4. `knowledge/metric_glossary.md`
5. `knowledge/business_kb.md`
