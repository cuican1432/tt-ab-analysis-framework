# Runbook

## When Starting a New Case

1. Confirm the source materials.
   - PRD
   - raw data docs
   - screenshots / tables
   - optional live Libra page
2. Identify the experiment object.
3. Identify the main metrics and guardrails.
4. Build the candidate metric set.
5. Extract or read facts into Stage A.
6. Turn Stage A into Stage B logic.
7. Write Stage C as a decision-oriented memo.
8. Evaluate in Stage D when needed.

Practical reminder:

- do not start by polishing language,
- start by making sure the source set is complete,
- then make sure the metric recall set is complete,
- and only then move into writing.

## When the Source Looks Wrong

- Check whether the issue is:
  - missing data,
  - wrong extraction,
  - wrong metric match,
  - wrong interpretation.
- If source facts are wrong, rerun A from source.
- Do not patch old A output manually.

Useful triage order:

1. confirm whether the source itself is missing the field,
2. confirm whether the extraction path is wrong,
3. confirm whether the metric was matched to the wrong row,
4. confirm whether the interpretation drifted after extraction.

If the problem is in steps 1-3, fix the source read and rebuild from A.
If the problem is only in step 4, fix B/C without pretending the data changed.

## When Doing Attribution

- Start from the main movement first.
  - What is the one result that actually matters for the decision?
- Then prioritize `2-3` attribution paths that are most likely to close the loop.
- If a clear path / funnel-style chain exists, prefer considering it first because it is often easier to close the mechanism loop.
  - For example: `A -> B -> C`, such as exposure -> click -> conversion, or entry -> use -> downstream result.
- Then ask which attribution route is most promising:
  - path / funnel,
  - user composition,
  - metric formula,
  - space / cannibalization,
  - time trend,
  - data quality,
  - external or product interference.
- Use the shortest route that can explain the movement clearly.
- Do not force every case through every attribution direction.
- If a funnel chain is incomplete, use the attribution route that best explains the movement instead of forcing a funnel story.
- Prefer a closed path chain over scattered slice anecdotes when both are available.
- If attribution is still weak, label it as indirect evidence or a hypothesis to verify.

## When Writing the Report

- Lead with the decision.
- Then show the strongest evidence.
- Then surface the most decision-relevant risks.
- Then state the remaining boundary or evidence gap.
- If the experiment has multiple treatment arms, do not stop at separate arm summaries.
- In multi-arm cases, add a dedicated comparison section that answers: who is better overall, who is weaker overall, and which differences actually matter for the decision.
- Only compare fine-grained product-mechanism differences across arms when the source explicitly shows those config or description differences.

Practical writing order:

1. answer the rollout / decision question,
2. show the primary evidence,
3. show the major guardrail or downside,
4. if multi-arm, compare the arms directly and state which one wins and why,
5. explain the most credible attribution path,
6. close with the remaining uncertainty.

What to avoid:

- opening with background instead of the decision,
- piling up every significant metric into the main conclusion,
- mixing global evidence and slice evidence without saying which is which,
- sounding more certain than the evidence allows.
