# Metric Glossary Guide | 指标字典说明

这个文件用于解释：
- glossary 怎么组织
- 字段是什么意思
- draft 和 formal 怎么流转
- 用户怎么更新 glossary

正式入库内容请看：
- `knowledge/metric_glossary.md`
- `knowledge/glossary/`

## Design Principle | 设计原则

glossary 不建议揉成一张大表。推荐分成三层：

1. `Metric Group Index | 指标组索引`
2. `Metric Index | 指标索引`
3. `Dimension Index | 维度索引`

原因：

- 指标组是召回和组织单位
- 指标是解释和归因单位
- 维度是下钻和切片单位

## Key Terms | 关键字段说明

### `polarity`

表示这个指标往哪个方向变通常更好。

建议只用：
- `higher_is_better`
- `lower_is_better`
- `depends_on_context`
- `descriptive_only`

### `typical_usage`

表示这个组或指标通常怎么被使用，不是当前实验的最终角色。

### `priority_hint`

表示这项内容在组内或解释时的常见优先级提示。

## Templates | 模板

### Metric Group Template

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

### Metric Template

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

### Dimension Template

```yaml
dimension_name:
dimension_aliases:
  -

meaning_zh:
meaning_en:

applies_to_groups:
  -

applies_to_metrics:

value_examples:
  -

warnings:
```

## Draft vs Formal | 草稿和正式库

### Formal

放在：
- `knowledge/glossary/`

特点：
- 已确认
- 可复用
- 不带待确认项
- 不带 case-specific 结论

### Draft

放在：
- `knowledge/drafts/`

特点：
- 已整理但未定稿
- 允许空字段
- 允许 `to confirm`
- 允许 placeholder

## Update Loop | 更新流程

推荐协作方式：

1. 用户给原始知识库或零散知识
2. 先整理成 glossary draft
3. 主动输出 `to confirm`
4. 用户用中文优先确认关键字段
5. confirmed 条目分批进入正式库
6. unfinished 内容继续留在 drafts

不要让用户自己通篇找问题。
