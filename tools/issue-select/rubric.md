# Rubric: is this a good first issue?


1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.


## Checks

| Check | Evidence | Pass condition | Weight |
| maintainer-alive | "maintainer first-response sample" under repo facts | median response time is 90 days or less, OR at least 1 human commit on the default branch in the last 60 days, OR a maintainer commented in the thread | required |
| repo-active | "last 5 default-branch commits" under repo facts | At least 1 commit within the last 80 days of the capture date | required |
| not-claimed | "this issue: assignees:" under repo facts, comments | assignee is none and no open PR linked or recent comment claiming it | required |
| scope-fit | issue body, comments, files changed | fix touches 3 or fewer files, targets a single function or localized component, and issue body contains no multi-item task checklist | required |
| ai-policy-allowed | "contribution policy" line under repo facts | does not state an outright ban on AI-assisted contributions. silence, disclosure requirements, and human review conditions pass | required |
| beginner-friendly | issue labels | Labeled "good first issue", "beginner-friendly", or marked for newcomers | preferred |

## Verdict rule

an issue is accepted if and ONLY IF every `required` check evaluates to PASS. If any `required check` evaluates to FAIL or UNCLEAR, the issue is rejected.
`preferred` checks should never change the accept or reject verdict. 
