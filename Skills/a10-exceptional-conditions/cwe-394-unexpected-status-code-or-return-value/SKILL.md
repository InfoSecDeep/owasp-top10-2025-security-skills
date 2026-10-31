
name: cwe-394-unexpected-status-code-or-return-value
description: Use when testing cwe-394 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-394, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-394 - Unexpected Status Code or Return Value

CWE-394: the application receives an unexpected status code or return value (a 302, a 403, a timeout) and does not handle it, so it continues on an unsafe path.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-394 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an unexpected status code or return value (a non-200, a 302, a 403) is not handled.

## Detection & Test

1. **Trigger the unexpected value.** Send a request that causes the unexpected status or return (a 302, a 403, a timeout).
2. **Confirm the value is received.** Show the app gets the unexpected value.
3. **Confirm no handling.** Show the app does not handle the value and continues.
4. **Confirm the unsafe continuation.** Show the app performs an action it should not after the unexpected value.
5. **Document the value, the request, and the outcome.

## Example Findings

- A 302 redirect from a payment gateway that is not checked, so the app proceeds with a null payment confirmation.
- A 403 from an upstream service that is not checked, so the app allows the action anyway.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).