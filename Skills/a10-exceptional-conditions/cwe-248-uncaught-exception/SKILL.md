
name: cwe-248-uncaught-exception
description: Use when testing cwe-248 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-248, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-248 - Uncaught Exception

CWE-248: an exception is thrown but not caught, so the application crashes or leaks information.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-248 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an exception is thrown and not caught, leading to a crash or information disclosure.

## Detection & Test

1. **Trigger the exception.** Send input that causes an error (a malformed value, a missing file).
2. **Observe the crash or error.** Confirm the app returns a 500 or leaks a stack trace.
3. **Confirm the exception is uncaught.** Show the error is not handled and leaks internals.
4. **Document the input, the exception, and the disclosure.

## Example Findings

- A malformed JSON body that triggers an uncaught `JSONDecodeError` with a full traceback.
- A missing file that triggers an uncaught `FileNotFoundError` with the file path.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).