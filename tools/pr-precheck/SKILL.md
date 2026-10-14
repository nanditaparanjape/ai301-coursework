---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

This tool answers exactly one question about a candidate PR package: is this pull request ready to submit? A PR package consists of the candidate PR title, description, commits, unified diff, and test evidence, evaluated against the plan it claims to implement and the target repository standards.

## Inputs and modes

- Live mode: Evaluates the student's local changes before opening a pull request. Inputs are the plan with any deviation notes in `plan.md`, the branch diff from `git diff main...HEAD`, the draft title and description in `pr_draft.md`, and captured verification output in `test_evidence.md`, evaluated against the target repository's PR template and contributing guidelines. For house-chain workflows, inputs are read from the assigned house plan and repro pack.
- Eval mode: Evaluates a standalone frozen package bundle (`calib-*.json` or `pkg-*.json`). The bundle contains the complete evaluation context; no external network requests or local files are read. Every check runs against the bundle text.

## The scope seam (live mode only)

In live mode, read `scope.md` before executing any checks. Verify that the repository target matches the `Repo:` definition in `scope.md`. If the `Repo:` line contains an unfilled placeholder, stop execution immediately and instruct the user to set the repository path in `scope.md`. Eval mode ignores `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and evaluate the PR title and description in `pr_draft.md` against its rules. Report any stylistic or tone infractions in the evaluation summary. The voice guide does not alter the pass/fail verdict unless a specific check in `rubric.md` references it. Eval mode ignores `voice-guide.md` entirely.

## Component reads

- `rubric.md` defines the four checks (`plan-fidelity`, `test-evidence`, `diff-quality`, and `standards-compliance`) and the verdict aggregation rule.
- `references/evidence-guide.md` maps where each category of evidence resides and what valid evidence requires.
- `procedure.md` provides the sequential operational steps for reading artifacts, gathering facts, executing checks, and determining the verdict. Follow `procedure.md` as written without omitting steps. If `rubric.md` or `procedure.md` is empty or unpopulated, refuse to grade.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject` (hold). The tool provides a readable per-check breakdown, followed by the mandatory JSON block as the very last element of the response with nothing after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}


```
