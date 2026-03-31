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

这两个 helper skill 现在也都是自包含结构，复制目录时会一并带上它们依赖的 `references/`。  
These two helper skills are also self-contained now, so copying the directory also carries their required `references/`.

### 2.5 Smoke Test Case | 烟测案例

如果你想快速验证这套框架是不是能真正跑起来，可以先用这个公开写在仓库里的测试案例：  
If you want to quickly verify that the framework really works, start with this repo-documented smoke test case:

- `Personalized Bubble / 个性化气泡`
  - Raw Data: [Lark Raw Data Doc](https://bytedance.larkoffice.com/docx/L2kwdjvt5oLCwsxbB7Wc6uMRnud)
  - PRD: [Lark PRD](https://bytedance.larkoffice.com/wiki/BT70wFcLAi5eh3k2ihJc4LCynWe)

- `DM Card UI Optimization / 私信卡片 UI 优化`
  - Raw Data: [Lark Raw Data Doc](https://bytedance.larkoffice.com/docx/GTtkd0Ixnos3VExjttecsuKEnxp)
  - PRD: [Lark PRD](https://bytedance.sg.larkoffice.com/docx/GNMUdHluloFyw3xeaSklIAaSgee)

最简单的验证方式是：  
The simplest validation flow is:

1. 安装主 skill  
   Install the main skill
2. 把上面的 `PRD` 和 `Raw Data` 链接直接喂给 `tt-ab-analysis-framework`  
   Pass the `PRD` and `Raw Data` links above directly into `tt-ab-analysis-framework`
3. 看它能否走通 doc-first 分析路径，并产出结构化实验报告  
   Check whether it can follow the doc-first analysis path and produce a structured report

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

`core/` 里的几个文档可以这样理解：  
You can read the files under `core/` like this:

- `workflow.md`
  - 讲默认流程怎么跑，尤其是 doc-first 路径和什么时候才进入 live Libra 分支。  
    Describes the default workflow, especially the doc-first path and when to enter the live Libra branch.
- `rules.md`
  - 讲不能破的硬规则和证据纪律，比如不能编造、Global 优先、slice 不能乱升格。  
    Covers the hard rules and evidence discipline, such as no fabrication, global-over-slice logic, and no overpromotion of slices.
- `memory.md`
  - 讲这套框架希望长期记住的默认共识和稳定约定。  
    Stores durable conventions and shared defaults that the framework should keep remembering.
- `runbook.md`
  - 讲实际执行时的操作习惯和落地方式，更像执行手册。  
    Explains execution habits and practical operating steps, more like a runbook.
- `tooling.md`
  - 讲不同工具和输入源怎么选，比如文档、导出文档、浏览器读取分别适合什么场景。  
    Explains tooling and source choices, such as when to use docs, exported docs, or browser reading.
- `index.md`
  - 讲总导航，帮你决定先看哪份文件。  
    Acts as the navigation page that helps you decide what to open first.

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

## Metric Tiers | 指标分层与职责

这套框架默认把指标分成三层来看。这样做的目的，不是把指标机械分类，而是帮助我们在写结论时分清“谁负责主结论、谁负责护栏、谁负责异常补充”。  
This framework uses three metric tiers by default. The goal is not to label metrics mechanically, but to clarify which metrics support the main conclusion, which ones act as guardrails, and which ones serve as anomaly-monitoring support.

- `Tier A`（主归因层）
  - 这层通常对应 PRD 目标、业务域核心指标、success metrics。  
    This tier usually maps to PRD targets, domain-core metrics, and success metrics.
  - 它主要用于主结论和深度归因。  
    It is mainly used for the main conclusion and deeper attribution.
  - 如果报告最后只允许留下最关键的 1 到 3 个结果，通常优先从这一层里选。  
    If the report only highlights the most important 1 to 3 results, they usually come from this tier first.

- `Tier B`（护栏 / 传导层）
  - 这层通常放公司核心、APP 必看、DAU、留存、性能，以及重要副作用指标。  
    This tier usually includes company-core metrics, app-level must-watch metrics, DAU, retention, performance, and major side-effect indicators.
  - 它主要用于判断实验有没有劣化风险、稳定性问题，或者收益是否伴随明显代价。  
    It is mainly used to judge whether the experiment introduces degradation, stability problems, or meaningful tradeoffs.
  - 这层不一定主导“收益成立”，但会强烈影响“能不能推、要不要保守”。  
    This tier may not decide whether the gain exists, but it strongly affects whether rollout should be conservative.

- `Tier C`（全量监控层）
  - 这层通常放没有被 Tier A / Tier B 覆盖，但出现显著异动的长尾指标和关键切片异常。  
    This tier usually covers long-tail metrics and important slice anomalies that are not already covered by Tier A or Tier B.
  - 它主要用于监控、风险补充和异常留痕。  
    It is mainly used for monitoring, risk supplementation, and anomaly logging.
  - 它可以帮助解释现象、提醒后续关注点，但不应该抢主结论。  
    It can help explain observations and flag follow-up areas, but it should not take over the main conclusion.

一个简单记法是：  
A simple memory aid is:

- `Tier A` 决定“核心结果是什么”  
  `Tier A` defines the core result
- `Tier B` 决定“这个结果稳不稳、值不值得推”  
  `Tier B` determines whether that result is safe and rollout-worthy
- `Tier C` 决定“还有哪些异常值得记下来，但不该喧宾夺主”  
  `Tier C` captures anomalies worth recording without letting them dominate the story

## Recall and Priority | 强制召回与优先级表达法

除了给指标分层，这套框架还会区分两件事：  
Beyond metric tiering, the framework keeps two separate questions apart:

- 哪些指标必须被召回进分析全集  
  which metrics must be recalled into the analysis universe
- 哪些指标最后值得进入主结论  
  which metrics deserve to enter the main conclusion

这两件事不是一回事。  
These are not the same thing.

### 召回全集（不能漏）| Recall Universe

默认必须召回这些内容：  
By default, recall all of the following:

- `Tier A`
  - PRD 目标、业务域核心、success metrics  
    PRD targets, business-core metrics, and success metrics
- `Tier B`（核心 / 必看）
  - 公司核心、APP 必看、DAU、留存、性能、重要副作用  
    company-core, app-level must-watch metrics, DAU, retention, performance, and major side effects
- `PRD` 明确点名的目标或护栏  
  - anything explicitly named in the PRD as a target or guardrail
- 整体显著结果
  - 默认指 global 层 `p < 0.05` 的结果  
    by default, global results with `p < 0.05`
- 关键维度显著结果
  - 默认指关键维度上 `p < 0.03` 的结果  
    by default, key-dimension results with `p < 0.03`

### 表达优先级 | Expression Priority

被召回，不等于被拔高。  
Being recalled does not automatically mean being elevated.

- 主结论通常只保留 `1-3` 个最关键结果。  
  The main conclusion usually keeps only `1-3` of the most important results.
- 主结论的排序应围绕 PRD 主目标来组织。  
  Main-conclusion ordering should be organized around the primary PRD objective.
- 进入全集但不属于主结论的指标，应降级进入这些位置：  
  Metrics that are recalled but do not belong in the main conclusion should be downgraded into:
  - 监控与风险  
    monitoring and risk
  - 异常长尾  
    long-tail anomalies
  - 核心护栏稳定项列表  
    stable core-guardrail lists
  - 数据附录  
    appendices

一个实用记法是：  
A practical memory aid is:

- “召回”解决的是不要漏看  
  recall solves coverage
- “优先级”解决的是不要乱拔高  
  priority solves overpromotion

## Attribution Discipline | 归因平权与防因果过推

这套框架不要求所有归因都来自同一种证据。更稳的做法是：哪条证据链能闭环，就优先用哪条。  
The framework does not require every attribution to come from the same kind of evidence. A safer rule is: use whichever evidence chain can actually close the loop.

默认平权看三类归因证据：  
By default, treat these three attribution routes as equally valid:

- 物理 / 布局证据  
  physical / layout evidence
- 机制 / 传导链路证据  
  mechanism / transmission-chain evidence
- 数据下钻 / 切片证据  
  drilldown / slice evidence

它们之间不是谁天然更高级，而是谁更能把“现象 -> 解释”说清楚。  
None of them is inherently superior; the useful one is the one that best connects the observation to the explanation.

真正做归因排查时，通常会沿着这些方向去看：  
In practice, attribution investigations usually move along these directions:

- 链路归因  
  - 看漏斗哪一步断了、哪一步爆了，以及上游变化有没有真的带动下游结果。  
    Check which funnel step broke or spiked, and whether upstream movement actually carried into downstream results.
- 用户归因  
  - 看新老用户、高低频用户、平台、机型、人群结构有没有变化，也要留心辛普森悖论。  
    Check whether composition changed across new vs existing users, heavy vs light users, platform, device, and segment mix, including Simpson's paradox risk.
- 指标结构归因  
  - 看公式拆解后，究竟是渗透、频次、客单价，还是存量 / 增量在驱动结果。  
    Decompose the metric formula to see whether penetration, frequency, basket size, or stock vs incremental effects are driving the movement.
- 空间归因  
  - 看有没有内部蚕食、模块竞争、资源挤压，避免“一个地方涨、别的地方掉”。  
    Check for cannibalization, module competition, or resource crowding so that one gain is not hiding losses elsewhere.
- 时间归因  
  - 看是短期新奇效应，还是更稳定的持续收益；也要考虑长周期业务的延迟回填。  
    Distinguish short-lived novelty effects from stable gains, and account for delayed backfill in long-conversion businesses.
- 数据质量归因  
  - 如果数据源提供了进组样本、分流或基线信息，就先看这些有效性信号；如果没有，就明确这部分暂时无法判断。  
    If the source provides assignment counts, traffic-split details, or baseline checks, review them first; if not, state clearly that this validity check cannot be completed.
  - 常见检查包括：`SRM`、离群值、AA 基线、埋点或分流问题。  
    Common checks include `SRM`, outliers, AA baselines, instrumentation, and assignment quality.
- 外部 / 产品归因  
  - 看版本更新、Bug、运营活动、按钮打架、误触等外部或交互因素。  
    Check app versions, bugs, ops events, button conflicts, accidental taps, and other external or interaction-driven factors.

做归因时，建议明确标注：  
When making an attribution, label it clearly when useful:

- `[直接证据]`
  - 例如：PRD 明确写了入口变化，数据也刚好在对应链路上提升  
    for example, the PRD explicitly changes an entry point and the linked metrics move accordingly
- `[间接证据]`
  - 例如：主链路提升明显，但中间机制只能通过相邻行为去推断  
    for example, the main path improves clearly, but the mechanism is inferred through adjacent behaviors
- `[待验证假设]`
  - 例如：存在一个合理解释，但当前还缺少足够数据把它坐实  
    for example, the explanation is plausible, but current evidence is not enough to confirm it

同时要守住两个边界：  
At the same time, keep two boundaries:

- 严禁无客观数据支撑的心理学臆测。  
  Do not invent psychology without objective support.
- 严禁无证据支撑的主观动机揣测。  
  Do not speculate about user motivation without evidence.

还有一个很实用的原则：  
There is also one very practical rule:

- 不是每次都要把所有方向都排完，而是优先排那些最可能真正解释当前异动的方向。  
  You do not need to exhaust every direction every time; prioritize the ones most likely to explain the current movement.

一句话记法：  
A simple memory aid is:

- 归因可以大胆找，但结论必须老实写。  
  Attribution can be exploratory, but conclusions must stay honest.

## Metric-Caliber Discipline | 严守口径底线

在解释任何异动之前，先把口径对齐。  
Before explaining any anomaly, align the metric caliber first.

默认至少检查这几件事：  
At minimum, check these:

- 定义  
  definition
- 分母  
  denominator
- 去重规则  
  dedup rule
- 窗口  
  window
- 时间粒度  
  time granularity

如果这些还没对齐，就不要急着下强结论。  
If these are not aligned yet, do not rush into a strong conclusion.

这套框架默认还有一个专门提醒：  
The framework also keeps one explicit reminder here:

- `DAU` 主要代表样本量和规模背景。  
  `DAU` mainly reflects sample size and scale context.
- 它可以帮助判断覆盖范围和体量变化。  
  It can help describe coverage and scale.
- 但它本身不应该被当成效果提升或效果劣化的直接结论。  
  But it should not by itself be used as the direct conclusion for treatment effect.

一个简单记法是：  
A simple memory aid is:

- 先对齐口径，再解释现象。  
  align caliber first, explain the movement second

## Global vs Segment Reading | 大盘与切片怎么看

大盘和切片，不建议用同一套宽松标准来读。  
Global results and slice results should not be read with the same loose standard.

- `Global`
  - 更看统计稳健性。  
    Focus more on statistical stability.
  - 默认先看 `p < 0.05`、置信区间是否跨 `0`；如果数据源提供了进组样本与分流信息，再补做 `SRM` 检查。  
    By default, check `p < 0.05` and whether the confidence interval crosses `0`; if assignment counts and split details are available, then also check `SRM`.
  - 即使显著，也要继续看业务幅度是否足够有意义。  
    Even if significant, still check whether the business magnitude is meaningful.

- `Segment`
  - 更看一致性，而不是只看单个显著。  
    Focus more on consistency than on a single significant point.
  - 默认把关键切片收紧到 `p < 0.03`。  
    By default, use a tighter `p < 0.03` threshold for key slices.
  - 但即使过了 `p < 0.03`，也还要看：
    - 方向是否和大盘一致  
      whether the direction is aligned with the global result
    - 相邻链路指标是否也同向  
      whether adjacent metrics in the chain move in the same direction
    - 有没有合理业务逻辑支撑  
      whether there is a credible business explanation
  - 如果只是很窄的小切片单点显著，而大盘和相邻切片都不支持，优先降级成监控项或待验证假设。  
    If only a very narrow slice is significant while the global result and nearby slices do not support it, downgrade it into monitoring or a hypothesis to verify.
  - 做异质性排查时，可以检查是否存在“局部表现更好，但整体没有完全体现”的现象；如果缺少结构信息，这类判断应保守写成异质性提示或待验证假设。  
    When checking heterogeneity, it is reasonable to ask whether some local strength is not fully reflected at the overall level; if structure information is incomplete, keep this as a cautious heterogeneity note or a hypothesis to verify.

一个简单记法是：  
A simple memory aid is:

- 大盘看稳健性  
  Global focuses on stability
- 切片看一致性  
  Segments focus on consistency

## Truthfulness First | 数据真实性第一

这套框架默认把“数据真实性”放在最前面。  
This framework puts data truthfulness first.

如果出现冲突，默认优先级是：  
When tradeoffs appear, the default priority is:

1. 防造假 / 防抄错  
   prevent fabrication and copying mistakes
2. 与 PRD 对齐  
   stay aligned with the PRD
3. 再考虑推演是否漂亮、表述是否高级  
   only then optimize the elegance or sophistication of the interpretation

也就是说：  
In practice, this means:

- 宁可少说，也不要写错。  
  it is better to say less than to say something wrong
- 宁可保守，也不要为了“像个完整报告”去补猜。  
  it is better to stay conservative than to guess just to make the report feel complete

## Conservative by Default | 缺省保守推断

当证据不足时，默认做保守表达。  
When evidence is insufficient, default to conservative language.

这时候应该明确区分三件事：  
At that point, clearly separate these three things:

- 能确认什么  
  what can be confirmed
- 还不能确认什么  
  what cannot yet be confirmed
- 哪些只是方向性判断  
  what is only directional for now

这套框架更偏向这样一种写法：  
This framework prefers writing that is:

- 保守  
  conservative
- 清晰  
  clear
- 可复核  
  reviewable

而不是：

- 华丽  
  flashy
- 看起来很完整  
  superficially complete
- 但其实站不住  
  yet not defensible

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
