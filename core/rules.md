# Rules

## Hard Rules

Maintainer-owned. Do not casually change this section.

- Never fabricate metrics, setup fields, or conclusions.
- Keep missing data missing.
- Keep non-significant results directional, not overstated.
- Treat PRD facts as the source of truth for experiment object and metric priority.
- If the PRD includes product images, screenshots, or visual comparison tables, treat them as part of the source evidence when the runtime can read images.
- Finished outputs from one experiment belong to that experiment only.
- Never reuse an old experiment's finished tables, conclusions, or report as evidence for a new experiment.

## Default Rules

Framework defaults live here. These rules are stable and should be changed carefully, but they are not as absolute as the hard rules above.

### Priority of Truth

Use this default priority:

1. prevent fabrication and copying mistakes
2. stay aligned with the PRD
3. optimize interpretation quality only after the first two are secure

### Evidence Discipline

- Global evidence drives the decision.
- Multi-dimensional evidence explains why the global result holds.
- A single extreme slice is supporting evidence only.
- Do not mix global evidence and slice evidence at the same level without labeling the distinction.
- If platform-level guardrails are missing, keep the final recommendation correspondingly conservative.

For significance reading:

- treat global metrics with the standard `p < 0.05` threshold unless the source specifies otherwise
- treat key slice / segment signals more conservatively, defaulting to `p < 0.03`
- even when a slice passes `p < 0.03`, do not elevate it alone unless direction, adjacent metrics, and business logic also support it
- if a narrow slice is significant but the global result and nearby slices do not support it, treat it as monitoring or a hypothesis to verify
- when checking heterogeneity, it is valid to note that some local gains may not fully show up at the overall level; if structure information is incomplete, keep this as a cautious heterogeneity note or a hypothesis to verify

### Metric Tiering

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

### Recall and Priority

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

### Attribution Discipline

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
When reading product-mechanism differences from a PRD, read concrete deltas at the feature level: entry points, triggers, page flow, permissions, supported objects, interaction changes, and effect scope.
When possible, connect attribution as a usable chain rather than a loose observation list:

- product / UX delta,
- the most credible mechanism, path, or structural change,
- metric movement,
- business implication,
- and the remaining uncertainty or next validation step.

Prefer this kind of chain when the source supports it, but do not force a fake chain when the middle steps are missing.

When investigating attribution, check the most relevant of these directions:

- path attribution
  - funnel breaks, step-level explosions, and downstream linkage
- user attribution
  - segment composition, new vs existing users, platform / device / frequency layers
- formula attribution
  - factor decomposition, stock vs incremental effects
- space attribution
  - internal cannibalization, module competition, spillover effects
- time attribution
  - novelty effects, delayed effects, and trend decay
- data-quality attribution
  - when available, check SRM, outliers, pre-period imbalance, and instrumentation issues
  - if the source does not expose assignment counts, split quality, or baseline checks, do not pretend this validity check was completed
- external / product attribution
  - app version changes, bugs, campaigns, ops interference, button conflicts, or accidental taps

Do not try to force every attribution through all directions. Use the directions that can actually explain the movement.

### Metric-Caliber Discipline

Before interpreting an anomaly, align:

- definition,
- denominator,
- dedup rule,
- window,
- time granularity.

If caliber is unclear, do not make a strong claim.

Treat `DAU` as a scale / sample-size signal, not as a direct treatment-effect conclusion.

### Report Discipline

- Write the report as a decision memo, not a data dump.
- Use business themes, not raw page order, as the main narrative structure.
- Keep risk and benefit at the same level of visibility.
- Name representative metrics and values when making a business-theme claim.
- For each major benefit or risk, try to explain not just what moved, but what business theme it represents.
- When the source is strong enough, push the write-up one layer deeper than metric listing:
  - what changed in the product,
  - which user path was likely affected,
  - which metrics moved,
  - what that means for the business,
  - and what still needs validation.
- For multi-arm experiments, do not describe each arm in isolation only.
- For multi-arm experiments, explicitly state which arm is better, which arm is weaker, and what the decision implication is.
- If there are multiple treatment arms, include a dedicated comparison section so the reader can see the strict arm-to-arm differences, not just separate summaries.
- Only make detailed product-mechanism comparisons when the source explicitly exposes the relevant configuration or description differences for those arms.
- Do not stop at "risk exists" or "benefit exists" when the report needs to support action. If the source allows it, add the most reasonable next action, validation ask, or rollout implication.
- When evidence is insufficient, explicitly separate:
  - what is confirmed,
  - what is not confirmed,
  - and what is only directional.
- Prefer conservative, clear, reviewable writing over polished but weakly supported writing.
