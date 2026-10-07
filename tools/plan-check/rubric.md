# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-consistent | Plan's stated root cause and mechanism compared against the repro evidence and observed failure output | Pass if the diagnosis correctly explains the reproduced failure and directly addresses the underlying cause shown in the repro evidence rather than merely masking the visible symptom. | required |
| scope-bounded | Plan's scope statement, target files, and proposed modifications compared against the issue description and root cause | Pass if the proposed edits are strictly focused on fixing the diagnosed cause without expanding into unrelated refactoring, feature additions, or unbounded architectural changes. | required |
| steps-actionable | Proposed implementation approach and specific files listed to touch | Pass if the changes describe concrete code locations and discrete actions that another developer could begin executing immediately without having to guess the implementation details. | required |
| test-verifiable | Plan's test plan steps and verification assertions compared against the repro steps and expected behavior | Pass if the test plan re-runs the repro scenario or adds automated tests that prove observable resolution of the defect, showing how before and after states will be demonstrated. | required |
| risks-identified | Plan's risks, unknowns, or edge cases compared against the touched components and behavior | Pass if genuine risks, compatibility concerns, or edge cases are explicitly acknowledged rather than assuming zero risk or presenting speculative guesses as verified facts. | required |
| conventions-observed | Draft plan comment compared against repo contributing conventions, thread history, and communication guidelines | Pass if the draft comment matches repository communication norms, respects previous maintainer guidance in the thread, and adheres to explicit repository policies (such as AI disclosure if mandated). | required |

## Verdict rule

Accept if and only if every required check passes. A grade of unclear on any required check counts as a fail and results in reject. Preferred checks provide qualitative feedback and do not change the verdict.
