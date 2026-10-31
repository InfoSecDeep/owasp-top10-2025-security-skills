
name: cwe-391-unchecked-error-condition
description: Use when testing cwe-391 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-391, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-391 - Unchecked Error Condition

CWE-391: an error condition is not checked, so the application continues on an unsafe path.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-391 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an error condition (a failed call, a null result) is not checked and the app continues.

## Detection & Test

1. **Find the unchecked error.** Identify where the app checks a condition but ignores the error state.
2. **Trigger the error.** Send input that causes the error condition.
3. **Confirm the error is not checked.** Show the app continues without handling the error.
4. **Confirm the unsafe behavior.** Show the app performs an action it should not after the error.
5. **Document the error, the unchecked state, and the outcome.

## Example Findings

- A failed API call that is not checked, so the app uses a default value that allows the action.
- A failed decryption that is not checked, so the app proceeds with a null plaintext.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).