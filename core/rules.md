# Rules

## Hard Rules

- Never fabricate metrics, setup fields, or conclusions.
- Keep missing data missing.
- Keep non-significant results directional, not overstated.
- Treat PRD facts as the source of truth for experiment object and metric priority.
- Finished outputs from one experiment belong to that experiment only.
- Never reuse an old experiment's finished tables, conclusions, or report as evidence for a new experiment.

## Priority of Truth

Use this default priority:

1. prevent fabrication and copying mistakes
2. stay aligned with the PRD
3. optimize interpretation quality only after the first two are secure

## Evidence Discipline

- Global evidence drives the decision.
- Multi-dimensional evidence explains why the global result holds.
- A single extreme slice is supporting evidence only.
- Do not mix global evidence and slice evidence at the same level without labeling the distinction.
- If platform-level guardrails are missing, keep the final recommendation correspondingly conservative.

## Metric Tiering

Use three default tiers:

- `Tier A`
  - PRD targets, business-core metrics, and success metrics
  - used for the main conclusion and deeper attribution
- `Tier B`
  - company-core metrics, app-level must-watch metrics, DAU, retention, performance, and major side effects
  - used for guardrails, transmission effects, and rollout-risk judgment
- `Tier C`
  - long-tail metrics and important slice anomalies not already covered by Tier A or Tier B
  - used for monitoring, risk supplementation, and anomaly logging

Do not let Tier C dominate the main conclusion unless the source explicitly proves it should.

## Recall and Priority

Separate these two questions:

1. what must be recalled into the analysis universe
2. what deserves to be elevated into the main conclusion

Default recall universe:

- `Tier A`
- `Tier B` core / must-watch metrics
- metrics explicitly named in the PRD as targets or guardrails
- global significant results, defaulting to `p < 0.05`
- key-dimension significant results, defaulting to `p < 0.03`

Priority rules:

- recall does not automatically mean elevation
- the main conclusion should usually keep only `1-3` top results
- ordering should follow the primary PRD objective
- recalled-but-nonprimary metrics should be downgraded into:
  - monitoring and risk,
  - long-tail anomaly sections,
  - stable guardrail lists,
  - or appendices

## Attribution Discipline

Use evidence from three equal routes:

- physical / layout evidence,
- mechanism / transmission-chain evidence,
- drilldown / slice evidence.

When useful, label claims as:

- `[direct evidence]`,
- `[indirect evidence]`,
- `[hypothesis to verify]`.

Use whichever route closes the explanation loop best.

Do not invent psychology or user motivation without hard support.

## Metric-Caliber Discipline

Before interpreting an anomaly, align:

- definition,
- denominator,
- dedup rule,
- window,
- time granularity.

If caliber is unclear, do not make a strong claim.

Treat `DAU` as a scale / sample-size signal, not as a direct treatment-effect conclusion.

## Report Discipline

- Write the report as a decision memo, not a data dump.
- Use business themes, not raw page order, as the main narrative structure.
- Keep risk and benefit at the same level of visibility.
- Name representative metrics and values when making a business-theme claim.
- When evidence is insufficient, explicitly separate:
  - what is confirmed,
  - what is not confirmed,
  - and what is only directional.
- Prefer conservative, clear, reviewable writing over polished but weakly supported writing.
