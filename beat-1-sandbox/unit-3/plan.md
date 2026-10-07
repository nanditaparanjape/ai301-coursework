# Plan: Issue #72 - Gracefully handle UnknownHashError in verify_password

## Diagnosis

The function verify_password(plain_password: str, hashed_password: str) -> bool in core/security.py relies on Passlibs pwd_context.verify(plain_password, hashed_password). When passed a malformed, corrupted, or unrecognized hash format, Passlib raises passlib.exc.UnknownHashError or ValueError rather than returning False.

The failing test in tests/unit/test_security.py demonstrates this behavior:
passlib.exc.UnknownHashError: hash could not be identified
tests/unit/test_security.py:222: in test_verify_with_wrong_hash_format
    assert verify_password("secret", "not-a-valid-hash") is False
core/security.py:28: in verify_password
    return pwd_context.verify(plain_password, hashed_password)

Callers expecting a boolean credential check receive an unhandled 500 error instead of a standard authentication rejection (False).

## Scope

### In-scope
- Modify core/security.py to import UnknownHashError from passlib.exc.
- Wrap pwd_context.verify(plain_password, hashed_password) inside verify_password in a try...except block catching (UnknownHashError, ValueError).
- Return False when those exceptions are encountered.
- In tests/unit/test_security.py, remove the @pytest.mark.xfail marker from test_verify_with_wrong_hash_format per CONTRIBUTING.md.

### Out-of-scope
- Altering password hashing schemes, algorithms, or salt rounds in CryptContext.
- Changing authentication token generation, OAuth2 flows, or database user models.
- Refactoring other helper utilities in core/security.py.

## Files to touch

- core/security.py: Add exception handling to verify_password.
- tests/unit/test_security.py: Remove the @pytest.mark.xfail marker from test_verify_with_wrong_hash_format so the passing test is evaluated as PASSED.

## Approach

1. In core/security.py, import UnknownHashError from passlib.exc.
2. In verify_password(plain_password: str, hashed_password: str) -> bool:
   try:
       return pwd_context.verify(plain_password, hashed_password)
   except (UnknownHashError, ValueError):
       return False
3. In tests/unit/test_security.py, remove the @pytest.mark.xfail marker decorator directly preceding test_verify_with_wrong_hash_format (line 222).
4. Run the test suite using pytest tests/unit/test_security.py to confirm test_verify_with_wrong_hash_format passes cleanly as PASSED rather than XPASS.

## Test plan

- Reproduction re-run: Execute pytest -v tests/unit/test_security.py -k test_verify_with_wrong_hash_format.
  - Before: XFAIL (or FAILED if executed without strict xfail handling) due to passlib.exc.UnknownHashError.
  - After: PASSED tests/unit/test_security.py::test_verify_with_wrong_hash_format.
- Full suite regression check: Run pytest tests/unit/test_security.py to confirm all security unit tests pass with 0 failures, 0 xfails, and 0 errors.

## Risks and unknowns

- Overly broad exception catching: Catching generic Exception would risk masking unexpected internal errors; bounding the catch strictly to (UnknownHashError, ValueError) eliminates this risk while covering Passlibs malformed hash exceptions.
- Timing attack considerations: Returning early on a malformed hash could introduce a negligible timing difference compared to full hash verification, but malformed hashes are not valid credential candidates.

## Deviations

None.
