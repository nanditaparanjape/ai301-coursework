# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

- **Where it lives:** In eval packages, look under the `## Repro evidence` section (error trace, exit code, observed behavior) and compare it against the `## Diagnosis` or `Root cause` section in the candidate plan. In live mode, look at the posted reproduction comment on the GitHub issue thread and compare it against the Diagnosis section in `plan.md`.
- **What good looks like:** The diagnosis cites the exact failure mechanism, exception type, and triggering inputs demonstrated in the repro evidence. It identifies the root cause rather than treating the symptom, without contradicting the observed error traces.

## Scope

- **Where it lives:** Look under `## Scope`, `In-scope`, and `Out-of-scope` (or `Not in scope`) sections of the plan, as well as the list of proposed files to modify.
- **What good looks like:** The scope explicitly specifies which modules or files will change and explicitly states what will not be touched. The modifications are bounded strictly to resolving the diagnosed root cause without adding unrequested features, refactoring unrelated files, or altering broad system architecture.

## Executability

- **Where it lives:** Look under `## Approach`, `## Implementation steps`, or `## Proposed changes` in `plan.md`.
- **What good looks like:** The steps name specific files, functions, conditional logic, or configuration values to adjust. The instructions are concrete enough that another developer could open the codebase and begin editing immediately without guessing the author's intent.

## Test plan

- **Where it lives:** Look under `## Test plan` or `## Verification` in the plan document.
- **What good looks like:** The test plan re-runs the specific reproduction commands from the repro evidence or specifies new automated unit tests, and states the exact observable output (exit code, output string, or assertion result) expected before and after the fix.

## Honesty

- **Where it lives:** Look under `## Risks and unknowns`, `## Assumptions`, or `## Deviations` in `plan.md`.
- **What good looks like:** Real risks, edge cases, backwards-compatibility implications, or unverified assumptions are acknowledged explicitly. The plan avoids claiming zero risk when touching shared code, and does not disguise open questions as certainties.

## Comms

- **Where it lives:** Look at the candidate plan comment (`comment.md` or package comment section) and read it against the `## Thread highlights` or maintainer instructions in the issue, as well as the `repo-facts` block or `CONTRIBUTING.md`.
- **What good looks like:** The comment addresses previous maintainer notes or reviewer concerns raised in the thread, respects repository tone and contribution guidelines, and includes any mandatory disclosures (such as AI usage policies) required by the repository.
