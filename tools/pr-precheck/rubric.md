# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-fidelity | The diff read against the plan's stated scope, boundary, and deviation notes | Every changed file and functional modification falls strictly within the plan's in-scope boundaries or is explicitly disclosed and justified under plan deviations; unnoted additions or deletions fail | required |
| test-evidence | The test evidence section read against the plan's test plan and the repository's verification checks | Observable before-and-after command outputs verify the defect is resolved, and the repository's required test suite or checks are executed with results displayed | required |
| diff-quality | The unified diff and commit list | The diff contains only code changes necessary for the fix, completely free of debris, debug statements, commented-out dead code, formatting churn, or unrelated files | required |
| standards-compliance | The PR title and description read against the repo's PR template and contributing instructions | All required sections of the PR template are filled with substantive content (no blank fields or leftover placeholders), and required disclosures (including AI-use disclosure) are present | required |

## Verdict rule

Accept if every required check passes with "pass". If any required check receives "fail" or "unclear", the verdict is reject. Preferred checks never change the verdict. An unverifiable claim counts as fail.
