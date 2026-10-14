# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

- Where it lives: In an eval bundle, in `plan_context_markdown` (under Diagnosis, Scope, and Deviations) read against `pr.diff` and `pr.description`. In live mode, in `plan.md` read against `git diff main...HEAD` and `pr_draft.md`.
- What good looks like: Every changed file and functional modification in the diff matches the plan's in-scope targets. Any change outside the original plan is explicitly documented and justified under the Deviations heading. The PR description accurately describes the diff without exaggerating or omitting changes.

## Test evidence (harness category: not-tested)

- Where it lives: In an eval bundle, in `pr.test_evidence`. In live mode, in `test_evidence.md` and the Testing section of `pr_draft.md`.
- What good looks like: Explicit command invocations showing the failing reproduction before the fix, the passing reproduction after the fix, and passing test results for the repository's standard test checks (e.g., unit test suite output).

## Diff quality (harness category: unreviewable)

- Where it lives: In an eval bundle, in `pr.diff` and `pr.commits`. In live mode, in `git diff main...HEAD` and `git log main..HEAD`.
- What good looks like: The diff is strictly scoped to the defect fix. It contains zero debugging statements (such as `print()` or `console.log`), zero commented-out code blocks, zero arbitrary whitespace reformats, and no unintended auxiliary files.

## Standards and comms (harness category: standards-wall)

- Where it lives: In an eval bundle, in `repo_facts` read against `pr.title` and `pr.description`. In live mode, in `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` read against `pr_draft.md`.
- What good looks like: Every heading of the PR template contains meaningful, project-specific content. The target issue number is explicitly linked (e.g., `Closes #...`), and the mandatory AI-use disclosure is fully stated in the Notes for Reviewers section.
