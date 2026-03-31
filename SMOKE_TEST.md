# Smoke Test

This file is a practical checklist for validating that the framework can be downloaded, installed, and referenced correctly.

## Goal

Verify three things:

1. the repository can be cloned,
2. the main skill can be installed locally,
3. the installed skill can still resolve its internal references.

## Recommended Test Environment

- a clean local folder
- a temporary Codex-style home directory
- no dependency on the original author workspace

## Step 1: Clone

```bash
mkdir -p ~/ab-workspace
cd ~/ab-workspace
git clone https://github.com/cuican1432/tt-ab-analysis-framework.git
cd tt-ab-analysis-framework
```

Expected result:

- repository downloads successfully
- `skills/tt-ab-analysis-framework/SKILL.md` exists
- `skills/tt-ab-analysis-framework/references/` exists

## Step 2: Install the Main Skill

```bash
mkdir -p ~/.codex/skills/tt-ab-analysis-framework
cp -R skills/tt-ab-analysis-framework/. ~/.codex/skills/tt-ab-analysis-framework/
```

Expected result:

- `~/.codex/skills/tt-ab-analysis-framework/SKILL.md` exists
- `~/.codex/skills/tt-ab-analysis-framework/references/core/` exists
- `~/.codex/skills/tt-ab-analysis-framework/references/knowledge/` exists

## Step 3: Check Internal References

The installed main skill should still be able to resolve:

- `./references/core/index.md`
- `./references/core/workflow.md`
- `./references/core/rules.md`
- `./references/core/memory.md`
- `./references/core/runbook.md`
- `./references/core/tooling.md`
- `./references/knowledge/metric_glossary.md`
- `./references/knowledge/business_kb.md`

Expected result:

- all referenced files exist after installation

## Step 4: Check Main Skill Intent Coverage

Open `~/.codex/skills/tt-ab-analysis-framework/SKILL.md` and confirm it still clearly supports:

- knowledge ingestion
- experiment report generation
- report generation with temporary metric or rule guidance

Expected result:

- all three usage modes are still visible in the installed skill

## Step 5: Optional Helper Skills

If helper skills are installed, verify:

- `~/.codex/skills/ab-experiment-analyst/SKILL.md`
- `~/.codex/skills/ab-metric-glossary/SKILL.md`

Expected result:

- both helper skills exist and can be read
- both helper skills keep their own `references/core/` and `references/knowledge/` folders after installation

## Step 6: Helper Skill Reference Check

If helper skills are installed, also verify these paths:

- `~/.codex/skills/ab-experiment-analyst/references/core/index.md`
- `~/.codex/skills/ab-experiment-analyst/references/core/workflow.md`
- `~/.codex/skills/ab-experiment-analyst/references/knowledge/metric_glossary.md`
- `~/.codex/skills/ab-metric-glossary/references/core/index.md`
- `~/.codex/skills/ab-metric-glossary/references/core/rules.md`
- `~/.codex/skills/ab-metric-glossary/references/knowledge/metric_glossary.md`

Expected result:

- helper-skill references also resolve after installation

## Pass Criteria

The smoke test passes when:

- clone succeeds,
- installation succeeds,
- the main skill remains self-contained after installation,
- the referenced `core` and `knowledge` files are present,
- the three main usage modes are still visible,
- and optional helper skills remain self-contained when installed.

## Notes

- The main skill is designed as a self-contained package.
- Copying only `SKILL.md` is not enough; copy the entire skill directory.
- The `cp -R .../. target/` pattern is preferred over `cp -R .../* target/` because it is more robust across environments.
