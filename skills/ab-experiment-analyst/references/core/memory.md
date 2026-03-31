# Memory

## Stable Working Memory

- Prefer doc-first analysis.
- Use live Libra extraction only when it is truly needed.
- New experiments must be analyzed from their own source materials.
- Old experiment outputs are not valid evidence for new experiments.
- Global metrics are the main decision evidence.
- Drilldown and slice analysis are supporting evidence unless the task explicitly centers on drilldown.

## Artifact Convention

- Store outputs under:

```text
experiment/<experiment_id>/version_<yyyymmdd>/
```

- Keep A / B / C / D outputs together under the same version directory.
- If the same experiment is rerun, create a new version directory instead of overwriting the old one.
