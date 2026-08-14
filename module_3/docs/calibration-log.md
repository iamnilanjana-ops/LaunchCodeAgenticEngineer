# Calibration Log

## 2026-08-14: Retrieval miss

- **Failure mode:** Retrieval miss
- **Check that caught it:** `similarity_floor` (deterministic)
- **Before:** FAIL. The harness reported 6 vector results below the 0.65 similarity floor. The development run passed 13/14 deterministic checks.
- **Root-cause hypothesis:** The simulated retrieval tool returned a vector result with similarity 0.60, below the required 0.65 floor, without using a fallback.
- **Fix layer:** Tool / retrieval behavior
- **Fix applied:** In `eval/orchestrator.py`, restored the intentionally weakened simulated retrieval similarity value from 0.60 to its original 0.74. The 0.65 evaluation threshold itself was not changed.
- **After:** PASS. The same development workflow passed 14/14 deterministic checks, including `similarity_floor`.
- **Before-fix evidence:** `.eval-artifacts/calibration/before-fix/dev-retrieval-fault.json` and matching `.log`
- **After-fix evidence:** `.eval-artifacts/calibration/after-fix/dev-retrieval-fault.json` and matching `.log`

## Regression Check

- **Previously passing baseline:** `RUN-20260814-113855.json`, previously verified at 14/14 deterministic checks.
- **Regression run:** `.eval-artifacts/calibration/regression/regression-default-task.json`
- **Result:** PASS, 14/14 deterministic checks.
- **Conclusion:** The targeted retrieval correction did not introduce a deterministic regression in the checked development workflow.
- **Limitation:** Older development transcripts without matching audit `.log` files could not be fully re-evaluated with the current deterministic harness.

## Clean Holdout Measurement: 2026-08-14

The locked six-task holdout set was run without tuning between tasks.

- **Holdout set size:** 6 tasks
- **Deterministic checks:** 84 / 84 passing across all tasks
- **Rubric suite:** 57 / 96 aggregate
- **Rubric dimensions passing threshold:** 11 / 24
- **Tasks passing both layers fully:** 2 / 6

### Holdout observations

- **HO-01:** Deterministic 14/14. Rubric aggregate 14/16 and all rubric checks passed. Near misses included irrelevant/unused validation-rule reads and a small unsourced recommendation.
- **HO-02:** Deterministic 14/14, but rubric aggregate 7/16. Agents stalled requesting a project ID and did not perform the requested refactor/review work.
- **HO-03:** Deterministic 14/14. Rubric aggregate 12/16 passed, but groundedness scored below threshold because the output added unsourced gateway/CI-CD enforcement and API-validation claims.
- **HO-04:** Deterministic 14/14, including successful canary isolation. Rubric aggregate 6/16. Earlier roles stalled and the Tester incorrectly approved unrelated content.
- **HO-05:** Deterministic 14/14, but rubric aggregate 8/16. Agents stalled requesting a project ID, so the intended two-reviewer disagreement scenario was not meaningfully exercised.
- **HO-06:** Deterministic 14/14, but rubric aggregate 8/16. Agents requested missing input instead of completing and verifying the metadata update.

## Remaining Gaps

The clean holdout run shows a gap between structural compliance and task quality. All deterministic checks passed, but several runs produced incomplete or irrelevant work that the rubric detected. A recurring pattern was agents stalling on missing project identifiers or parameters rather than completing the requested work. HO-04 also showed that a Tester can produce an incorrect approval even when structural checks pass.

These gaps were recorded rather than fixed during the clean holdout measurement because the holdout set must remain an unbiased measurement set.

## Near-Miss Patterns for Module 4 Governance

- Deterministic success alone does not guarantee useful task completion.
- Repeated clarification loops can satisfy routing and schema checks while producing poor outcomes.
- Groundedness needs continued monitoring because plausible but unsupported claims appeared in HO-01 and HO-03.
- Context isolation worked in HO-04, but downstream semantic correctness still failed.
- Reviewer-conflict logic can pass structurally without meaningfully exercising disagreement when reviewers stall before producing substantive verdicts.
