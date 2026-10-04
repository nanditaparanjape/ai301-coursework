# Evidence guide: where proof lives in a reproduction package

## Environment

### Where it lives
Look at the environment block at the top of the repro report, and cross-check it against the issue's stated target and repo facts.

### What good looks like
The report explicitly lists the tool version, operating system, and build or commit hash tested. It matches the issue's target or runs on the current supported release/main branch. If the repo asks to verify against the latest version or main, testing an obsolete legacy version without explanation fails.

## Steps

### Where it lives
Look at the reproduction steps section inside the repro report.

### What good looks like
The steps clearly describe the execution path. Supplying explicit shell commands or referencing the issue's script verbatim (e.g. running an issue script or reproduction test case) passes. Steps fail only if they leave the reader unable to run the reproduction without guessing missing arguments or files.

## Behavior shown

### Where it lives
Look at the terminal output, error logs, or failure excerpts, and check them against the issue's original error description.

### What good looks like
The terminal output demonstrates the bug reported in the issue, showing matching failure modes, exit codes, or parse errors rather than unrelated user mistakes.

## Honesty

### Where it lives
Look at the expected versus actual section and compare it with the final reproduction conclusion.

### What good looks like
The report sticks to what the logs prove. An evidenced run stating the bug could not be reproduced passes; claiming the bug was reproduced when the output shows an unrelated error fails.

## Comms

### Where it lives
Look at the candidate claim comment, the repro comment, and the repo facts (specifically CONTRIBUTING.md, bug report templates, and AI policies).

### What good looks like
The claim references the specific issue or failure mode without making ungrounded fix promises or setting arbitrary deadlines. If the repository facts state that all AI usage must be disclosed, the draft comment or report must include that disclosure; omitting disclosure when the repo asks for it is a failure.