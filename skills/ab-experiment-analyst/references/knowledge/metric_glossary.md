# Metric Glossary | 指标字典

这个文件用于沉淀**可复用的指标知识**，帮助模型和使用者：

- 识别指标组是什么  
  identify what a metric group is
- 识别单个指标是什么意思  
  identify what a metric means
- 识别维度口径是什么意思  
  identify what a dimension means
- 避免把相近指标、相近维度、相近口径搞混  
  avoid confusing neighboring metrics, dimensions, or calibers

这个文件**不负责**替当前实验决定：

- 哪个组一定是 success metric
- 哪个组一定是 guardrail
- 当前实验最终结论是什么

这些属于当前实验分析，不属于 glossary 本身。  
Those belong to case-specific analysis, not to the glossary itself.

---

## Design Principle | 设计原则

建议把 glossary 分成三层，而不是把所有东西揉成一张表：

1. **Metric Group Index | 指标组索引**
2. **Metric Index | 指标索引**
3. **Dimension Index | 维度索引**

原因：

- 指标组是**召回和组织单位**  
  metric groups are recall and organization units
- 指标是**解释和归因单位**  
  metrics are interpretation and attribution units
- 维度是**下钻和切片单位**  
  dimensions are drilldown and slice units

这三个粒度不同，混写容易让模型把维度当指标，或者把组描述误套到单个指标上。  
These three layers have different granularity. Mixing them often causes confusion.

---

## Writing Rules | 填写规则

- 可以先空着，不需要一次补全所有字段。  
  It is fine to leave fields blank at first.
- 优先写**稳定、可复用**的信息。  
  Prefer stable, reusable information.
- 不要把某一次实验的结论直接写进 glossary。  
  Do not write one experiment's conclusion into the glossary.
- 不要把 `success / guardrail / supporting / long_tail` 这种当前实验角色写死在 glossary 里。  
  Do not hard-code case-specific roles such as success or guardrail into the glossary.
- 如果要表达经验角色，请用 `typical_usage` 或 `priority_hint`，不要写成绝对规则。  
  If you need to express a typical role, use `typical_usage` or `priority_hint`, not an absolute role.

---

## Key Terms | 关键字段说明

### `polarity`

表示这个指标**往哪个方向变通常更好**。  
This indicates which direction is usually better for the metric.

建议只用下面几种值：

- `higher_is_better`
- `lower_is_better`
- `depends_on_context`
- `descriptive_only`

例子：

- `Send Message PV/User`
  - `polarity: higher_is_better`
- `block/user`
  - `polarity: lower_is_better`
- `DAU`
  - `polarity: descriptive_only`

### `typical_usage`

表示这个组或指标**通常怎么被使用**，不是当前实验的最终角色。  
This tells how the group or metric is typically used, not its final role in the current case.

例子：

- `often used as a business-core metric group`
- `often used as a guardrail in social interaction experiments`
- `sometimes used as supporting evidence`

### `priority_hint`

表示这项内容在**组内或解释时的常见优先级**。  
This indicates a common interpretation or in-group priority hint.

例子：

- `P0`
- `P1`
- `P2`
- `context_dependent`

---

## 1. Metric Group Index | 指标组索引

每个条目对应一个指标组。  
Each entry corresponds to one metric group.

### Suggested Fields | 建议字段

- `group_name`
- `group_aliases`
- `description_zh`
- `description_en`
- `usage_scope`
- `is_company_core`
- `is_business_core`
- `is_sub_business_core`
- `typical_usage`
- `priority_hint`
- `common_dimensions`
- `notes`

### Template | 模板

```yaml
group_name:
group_aliases:
  - 

description_zh:
description_en:

usage_scope:
is_company_core:
is_business_core:
is_sub_business_core:

typical_usage:
priority_hint:

common_dimensions:
  - 

notes:
```

### Example | 示例

```yaml
group_name: Key Project-DM
group_aliases:
  - DM core interaction

description_zh: 私信业务中的核心互动指标组，通常覆盖发送、互动对象、互动频次等结果。
description_en: A DM interaction metric group that often covers sending, interaction breadth, and interaction frequency.

usage_scope: DM / social interaction experiments
is_company_core:
is_business_core: true
is_sub_business_core: true

typical_usage: often used as a business-core supporting group in DM experiments
priority_hint: P1

common_dimensions:
  - os
  - active_days_28d_prev_1d_layer
  - predicted_age_group_classifier_latest_prev_1d_layer

notes: Do not automatically treat this group as the main success group in every experiment.
```

---

## 2. Metric Index | 指标索引

每个条目对应一个指标。  
Each entry corresponds to one metric.

建议主键使用：

- `group_name + metric_name`

这样可以避免同名指标跨组撞车。  
This avoids collisions for the same metric name across groups.

### Suggested Fields | 建议字段

- `group_name`
- `metric_name`
- `metric_aliases`
- `meaning_zh`
- `meaning_en`
- `caliber_meaning`
- `calculation_method`
- `numerator`
- `denominator`
- `polarity`
- `priority_hint`
- `neighbor_metric_diff`
- `interpretation_notes`

### Template | 模板

```yaml
group_name:
metric_name:
metric_aliases:
  - 

meaning_zh:
meaning_en:

caliber_meaning:
calculation_method:
numerator:
denominator:

polarity:
priority_hint:

neighbor_metric_diff:
interpretation_notes:
```

### Example | 示例

```yaml
group_name: DM Core
metric_name: Send Message PV/User
metric_aliases:
  - send pv per user

meaning_zh: 每个用户平均发送消息次数。
meaning_en: Average number of message sends per user.

caliber_meaning: user-level average send intensity
calculation_method:
numerator: total send message PV
denominator: users

polarity: higher_is_better
priority_hint: P0

neighbor_metric_diff: Different from Send Message Days/User, which focuses on active days rather than total sending volume.
interpretation_notes: Often used as a direct expression-intensity signal in DM experiments.
```

---

## 3. Dimension Index | 维度索引

每个条目对应一个维度。  
Each entry corresponds to one dimension.

### Suggested Fields | 建议字段

- `dimension_name`
- `dimension_aliases`
- `meaning_zh`
- `meaning_en`
- `applies_to_groups`
- `applies_to_metrics`
- `value_examples`
- `warnings`

### Template | 模板

```yaml
dimension_name:
dimension_aliases:
  - 

meaning_zh:
meaning_en:

applies_to_groups:
  - 

applies_to_metrics:
  - 

value_examples:
  - 

warnings:
```

### Example | 示例

```yaml
dimension_name: os
dimension_aliases:
  - platform

meaning_zh: 按操作系统拆分的人群维度。
meaning_en: A dimension that splits users by operating system.

applies_to_groups:
  - DM Core

applies_to_metrics:
  - Send Message PV/User

value_examples:
  - android
  - ios

warnings: Do not treat OS differences as product-mechanism proof by itself; use it as supporting drilldown evidence.
```

---

## Partially Ingested Stable Entries | 已分批入库的稳定条目

These entries are already stable enough to be reused, even though the full DM glossary is still evolving.  
下面这些条目已经足够稳定，可以先正式入库复用；完整的 DM glossary 仍可继续在 `drafts/` 中迭代。

### Metric Groups | 指标组

```yaml
group_name: DM Core
group_aliases:
  - 私信核心指标组

description_zh: 私信核心使用行为指标组，通常用于观察进入会话、停留、发送等主链路行为。
description_en: A core DM usage metric group that usually covers entering chat, staying, and sending behaviors.

usage_scope: DM / direct message experiments
is_company_core:
is_business_core: true
is_sub_business_core: true

typical_usage: often used as a business-core metric group in DM experiments
priority_hint: P0

common_dimensions:
  - By Entrance
  - By Msg Type
  - By Motivation

notes: Confirmed in round-1 glossary review.
```

```yaml
group_name: DM Voice Message
group_aliases:
  - 私信语音指标组

description_zh: 私信语音消息相关指标组，通常用于观察语音消息录制、发送和使用行为。
description_en: A DM voice-message metric group used to observe recording, sending, and usage behavior for voice messages.

usage_scope: DM / voice-message related experiments
is_company_core:
is_business_core:
is_sub_business_core: true

typical_usage: often used as a feature-specific supporting group
priority_hint: P1

common_dimensions:

notes: Confirmed in round-1 glossary review.
```

```yaml
group_name: DM Group Chat
group_aliases:
  - 群聊指标组

description_zh: 私信群聊相关指标组，用于观察群聊进入、互动和发送行为。
description_en: A DM group-chat metric group used to observe group-chat entry, interaction, and sending behavior.

usage_scope: DM / group chat experiments
is_company_core:
is_business_core:
is_sub_business_core: true

typical_usage: often used as a sub-business supporting group
priority_hint: P1

common_dimensions:

notes: Confirmed in round-1 glossary review.
```

### Dimensions | 维度

```yaml
dimension_name: By Entrance
dimension_aliases:
  - 拆分渠道

meaning_zh: 行为维度下钻，表示消息发送或私信行为来自哪个入口渠道，例如 FYP、Inbox 等。
meaning_en: A behavioral drilldown dimension that shows which entrance channel a DM action comes from, such as FYP or Inbox.

applies_to_groups:
  - DM Core

applies_to_metrics:

value_examples:
  - FYP
  - Inbox

warnings: Entrance values should be treated as source-channel splits, not as user-quality tiers.
```

```yaml
dimension_name: By Msg Type
dimension_aliases:
  - 拆分消息类型

meaning_zh: 行为维度下钻，表示私信消息类型，如 Text、Emoji、Voice、Sticker 等。
meaning_en: A behavioral drilldown dimension that shows DM message types such as Text, Emoji, Voice, and Sticker.

applies_to_groups:
  - DM Core
  - DM Voice Message

applies_to_metrics:

value_examples:
  - Text
  - Emoji
  - Voice
  - Sticker

warnings: Message-type splits are useful for heterogeneity and mechanism explanation, but should not replace global evidence.
```

```yaml
dimension_name: By Motivation
dimension_aliases:
  - 拆分聊天动机

meaning_zh: 行为维度下钻，表示私信动机类型，例如分享、主动聊天等。
meaning_en: A behavioral drilldown dimension that shows DM motivation types such as sharing or proactive chatting.

applies_to_groups:
  - DM Core

applies_to_metrics:

value_examples:
  - 分享
  - 主动聊天

warnings: Motivation definitions are business-defined and should not be overgeneralized beyond the source taxonomy.
```

维度是“怎么切”的规则，不是指标本身。  
A dimension tells how data is sliced; it is not a metric itself.

### Suggested Fields | 建议字段

- `dimension_name`
- `dimension_aliases`
- `meaning_zh`
- `meaning_en`
- `applies_to_groups`
- `applies_to_metrics`
- `value_examples`
- `warnings`

### Template | 模板

```yaml
dimension_name:
dimension_aliases:
  - 

meaning_zh:
meaning_en:

applies_to_groups:
  - 

applies_to_metrics:
  - 

value_examples:
  - 

warnings:
```

### Example | 示例

```yaml
dimension_name: active_days_28d_prev_1d_layer
dimension_aliases:
  - active_days layer

meaning_zh: 按近 28 天活跃天数分层的人群维度。
meaning_en: A user segmentation dimension based on active days in the previous 28 days.

applies_to_groups:
  - DM Core
  - Key Project-DM

applies_to_metrics:
  - Send Message PV/User
  - Enter Chat PV/User

value_examples:
  - new_user
  - 0-7_days
  - 8-14_days
  - 15-21_days
  - 21+_days

warnings: Do not treat these values as ordered business quality tiers without source support.
```

---

## 4. Optional: Dimension Value Index | 可选：维度值索引

如果某个维度的枚举值非常多，且每个值都有明确业务含义，可以再单独补一层。  
If a dimension has many values and each one has clear business meaning, add a separate value index.

### Suggested Fields | 建议字段

- `dimension_name`
- `value_name`
- `value_aliases`
- `meaning_zh`
- `meaning_en`
- `ordering`
- `notes`

### Template | 模板

```yaml
dimension_name:
value_name:
value_aliases:
  - 

meaning_zh:
meaning_en:

ordering:
notes:
```

---

## Recommended Update Order | 推荐更新顺序

如果你们要统一补 glossary，建议按这个顺序来：  
If your team wants to update the glossary in a consistent way, use this order:

1. 先补 `Metric Group Index`
2. 再补 `Metric Index`
3. 最后补 `Dimension Index`

因为模型通常会先问：

- 这是什么组？
- 这个指标是什么意思？
- 这个维度又是什么意思？

That order matches how the model usually reasons.

---

## Minimum Viable Update | 最小可行更新

如果时间有限，先补下面这些字段就够了：  
If time is limited, start with these fields first:

### 对指标组

- `group_name`
- `description_zh`
- `is_business_core`
- `typical_usage`

### 对指标

- `group_name`
- `metric_name`
- `meaning_zh`
- `polarity`

### 对维度

- `dimension_name`
- `meaning_zh`
- `value_examples`

先把骨架搭好，比一次写得过满更重要。  
Getting the structure right matters more than filling everything at once.
