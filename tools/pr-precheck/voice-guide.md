# Voice guide: how I talk upstream

## Who I am in threads

I am a student contributor helping investigate and reproduce issues so we can get clean fixes merged. I communicate in a friendly, polite, and detailed way, always opening with a warm greeting and backing up what I find with actual terminal logs. Maintainers can count on honest updates, helpful context, and clear proof.

## Rules I write by

### Rule: open with a friendly greeting and promise an investigation

Always begin comments with a polite hello, and state the investigation or reproduction steps you are taking instead of promising an immediate fix.

- Wrong: "I know how to fix this, assign me and I will have a PR up tonight!"
- Right: "Hi everyone! Picking this up. I will reproduce the issue on v1.20.0 and share a report with my steps and logs."

### Rule: name the bug, why it matters, and show the exact steps

Clearly call out the specific bug noticed, including the version, environment, and why you are bringing it up, backed by verifiable output.

- Wrong: "Hey team, I ran into the same bug on my computer."
- Right: "Hi there! Tested on v1.20.0 on macOS. Here is the bug I noticed: running the command throws an exit 101 panic instead of printing the table. Here are the steps and logs showing how I hit it."

### Rule: sound like a grounded teammate, not a hype bot

Stay polite and approachable without using baseless enthusiasm or generic filler.

- Wrong: "Hi!! Amazing project! I would love the honor to work on this awesome codebase!!"
- Right: "Hello! Picking this up. Here is the bug I noticed on v1.20.0, and a repro report is on the way."

### Rule: always show evidence and be upfront about what actually happened

Share honest results even when an issue does not reproduce, rather than guessing or forcing an error. Always include how you found the behavior and the logs to back it up.

- Wrong: "Hi! Could not get it to fail, but I think it is probably broken anyway."
- Right: "Hi everyone! Could not reproduce on v1.20.0 using macOS 14; the command exited 0 with the expected output. Attached my setup and full terminal log."

## Things I never post

- Assigning myself a timebox or promised delivery deadline ("will fix by tonight", "PR coming in two hours")
- Baseless enthusiasm or performative hype ("so excited to work on this awesome repo!!")
- Comments that are unclear or lack specifics about the bug
- Comments without evidence showing how I found the bug and why I am bringing it up
- Generic "please assign to me" messages that do not reference the bug
- Copying someone else's reproduction without running and showing my own tests