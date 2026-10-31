
name: cwe-397-throws-for-generic-exception
description: Use when testing cwe-397 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-397, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-397 - Throws for Generic Exception

CWE-397: the application throws a generic exception (a base type) instead of a specific one, so the caller cannot handle the specific error.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-397 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a generic exception is thrown instead of a specific one, so the caller cannot handle the error precisely.

## Detection & Test

1. **Find the generic throw.** Identify where the app throws a generic exception (a `Exception`, a `Throwable`).
2. **Trigger the error.** Send input that causes the specific error.
3. **Confirm the generic throw.** Show the app throws a generic exception instead of a specific one.
4. **Confirm the caller cannot handle it.** Show the caller catches the generic exception and ignores the specific state.
5. **Document the throw, the generic type, and the caller's handling.

## Example Findings

- A `throw new Exception("error")` that hides the specific error (a missing file, a DB failure).
- A generic exception that the caller catches and retries, masking the real failure.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).