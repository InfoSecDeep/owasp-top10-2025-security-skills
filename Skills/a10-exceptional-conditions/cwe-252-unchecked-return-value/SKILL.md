
name: cwe-252-unchecked-return-value
description: Use when testing cwe-252 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-252, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-252 - Unchecked Return Value

CWE-252: a function or API call returns a value (success, error, a pointer) that is not checked, so the app continues on a failed path.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-252 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a return value (success code, nullable, error flag) is not checked and the app continues.

## Detection & Test

1. **Find the unchecked return.** Identify where the app calls a function or API and ignores the return value.
2. **Force the failure.** Trigger the condition that makes the return value fail (a DB error, a file not found).
3. **Confirm the app continues.** Show the app proceeds without handling the failure.
4. **Document the call, the failure, and the unsafe continuation.

## Example Findings

- A DB query that returns null on failure, but the app uses the null result without a check.
- A file read that fails, but the app continues with a null buffer and reads unrelated data.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).