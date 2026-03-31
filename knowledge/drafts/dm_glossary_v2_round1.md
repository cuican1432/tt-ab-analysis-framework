# DM Glossary v2 (Round 1 Confirmed) | 私信 Glossary v2（第一轮确认版）

Source | 来源：

- [【AI+AB】私信知识库](https://bytedance.larkoffice.com/wiki/XVoNwDn7piwyKukCRWNcXMD1nId)
- Round-1 review decisions from the glossary draft

Purpose | 用途：

- 这是在 `dm_glossary_seed_from_ai_ab_kb.md` 基础上，吸收第一轮确认结果后的整理版。  
- 它比 seed draft 更稳定，但仍然属于 **draft**，还没有直接并入正式 glossary。  
- 这份文件的目标是把已经确认的内容先固化下来，方便下一轮继续补充。

---

## 1. Metric Group Index | 指标组索引

### Entry 1

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

notes: Confirmed as a retained long-term group name in round-1 review.
```

### Entry 2

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

notes: Confirmed as a retained long-term group name in round-1 review.
```

### Entry 3

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

notes: Confirmed as a retained long-term group name in round-1 review.
```

---

## 2. Metric Index | 指标索引

这一轮仍然保留 placeholder。  
This round still keeps the metric layer as placeholders.

原因：  
Reason:

- `二、私信业务核心指标组` 与 `四、私信语音指标组` 下面的具体指标条目，本轮确认是先不强补。  
- 后续拿到更完整的指标定义后，再从 placeholder 升级成正式条目。

### Placeholder Example

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

---

## 3. Dimension Index | 维度索引

### Entry 1

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

### Entry 2

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

### Entry 3

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

---

## 4. Business Terms That Should Probably Also Enter `business_kb.md`

### Entry 1

```yaml
term: MUF
term_zh: 双关
meaning_zh: 指用户间互为关注的关系（Mutual Follow），是私信核心互动的基础关系。
meaning_en: Mutual Follow; a bilateral follow relationship that serves as a core relational foundation for DM interaction.
notes: `双关` is confirmed as the preferred Chinese term in round-1 review.
```

### Entry 2

```yaml
term: Pair
term_zh: 私信关系对
meaning_zh: 指存在私信行为的一对关系对，包含发送方和接收方，存在方向，重复行为去重。
meaning_en: A directional DM pair consisting of sender and receiver; repeated actions are deduplicated at the pair level.
notes: A→B and B→A count as two pairs; repeated A→B actions count as one pair.
```

### Entry 3

```yaml
term: Message Requests
term_zh: 消息请求
meaning_zh: TikTok 防范陌生人骚扰的机制；对未互关用户发消息时，对方先收到消息请求。
meaning_en: TikTok's anti-harassment mechanism for non-mutual users; the receiver gets a message request before full DM access is granted.
notes:
```

### Entry 4

```yaml
term: Big-moji
term_zh:
meaning_zh:
meaning_en:
notes: Keep this separate from `UGC sticker` and `Sticker panel`; do not merge them into a single `Sticker` term.
```

### Entry 5

```yaml
term: UGC sticker
term_zh:
meaning_zh:
meaning_en:
notes: Keep this separate from `Big-moji` and `Sticker panel`.
```

### Entry 6

```yaml
term: Sticker panel
term_zh:
meaning_zh:
meaning_en:
notes: Keep this separate from `Big-moji` and `UGC sticker`.
```

---

## 5. Remaining To Confirm | 仍待确认

### Should Confirm | 建议确认

1. `Big-moji`、`UGC sticker`、`Sticker panel` 的正式中文名、英文定义和边界。  
2. 如果你们后续已有正式的指标优先级体系，可以继续补 `priority_hint`。  

### Optional Follow-up | 可选补充

1. 后续拿到完整指标定义页后，把 `Metric Index` 的 placeholder 补成正式条目。  
2. 如果某些维度有固定枚举值定义，可以继续拆出 `dimension value index`。  

---

## Suggested Next Round | 建议下一轮怎么继续

你下一轮可以直接这样给：

```text
请基于 dm_glossary_v2_round1 继续修订。
需要补充：
1. Big-moji / UGC sticker / Sticker panel 的术语定义
2. 需要新增的具体指标
3. 需要补充的 polarity
4. 需要补充的维度枚举值
```

这样就可以继续往 glossary v3 收。
