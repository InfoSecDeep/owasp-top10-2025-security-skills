
name: cwe-369-divide-by-zero
description: Use when testing cwe-369 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-369, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-369 - Divide by Zero

CWE-369: the application divides by a value that can be zero, causing a crash or an unsafe result.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-369 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a division by a user-controllable value can be zero, causing a crash or an unsafe result.

## Detection & Test

1. **Find the division.** Identify where the app divides by a value (a count, a quantity, a rate).
2. **Set the divisor to zero.** Send a request that makes the divisor zero.
3. **Observe the crash or result.** Confirm the app crashes or returns an unsafe value.
4. **Confirm the impact.** Show the division by zero leads to a crash, a disclosure, or a state change.
5. **Document the divisor, the request, and the outcome.

## Example Findings

- A `quantity=0` parameter that divides a price, causing a crash or an infinite price.
- A `rate=0` that divides a calculation, causing a division-by-zero error with a stack trace.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).