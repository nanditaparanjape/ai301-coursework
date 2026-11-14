# Playbook: Nandita Paranjape

## Response rules

- Answer the reviewer's technical question or requested change in the first sentence before explaining context.
- Never defend existing code or explain why a bug happened; acknowledge the feedback and point directly to the updated commit or test.
- Keep replies under four sentences unless walking through a failing test case.

## Staleness thresholds

- Wait 7 quiet days before sending a first-review nudge. `codepath/pathreview-ai301-fa26-s1` has no `CONTRIBUTING.md` and zero merged external PRs (`gh pr list --state merged` returned `[]`), so a one-week window gives course maintainers reasonable turnaround time.
- Wait 5 quiet days after pushing requested changes before nudging on a stalled review.

## Nudge etiquette

- Summarize what the PR changes in one sentence (e.g., catching `UnknownHashError` and `ValueError` in `verify_password`) so a reader needs zero prior context.
- Ask for one specific action (a review on the current passing CI build) and tag only the assigned reviewer if one exists, or leave untagged if unassigned.
- Never apologize for pinging, use exclamation marks, or send more than one nudge per PR.

## Walk-away criteria

- Close the PR if a maintainer explicitly rejects the approach, if the underlying issue is closed via another commit, or if the PR remains quiet for 30 days after the single nudge (or 45 total quiet days in a course sandbox repo with no merges).
- Leave a brief closing comment stating that the PR is being closed due to inactivity/sandbox completion so maintainers do not spend time reviewing stale branches.
