# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

nanditaparanjape

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5902128940

Hi, I see others are investigating this as well. I'm reproducing the UnknownHashError in core/security.py locally on macOS with Python 3.11 to verify the failure mode against tests/unit/test_security.py. I'll share my reproduction notes shortly.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5902213212

### Reproduction Report

**Environment:**
- OS: macOS (Darwin arm64)
- Python: 3.13.1
- pytest: 9.1.1
- Repository: codepath/pathreview-ai301-fa26-s1 (main)

**Steps to Reproduce:**

1. Set up virtual environment and install dependencies:
`python3 -m venv .venv && source .venv/bin/activate && pip install pytest passlib`

2. Run the security unit tests with summary flags:
`pytest tests/unit/test_security.py -rxX -v`

**Observed Behavior:**

The test suite completes with 24 passed and 1 xfailed test:
`XFAIL tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False`

When verify_password receives an invalid hash string, passlib raises an unhandled UnknownHashError rather than returning False.

**Expected Behavior:**
verify_password should handle malformed or unsupported hash strings safely and return False.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

- Run 1 (full 20-package run): 17/20 scored items.
- Run 2 (targeted --only pkg-06,pkg-09,pkg-10,pkg-12): 4/4 scored items.
- Run 3 (full 20-package run): 18/20 scored items (below the bar: category floor unmet: no match in disclosure).
- Run 4 (targeted --only pkg-01,pkg-16,pkg-20): 3/3 scored items.
- Run 5 (confirming full 20-package run): 20/20 scored items.

**Package analysis**

Package: pkg-20
Gold label: reject
Initial rubric verdict: accept
Final rubric verdict: reject

In pkg-20 (source ghostty-org/ghostty#13604), the repository facts explicitly state strict contribution rules: "All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance... AI-assisted issues and comments must be reviewed and edited by a human before submission." The candidate claim comment and reproduction report included zero disclosure text. 

My rubric initially graded pkg-20 as accept because the check condition in conventions-observed framed AI disclosure as an optional illustration ("like stating whether an AI tool helped write it when the repository asks for disclosure"). Because Sonnet did not treat this as an absolute failure condition, the package slipped through. Once conventions-observed was revised to explicitly demand disclosure whenever repository policy mandates it, the rubric correctly failed the package and matched the gold label.

**Check rationale**

Check quoted from tools/repro-check/rubric.md:

| conventions-observed | The claim and repro comments checked against repo facts and contribution/AI policies | Pass if the comments follow all repository rules. If the repository policy mandates AI-use disclosure on comments/contributions, the comments MUST contain explicit AI disclosure stating the tool or assistance used; fail if disclosure is omitted. | required |

Why it reads this way:
The initial draft of this check read: "Pass if the comment follows repo rules, like stating whether an AI tool helped write it when the repository asks for disclosure." That phrasing was too soft; Sonnet evaluated missing disclosure as a minor stylistic choice rather than a mandatory compliance failure. Revising the condition to require that comments "MUST contain explicit AI disclosure stating the tool or assistance used; fail if disclosure is omitted" turned repo compliance into a clear binary boundary, which was necessary to pass the single-package disclosure category floor on pkg-20.

**Trade-offs**

Tightening conventions-observed ensures strict compliance on repositories with explicit AI policies like Ghostty (pkg-20), but it introduces the risk of rejecting human-authored contributions on repositories whose contributing guidelines are ambiguous or recommend disclosure without strictly enforcing it. Conversely, loosening claim-specific to accept natural issue exploration (such as in pkg-09 and pkg-10) allowed valid exploratory comments to pass, but required running canary package pkg-06 with --only to confirm that low-effort comments lacking genuine technical focus were still reliably rejected.

---

Related paths: eval-run.txt in this directory; your skill's files in tools/repro-check/.
