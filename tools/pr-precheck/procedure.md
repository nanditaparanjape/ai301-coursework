# Procedure: how this tool grades a PR package

## Read order

1. Read the plan context completely, noting down the in-scope files, out-of-scope boundaries, expected behavior changes, and any recorded deviation notes.
2. Read the repo-facts block (or repository PR template and contributing policy in live mode) to identify all required PR template sections, testing requirements, and disclosure policies.
3. Read the candidate PR title and description, identifying claimed changes, linked issues, and stated testing outcomes.
4. Read the unified diff and commit history, comparing changed files and line hunks directly against the plan scope.
5. Read the test evidence section, checking observed outputs against the plan's test plan and the repo's check results.

## Evidence gathering

- For `plan-fidelity`: Compare the file list and logic changes in the diff against the plan's scope and deviation notes. Record any unnoted file modifications or omitted plan commitments.
- For `test-evidence`: Check the test evidence block for concrete before-and-after reproduction commands and outputs, plus verification test suite runs. Record missing command outputs or unverified assertions.
- For `diff-quality`: Inspect every hunk of the diff for debugging print statements, commented-out dead code, syntax debris, whitespace/formatting churn, or unrelated file modifications.
- For `standards-compliance`: Check each section of the PR description against the template asks. Verify the issue reference is present, all checklist boxes are addressed, and the AI-use disclosure is provided.

## Check execution

Execute the checks in exact table order: `plan-fidelity`, `test-evidence`, `diff-quality`, and `standards-compliance`.
- If evidence for a check is absent or incomplete in the package, assign a grade of `fail` with an evidence line noting the missing artifact.
- Formulate each evidence string as a single concise line citing the specific fact, file, or quote that determined the grade.

## Verdict assembly

1. Evaluate all required checks against the gathered evidence.
2. If all four required checks pass, emit the verdict `accept`.
3. If one or more required checks fail or are unclear, emit the verdict `reject`.
4. Quote the exact finding of the first failing required check in the summary explanation.
5. Format the machine output as the final fenced JSON block according to CONTRACT.md with no text following it.
