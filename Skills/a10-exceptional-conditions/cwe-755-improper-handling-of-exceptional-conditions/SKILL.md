
name: cwe-755-improper-handling-of-exceptional-conditions
description: Use when testing cwe-755 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-755, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-755 - Improper Handling of Exceptional Conditions

CWE-755: the application handles an exceptional condition in a way that is unsafe (a fallback to a permissive default, a retry that hides the error).

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-755 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an exceptional condition is handled in an unsafe way (a permissive fallback, a hidden retry).

## Detection & Test

1. **Find the handling.** Identify where the app handles an exceptional condition (a catch block, a fallback).
2. **Identify the unsafe handling.** Note the permissive default, the hidden retry, or the swallowed error.
3. **Trigger the condition.** Send input that causes the exceptional condition.
4. **Confirm the unsafe handling.** Show the app uses the permissive default or hides the error.
5. **Document the condition, the handling, and the unsafe outcome.

## Example Findings

- A catch block that defaults the user to `admin` on a DB failure.
- A retry loop that hides a persistent authentication failure.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).