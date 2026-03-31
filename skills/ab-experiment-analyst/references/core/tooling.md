# Tooling

## Default Tool Preference

- Prefer local files and structured docs first.
- If browser work is needed, prefer:
  - `openclaw`
  - `browser playwright mcp`
- Use direct CDP only as a fallback when the browser is already open but the gateway path is unstable.

## Tooling Principle

- Prefer scriptable, traceable steps over manual one-off handling.
- Prefer structured extraction over copy-paste summaries.
- Prefer validators when label fidelity or row fidelity matters.

## Browser Note

When live Libra extraction is required:

- reuse the same tab when possible,
- avoid repeated reopen / refocus churn,
- keep provenance when available.
