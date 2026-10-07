# Procedure: how this skill grades a plan package

## Read order

1. Read the issue description and thread highlights first to understand the reported problem, user expectations, and any maintainer constraints or guidance.
2. Read the reproduction evidence second to identify the exact verified failure mode, commands executed, error traces, and observable outputs.
3. Read the repository facts and contributing guidelines third to record repository-specific conventions (e.g., testing conventions, communication tone, AI disclosure requirements).
4. Read the plan document (`plan.md`) fourth, noting the stated diagnosis, proposed scope boundaries, touched files, implementation steps, test verification steps, and risks/unknowns.
5. Read the draft comment (`comment.md`) last to check how the proposed plan is communicated upstream against the issue thread and repository guidelines.

## Evidence gathering

1. For `diagnosis-consistent`: Extract the root cause and mechanism stated in the plan. Compare directly against the reproduced failure output and error traces extracted in Read Order Step 2.
2. For `scope-bounded`: Extract the files to touch and modification list from the plan. Verify that every change targets the root cause and that no unrelated feature work or wide refactorings are planned.
3. For `steps-actionable`: Locate the approach and discrete steps in the plan. Check whether exact functions, modules, and changes are explicit enough for another developer to execute without ambiguity.
4. For `test-verifiable`: Extract the test plan commands and assertions. Confirm they either re-run the repro steps or add automated tests demonstrating a before-and-after behavioral difference.
5. For `risks-identified`: Locate the risks, unknowns, or edge cases section. Note whether potential side effects or uncertainties are honestly identified rather than treated as non-existent.
6. For `conventions-observed`: Inspect the draft comment text against repository conventions and the thread history gathered in Read Order Steps 1 and 3, checking for required disclaimers, proper tone, and alignment with maintainer instructions.

## Check execution

1. Grade each check in strict sequence:
   - `diagnosis-consistent`
   - `scope-bounded`
   - `steps-actionable`
   - `test-verifiable`
   - `risks-identified`
   - `conventions-observed`
2. Evaluate each check against its pass condition in `rubric.md`.
3. If an evidence item required by a check is completely missing from the submission (e.g., no test plan provided, missing risks section), mark that check as `fail`.
4. If evidence is ambiguous, contradictory, or cannot be evaluated definitively against the criteria, mark the check as `unclear`.

## Verdict assembly

1. Review the assigned grade for each check in the checks table.
2. If all required checks are graded `pass`, assemble a final verdict of `accept`.
3. If any required check is graded `fail` or `unclear`, assemble a final verdict of `reject`.
4. In the output JSON block, list every check with its assigned grade (`pass`, `fail`, or `unclear`) and quote the specific evidence snippet that determined the grade for failing or deciding checks.
