# Metric Group Index | 指标组索引

## Entry

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

notes:
```

## Entry

```yaml
group_name: DM Voice Message
group_aliases:
  - 私信语音指标组

description_zh: 私信语音消息相关指标组，通常用于观察语音录制、取消、发送等行为。
description_en: A DM voice-message metric group that usually covers recording, canceling, and sending voice messages.

usage_scope: DM / direct message experiments
is_company_core:
is_business_core: true
is_sub_business_core: true

typical_usage: often used when a DM experiment may affect voice-message creation or usage
priority_hint: P1

common_dimensions:
  - By Msg Type

notes:
```

## Entry

```yaml
group_name: DM Group Chat
group_aliases:
  - 私信群聊指标组

description_zh: 私信群聊相关指标组，通常用于观察群聊进入、发送、互动与创建行为。
description_en: A DM group-chat metric group that usually covers entering, sending, interacting, and creating group chats.

usage_scope: DM / social interaction experiments
is_company_core:
is_business_core: true
is_sub_business_core: true

typical_usage: often used when a DM experiment may spill over into group-chat behavior
priority_hint: P1

common_dimensions:
  - By Entrance
  - By Motivation

notes:
```
