# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

nanditaparanjape

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-2391060935

Hi team,

Here is the proposed plan to address the UnknownHashError in verify_password for Issue #72:

### Proposed Changes
1. Target: core/security.py and tests/unit/test_security.py
2. Implementation: 
   - In core/security.py, import UnknownHashError from passlib.exc and wrap pwd_context.verify(plain_password, hashed_password) in a try...except (UnknownHashError, ValueError): block that returns False.
   - In tests/unit/test_security.py, remove the @pytest.mark.xfail marker from test_verify_with_wrong_hash_format per CONTRIBUTING.md guidelines.
3. Verification: Re-run pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format to ensure it transitions cleanly to PASSED, and verify the full test suite passes with 0 failures and 0 errors.

This change is strictly bounded to exception handling in verify_password and the corresponding test marker removal.

Best,
Nandita

---

## Your branch

**Branch**

fix/72-handle-unknown-hash-error

**Evidence**

Before implementation:
```bash
$ pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format
============================= test session starts ==============================
collected 25 items / 24 deselected / 1 selected

tests/unit/test_security.py::test_verify_with_wrong_hash_format XFAIL    [100%]

======================= 1 xfailed, 24 deselected in 0.42s =======================
```

After implementation:
```bash
$ pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format
============================= test session starts ==============================
collected 25 items / 24 deselected / 1 selected

tests/unit/test_security.py::test_verify_with_wrong_hash_format PASSED   [100%]

======================= 1 passed, 24 deselected in 0.38s =======================
```

Full suite regression run:
```bash
$ pytest tests/unit/test_security.py
============================= test session starts ==============================
collected 25 items

tests/unit/test_security.py .........................                    [100%]

============================== 25 passed in 1.15s ===============================
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. 19/20 scored items  (bar: 18/20: PASS)

**Package analysis**

`pkg-14`:
- Gold label: `accept`
- Rubric decision: `reject`
- Explanation: The rubric failed `pkg-14` on `steps-actionable` because the proposed steps referenced modifying an abstract configuration layer without identifying the exact source file path or function boundary. While gold considered the high-level description sufficient for an accept, the rubric strictly enforces that action steps must specify the concrete module path to be actionable.

**Check rationale**

Check from `rubric.md`:
```markdown
### steps-actionable
The approach must provide concrete, ordered implementation steps targeting specific files and functions, rather than vague intentions or architectural summaries.
```

Why it reads that way:
The check was formulated to reject plans that state general goals like "improve error handling in the auth module" without detailing the specific calls and exception blocks to be written. During calibration, vague plans produced incomplete PRs and unexpected scope creep, so the check was hardened to require file-level and function-level targets.

**Trade-offs**

By strictly enforcing `steps-actionable` requiring explicit function and file targets, `pkg-14` was rejected despite having sound architectural intent (producing our single disagreement against gold's `accept`). This false rejection was accepted as a necessary trade-off to ensure ambiguous or unbuildable plans (such as `pkg-10`, `pkg-17`, and `pkg-18`) were reliably rejected across all test cases.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
