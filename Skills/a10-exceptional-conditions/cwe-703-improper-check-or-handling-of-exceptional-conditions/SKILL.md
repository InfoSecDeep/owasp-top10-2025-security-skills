
name: cwe-703-improper-check-or-handling-of-exceptional-conditions
description: Use when testing cwe-703 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-703, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-703 - Improper Check or Handling of Exceptional Conditions

CWE-703: the application checks or handles an exceptional condition in a way that misses the actual error (a wrong comparison, a missing branch).

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-703 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an exceptional condition is checked or handled incorrectly (a wrong comparison, a missing branch).

## Detection & Test

1. **Find the check.** Identify where the app checks for an exceptional condition (a null, a timeout, a status).
2. **Identify the flaw.** Note the incorrect comparison, the missing branch, or the wrong value.
3. **Trigger the condition.** Send input that causes the exceptional condition.
4. **Confirm the flaw is bypassed.** Show the check does not detect the condition and the app continues.
5. **Document the check, the flaw, and the bypass.

## Example Findings

- A null check that compares to the wrong field, so the null is not caught.
- A status check that uses `== 200` but the API returns `201`, so the success is not detected.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).