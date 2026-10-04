# Contribution: Fix Unhandled UnknownHashError in Password Verification (#72)

Path: `beat-2-contribution/contribution-story.md`

**Contribution Number:** 1
**Student:** Nandita Paranjape
**GitHub Username:** nanditaparanjape
**Issue:** https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72
**Pull Request:** https://github.com/codepath/pathreview-ai301-fa26-s1/pull/84

---

## Toolkit

**Unit 5: issue-scout evaluation and selection**
Built and calibrated the issue-scout rubric across synthetic test suites to exceed the 18/20 agreement threshold. Ran the scout on live upstream repositories to filter issues matching Python security and authentication scope. Updated rubric boundary checks to catch unhandled third-party library exceptions.

**Unit 6: reproduction protocol and environment isolation**
Executed pytest reproduction suites in an isolated Python 3.12 virtual environment. Uncovered passlib `UnknownHashError` during unhandled hash verification failures. Maintained structured reproduction notes to ensure deterministic test cases.

**Unit 7: implementation and ruff gate validation**
Implemented defensive exception handling around CryptContext verification and updated test markers. The local ruff linter flagged docstring placement and import grouping on initial commit. Restructured import hierarchies to satisfy ruff formatting gates cleanly before pushing upstream.

**Unit 8: pull request workflow and upstream tracking**
Created PR #84 targeting upstream main with structured reproduction and verification summaries. Monitored automated CI workflows to confirm green checkmarks across all test runs. Documented complete contribution trace and responses in course portfolio.

---

## Why I Chose This Issue

During the issue scouting phase across `codepath/pathreview-ai301-fa26-s1`, issue #72 immediately stood out because it directly touched backend authentication robustness in `core/security.py`. The issue-scout evaluated the issue against our selection rubric, scoring it as an accept due to clear scope, deterministic test coverage already sketched in `tests/unit/test_security.py`, and low ambiguity. The bug involved passlib's `UnknownHashError` escaping unhandled during authentication attempts with corrupted, truncated, or incompatible hash strings, bubbling up as an unexpected HTTP 500 instead of returning `False`.

This issue matched my backend Python experience and gave me an opportunity to practice defensive programming in password hashing subsystems. The scout proved reliable on focused unit-level bugs, though it initially flagged the presence of `xfail` test decorators as potential repository debt. I manually verified `CONTRIBUTING.md` guidelines, which confirmed that removing `xfail` upon resolving the bug was the expected workflow.

Claim comment link: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-3365851410

**Toolkit**

- Tool: issue-scout (rubric scoring and live GitHub issue filtering)
- What it produced: Ranked issue #72 with high feasibility and clear unit test hooks.
- Difficulties: Scout initially flagged existing `xfail` test annotations as repository risk.
- What changed: Verified project contribution standards to confirm removing `xfail` is the intended pattern for targeted bugs.

---

## Understanding the Issue

**Problem Description**

In `core/security.py`, `verify_password(plain_password: str, hashed_password: str) -> bool` uses Passlib's `CryptContext.verify()`. When passed a malformed hash, an empty string, or an unknown algorithm scheme, Passlib raises `passlib.exc.UnknownHashError` or `ValueError`. Because `verify_password` did not catch these specific exceptions, the unhandled error escalated to caller handlers and crashed authentication routes with a 500 error instead of cleanly denying authentication.

**Expected Behavior**

`verify_password` should return `False` whenever password verification cannot be completed due to invalid, unrecognized, or corrupted hash formats.

**Current Behavior**

Passing an unrecognized or corrupted hash string raised an unhandled `passlib.exc.UnknownHashError`, crashing the execution thread.

**Affected Components**

- `core/security.py`: `verify_password` function and exception imports.
- `tests/unit/test_security.py`: `test_verify_with_wrong_hash_format` test case.

**Toolkit**

- Tool: pytest and traceback inspection
- What it produced: Pinpointed `UnknownHashError` bubbling directly from `pwd_context.verify`.
- Difficulties: Determining whether to catch generic `Exception` or narrow passlib exceptions.
- What changed: Narrowed exception scope to `(UnknownHashError, ValueError)` to avoid masking broader system errors.

---

## Reproduction Process

**Environment Setup**

- macOS (Darwin arm64)
- Python 3.12 within virtual environment (`.venv`)
- Project dependencies installed via `pip install -e ".[dev]"`
- Test suite driven by `pytest` and linter driven by `ruff`

**Steps to Reproduce**

1. Activate virtual environment: `source .venv/bin/activate`
2. Run targeted test: `.venv/bin/pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -rxX`
3. Observe test marked `XFAIL` due to expected `UnknownHashError` failure when passing `"not-a-valid-hash"`.

**Reproduction Evidence**

- **Commit showing reproduction:** https://github.com/nanditaparanjape/pathreview-ai301-fa26-s1/commit/aac06feb7b92ff2420959fc961f77d3326f59c11
- **Screenshots/logs:** `tests/unit/test_security.py:48: UnknownHashError: hash could not be identified`
- **My findings:** The existing test file contained an explicit `xfail` marker documenting the expected bug behavior. Running the test confirmed that `pwd_context.verify` directly raised `passlib.exc.UnknownHashError`.

**Toolkit**

- Tool: pytest CLI with `-rxX` verbose flags
- What it produced: Full stack trace confirming unhandled exception path in Passlib.
- Difficulties: None met during reproduction.
- What changed: Nothing.

---

## Solution Approach

**Analysis**

The bug resides inside `core/security.py` where `pwd_context.verify(plain_password, hashed_password)` executes without error boundaries. Passlib intentionally raises `UnknownHashError` when hash identifiers do not match configured schemes (e.g., bcrypt). It can also throw `ValueError` on corrupted payload slices.

**Proposed Solution**

Wrap `pwd_context.verify(plain_password, hashed_password)` in a `try...except (UnknownHashError, ValueError):` block and return `False`. Deliberately leave token creation, expiration handling, and hashing generation untouched.

**Implementation Plan**

1. Import `UnknownHashError` from `passlib.exc` in `core/security.py`.
2. Wrap `pwd_context.verify` in `verify_password` with targeted exception handling returning `False`.
3. Remove `@pytest.mark.xfail` from `test_verify_with_wrong_hash_format` in `tests/unit/test_security.py`.
4. Run full test suite and `ruff` lint validation before opening PR.

**Toolkit**

- Tool: Python static analysis and editor environment
- What it produced: Clean patch in `core/security.py` returning `False` on invalid hash strings.
- Difficulties: Initial import placement violated ruff sorting rules.
- What changed: Grouped `from passlib.exc import UnknownHashError` with CryptContext imports below module docstring.

---

## Testing Strategy

Observed checks proving the fix:
1. Re-ran `pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format`: changed from `XFAIL` to `PASSED`.
2. Executed full unit test suite: `.venv/bin/pytest tests/unit/test_security.py` -> 25 passed, 0 failed, 0 xfailed.
3. Executed code quality checks: `.venv/bin/ruff check core/security.py tests/unit/test_security.py` -> All checks passed.

**Toolkit**

- Tool: pytest and ruff CLI
- What it produced: 25/25 passing tests and 0 lint violations.
- Difficulties: Lint check failed on PR #84 initially due to import order.
- What changed: Reordered imports and docstring, committed fix, and confirmed CI check turned green.

---

## Implementation Notes

**2026-10-02**

Reproduced issue #72 locally using pytest. Confirmed `UnknownHashError` on invalid hash format. Formulated implementation plan to catch `UnknownHashError` and `ValueError`.

**2026-10-03**

Patched `core/security.py` and un-xfailed `test_verify_with_wrong_hash_format`. Committed changes and created personal fork on GitHub. Pushed branch `fix/72-handle-unknown-hash-error` and opened Pull Request #84. Caught ruff import order failure in GitHub Actions, applied docstring and import fixes locally, pushed update, and verified green CI status. Posted implementation plan comment on Issue #72.

**Toolkit**

- Tool: Git and GitHub Pull Request workflow
- What it produced: PR #84 submitted with green CI status and linked issue comment.
- Difficulties: Initial push targeted upstream instead of personal fork, and PR had a ruff lint error.
- What changed: Configured correct remote fork URL and reordered imports to pass all checks.

---

## Pull Request

**PR Link:** https://github.com/codepath/pathreview-ai301-fa26-s1/pull/84

**PR Description:**
Resolves #72. Wrapped `pwd_context.verify(plain_password, hashed_password)` in `core/security.py` within a `try...except (UnknownHashError, ValueError):` block returning `False`. Removed `@pytest.mark.xfail` marker from `test_verify_with_wrong_hash_format` in `tests/unit/test_security.py`. Verified 25/25 unit tests pass and all ruff checks pass.

**Maintainer Feedback:**

- 2026-10-03: None yet; automated GitHub Actions CI completed with green passing checks.
- 2026-10-03: Awaiting maintainer review.

**Status:** Awaiting review

**Toolkit**

- Tool: GitHub Actions and PR interface
- What it produced: Active pull request with passing build checks.
- Difficulties: None after pushing the lint formatting fix.
- What changed: Nothing.

---

## Learnings and Reflections

**Technical Skills Gained**

Deepened understanding of Passlib exception hierarchies, defensive programming in authentication utility layers, and GitHub fork-and-pull-request workflows. Learned how strict CI linting gates (`ruff`) enforce docstring placement and import grouping.

**Challenges Overcome**

Resolving git remote configurations when working across starter and fork repositories, as well as fixing fast-failing CI lint errors on upstream PRs by running and inspecting local linter outputs.

**What I'd Do Differently Next Time**

Always run the full pre-commit and linter suite (`ruff check` and `ruff format`) before pushing the initial branch commit, preventing avoidable CI failures on newly opened pull requests.

---

## Resources Used

- Passlib CryptContext Exception Documentation: https://passlib.readthedocs.io/en/stable/lib/passlib.exc.html
- CodePath AI301 Contribution Guidelines: `CONTRIBUTING.md` in repository root
- GitHub Actions CI workflow logs for PR #84: https://github.com/codepath/pathreview-ai301-fa26-s1/pull/84
