# Dimension Index | 维度索引

## Entry

```yaml
dimension_name: By Entrance
dimension_aliases:
  - 入口拆分

meaning_zh: 按入口来源拆分行为表现的维度。
meaning_en: A dimension that splits behavior by product entry source.

applies_to_groups:
  - DM Core
  - DM Group Chat

applies_to_metrics:

value_examples:
  - share
  - group_chat_entry
  - conversation_detail

warnings: Use this dimension to explain path differences, but do not let one entrance slice override the global result by itself.
```

## Entry

```yaml
dimension_name: By Msg Type
dimension_aliases:
  - 消息类型拆分

meaning_zh: 按消息类型拆分行为表现的维度，如 text、emoji、voice、sticker、camera。
meaning_en: A dimension that splits behavior by message type such as text, emoji, voice, sticker, or camera.

applies_to_groups:
  - DM Core
  - DM Voice Message

applies_to_metrics:

value_examples:
  - text
  - emoji
  - voice
  - sticker
  - camera

warnings: Useful for heterogeneity and expression-style analysis, but should remain supporting evidence unless the source strongly proves otherwise.
```

## Entry

```yaml
dimension_name: By Motivation
dimension_aliases:
  - 动机拆分

meaning_zh: 按互动或发送动机拆分表现的维度。
meaning_en: A dimension that splits performance by interaction or sending motivation.

applies_to_groups:
  - DM Core
  - DM Group Chat

applies_to_metrics:

value_examples:
  - social
  - share
  - creator_message

warnings: Motivation-based slices are useful for interpretation, but should be treated carefully when the source does not fully explain the classification logic.
```
