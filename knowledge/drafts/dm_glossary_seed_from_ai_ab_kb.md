# DM Glossary Seed Draft | 私信知识库首版整理稿

Source | 来源：

- [【AI+AB】私信知识库](https://bytedance.larkoffice.com/wiki/XVoNwDn7piwyKukCRWNcXMD1nId)

Purpose | 用途：

- 这是基于现有知识库整理出的**第一版结构化 glossary 初稿**。  
- 能确认的字段先填。  
- 不能确认的字段先留空。  
- 最后附一段 `To Confirm`，方便你下一轮修订。

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
  - by entrance
  - by msg type
  - by motivation

notes: Group name visible in linked DM-related materials and repeatedly referenced as a core analysis unit.
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

notes: Mentioned by the knowledge-base structure, but detailed metric content was not fully expanded in the visible section.
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

notes: Mentioned in the business-intro section as part of the DM product surface, but metric details still need confirmation.
```

---

## 2. Metric Index | 指标索引

这轮 source 可见部分主要是业务术语和结构说明，**单个指标定义并没有完整展开**。  
The visible part of the source focused more on business terms and structure, so single-metric definitions were not fully expanded.

先放一个模板化 placeholder，等你们下一轮补。  
Below is a placeholder entry shape for the next round.

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

meaning_zh: 行为维度下钻，表示私信消息类型，如 Text、Emoji 等。
meaning_en: A behavioral drilldown dimension that shows DM message types such as Text and Emoji.

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
notes:
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

---

## 5. To Confirm | 待确认

你不需要自己通篇找问题，优先看下面这份确认清单就可以。  
You do not need to scan the whole draft for gaps. Start from this review list.

### Must Confirm | 必须确认

1. `DM Core`、`DM Voice Message`、`DM Group Chat` 这些指标组的正式命名，是否和你们 raw data / report 里的命名完全一致。  
2. `二、私信业务核心指标组` 和 `四、私信语音指标组` 下面的**具体指标条目**，这轮可见区域没有完整展开，建议下一轮补进。  
3. `MUF` 中文原文写成了“**双关**”，这看起来像 OCR 或写法问题；建议确认是不是应该改成“**双关 / 互关**”中的某个正式版本。  

### Should Confirm | 建议确认

1. `By Entrance / By Msg Type / By Motivation` 这三个维度的**正式英文名**是否固定，就按 source 里的大小写和拼法来。  
2. `Sticker` 当前在知识库里被描述为“贴纸消息”，但原文里同时出现了 `Big-moji / UGC sticker / Sticker pannel`，建议下一轮统一术语。  

### Optional Follow-up | 可选补充

1. 如果你们已经有更正式的指标优先级定义，可以补 `priority_hint`。  
2. 如果后面能拿到完整指标定义页，再把 `Metric Index` 里的 placeholder 补成正式条目。  

---

## Suggested Next Round | 建议下一轮怎么给我

你下一轮可以直接这样给：

```text
请基于这版 glossary 初稿继续修订。
需要修改：
1. 哪些指标组名称要改
2. 哪些指标要补
3. 哪些维度口径要补
4. 哪些 polarity 要确认
5. 哪些术语解释不对
```

这样我就可以把这版初稿收成更正式的 glossary v2。
