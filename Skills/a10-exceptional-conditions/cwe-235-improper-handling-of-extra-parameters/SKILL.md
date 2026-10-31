
name: cwe-235-improper-handling-of-extra-parameters
description: Use when testing cwe-235 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-235, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-235 - Improper Handling of Extra Parameters

CWE-235: the application does not handle extra, unexpected parameters, so they are processed or cause unsafe behavior.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-235 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the application receives extra parameters it does not expect and processes them.

## Detection & Test

1. **Add an extra parameter.** Include a parameter the app does not document (e.g., `role=admin`, `isAdmin=true`).
2. **Submit the request.** Send the request with the extra parameter.
3. **Observe the behavior.** Confirm the extra parameter is processed and changes the outcome.
4. **Confirm the unsafe behavior.** Show the extra parameter escalates privileges or changes state.
5. **Document the parameter, the value, and the outcome.

## Example Findings

- A login form that accepts an extra `role=admin` parameter and sets the role.
- A payment form that accepts an extra `discount=100%` parameter and applies it.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).