# Rules

## Hard Rules

- Never fabricate metrics, setup fields, or conclusions.
- Keep missing data missing.
- Keep non-significant results directional, not overstated.
- Treat PRD facts as the source of truth for experiment object and metric priority.
- Completed A / B / C / D outputs are case-local only.
- Never reuse one experiment's finished outputs as evidence or template for a new experiment.

## Evidence Discipline

- Global evidence drives the decision.
- Multi-dimensional evidence explains why the global result holds.
- A single extreme slice is supporting evidence only.
- Do not mix global evidence and slice evidence at the same level without labeling the distinction.
- If platform-level guardrails are missing, keep the final recommendation correspondingly conservative.

## Attribution Discipline

Use evidence from three equal routes:

- physical / layout evidence,
- mechanism / transmission-chain evidence,
- drilldown / slice evidence.

When useful, label claims as:

- `[direct evidence]`,
- `[indirect evidence]`,
- `[hypothesis to verify]`.

Do not invent psychology or user motivation without hard support.

## Metric-Caliber Discipline

Before interpreting an anomaly, align:

- definition,
- denominator,
- dedup rule,
- window,
- time granularity.

If caliber is unclear, do not make a strong claim.

## Report Discipline

- Write the report as a decision memo, not a data dump.
- Use business themes, not raw page order, as the main narrative structure.
- Keep risk and benefit at the same level of visibility.
- Name representative metrics and values when making a business-theme claim.
