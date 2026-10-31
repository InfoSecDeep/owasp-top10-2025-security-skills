
name: cwe-234-failure-to-handle-missing-parameter
description: Use when testing cwe-234 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-234, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-234 - Failure to Handle Missing Parameter

CWE-234: the application does not handle a request that is missing a required parameter, so it either errors, fails open, or behaves unexpectedly.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-234 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a request is missing a required parameter and the application does not handle it gracefully.

## Detection & Test

1. **Identify the required parameter.** Find the parameter the app expects (an ID, a token, a field).
2. **Omit the parameter.** Send the request without the parameter.
3. **Observe the behavior.** Note whether the app errors, logs a stack trace, or fails open (performs the action anyway).
4. **Confirm the unsafe behavior.** Show the missing parameter leads to an error, a disclosure, or a bypass.
5. **Document the parameter, the request, and the observed behavior.

## Example Findings

- A required `id` parameter omitted, so the app returns a 500 with a stack trace.
- A required `role` parameter omitted, so the app defaults to `admin` (fails open).

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).