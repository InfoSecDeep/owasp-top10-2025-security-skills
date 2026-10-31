
name: cwe-396-catch-for-generic-exception
description: Use when testing cwe-396 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-396, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-396 - Catch for Generic Exception

CWE-396: the application catches a generic exception (a catch-all) and handles it imprecisely, so specific errors (a crash, a security event) are missed.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-396 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a generic exception (a catch-all) is caught and handled in a way that masks specific errors.

## Detection & Test

1. **Find the catch-all.** Identify where the app catches a generic exception (a `catch (Exception)`, a `try/catch` with no type).
2. **Trigger a specific error.** Send input that causes a specific error (a crash, a security event).
3. **Confirm the catch-all handles it.** Show the specific error is caught by the generic handler and not treated specially.
4. **Confirm the masking.** Show the catch-all masks the specific error and the app continues.
5. **Document the catch-all, the specific error, and the masking.

## Example Findings

- A `catch (Exception e) { log(e); }` that masks a security-relevant exception.
- A generic handler that returns a generic 500, hiding the specific error from the analyst.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).