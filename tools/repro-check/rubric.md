# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `claim-specific` | The claim comment draft compared against the issue title, thread, and description | Pass if the claim discusses the specific issue, scenario, or behavior being investigated and communicates intent to work on or reproduce it. Natural phrasing and referencing thread details count as a pass. Fail only if it makes unsubstantiated fix guarantees, promises delivery deadlines, or is generic boilerplate/spam ("assign to me"). In a repro-only report, mark not applicable (pass). | required |
| `env-recorded` | The environment section at the top of the reproduction report compared against repo facts and the issue | Pass if it lists the tool version, operating system, and build or commit hash tested, and tests a target version relevant to the issue. Fail if it tests an outdated or irrelevant version (for example, testing an ancient release when the repo or issue asks for current latest/main) without explaining why. | required |
| `steps-followable` | The reproduction steps section in the report | Pass if the steps provide clear commands or explicitly reference the issue's code/scripts so another person can run them. Inline scripts, reproduction commands, or running the issue's test script verbatim all pass. Fail only if critical setup steps or parameters are completely missing. | required |
| `behavior-matches` | The terminal log or error output compared against the original issue report | Pass if the output demonstrates the bug described in the issue, or clearly documents what occurred when attempting to trigger it. Fail if the output is just an unrelated typo or CLI configuration failure. | required |
| `honesty` | What actually happened compared to what was supposed to happen, plus the final conclusion | Pass if the conclusion accurately reflects the output. A faithful run concluding "could not reproduce" passes; claiming a bug happened when the output shows an unrelated error fails. | required |
| `conventions-observed` | The claim and repro comments checked against repo facts and contribution/AI policies | Pass if the comments follow all repository rules. If the repository policy mandates AI-use disclosure on comments/contributions, the comments MUST contain explicit AI disclosure stating the tool or assistance used; fail if disclosure is omitted. | required |

## Verdict rule

Accept if every required check passes. Reject if any required check fails or lacks enough detail to verify. A check that does not apply counts as a pass.