# Unit 1: Issue Selection

## Issue link
[https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72)

## Verdict output
```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Human commit by Andrew Burke on Sep 16, 2026, within 60-day window"},
      {"name": "repo-active", "grade": "pass", "evidence": "Most recent default-branch commit Sep 16, 2026, within 80-day threshold"},
      {"name": "not-claimed", "grade": "pass", "evidence": "No assignees, no linked PRs, and no claim comments on the thread"},
      {"name": "scope-fit", "grade": "pass", "evidence": "Bounded bug fix: catch UnknownHashError in core/security.py and return False; remove one @pytest.mark.xfail marker"},
      {"name": "ai-policy-allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md is silent on AI-assisted contributions; silence passes"},
      {"name": "beginner-friendly", "grade": "pass", "evidence": "Labeled 'good first issue' and 'tier-1 (Starter difficulty)'"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Human commit by Andrew Burke on Sep 16, 2026, within 60-day window"},
      {"name": "repo-active", "grade": "pass", "evidence": "Most recent default-branch commit Sep 16, 2026, within 80-day threshold"},
      {"name": "not-claimed", "grade": "pass", "evidence": "Classmate claim comment does not block per Path Review house rules"},
      {"name": "scope-fit", "grade": "pass", "evidence": "Bounded bug fix: add empty-corpus guard in rag/retriever/keyword_search.py; remove one @pytest.mark.xfail marker"},
      {"name": "ai-policy-allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md is silent on AI-assisted contributions; silence passes"},
      {"name": "beginner-friendly", "grade": "pass", "evidence": "Labeled 'good first issue' and 'tier-1'"}
    ],
    "verdict": "accept"
  }
]
```
## Run history
1. First run: 11/20 PASS (strict 3-day maintainer and 5-day commit windows; missing AI policy check)
2. Final run: 18/20 PASS (expanded maintainer window to 90 days, commit window to 80 days, and added explicit AI contribution check)

## Issue analysis
In the benchmark evaluation, issue-19 was marked as a gold accept but resulted in a reject verdict because it failed scope-fit and beginner-friendly (preferred). The issue body was perceived as broader in scope due to ambiguous task wording, triggering the strict boundaries of the scope-fit rule. While gold labeled it acceptable for a beginner, the rubric rejected it because it lacked explicit single-function boundaries.

## Check rationale
* `maintainer-alive`: Evaluates whether "median response time is 90 days or less, OR at least 1 human commit on the default branch in the last 60 days, OR a maintainer commented in the thread". This prevents contributing to projects where PRs go unreviewed.
* `repo-active`: Verifies "At least 1 commit within the last 80 days of the capture date" to confirm general codebase activity.
* `not-claimed`: Checks that "assignee is none and no open PR linked or recent comment claiming it" so work is not duplicated.
* `scope-fit`: Verifies that "fix touches 3 or fewer files, targets a single function or localized component, and issue body contains no multi-item task checklist" to prevent students from tackling sprawling refactors.
* `ai-policy-allowed`: Verifies repository "does not state an outright ban on AI-assisted contributions. silence, disclosure requirements, and human review conditions pass" to ensure workflow compliance.
* `beginner-friendly`: Checks if issue is "Labeled 'good first issue', 'beginner-friendly', or marked for newcomers" as a preferred ranking signal.

## Selection rationale
Issue #72 was chosen because it passed all five required checks and satisfied the preferred beginner-friendly check. It targets a clear exception handling bug in core/security.py where passlib raises an UnknownHashError on invalid hashes instead of returning False. The fix is isolated to a single function, requires updating one test in tests/unit/test_security.py by removing an @pytest.mark.xfail decorator, and does not require complex architecture or schema changes.

## Trade-offs
The rubric prefers quick, contained bug fixes over big features or broad docs rewrites. It will take a short, bare-bones issue description if the code fix itself is small, but it immediately filters out messy multi-part checklist tasks even if they have a beginner tag.
