
name: cwe-390-detection-of-error-condition-without-action
description: Use when testing cwe-390 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-390, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-390 - Detection of Error Condition without Action

CWE-390: an error is detected (logged, flagged) but not acted upon, so the app continues on an unsafe path.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-390 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an error is detected (a log entry, a flag) but the application does not act on it.

## Detection & Test

1. **Trigger the error.** Send input that causes the error to be detected.
2. **Confirm the detection.** Show the error is logged or flagged.
3. **Confirm no action is taken.** Show the app continues without handling the error.
4. **Confirm the unsafe continuation.** Show the app performs an action it should not after the error.
5. **Document the error, the detection, and the unsafe continuation.

## Example Findings

- A failed DB authentication that is logged but the app continues with a null connection.
- A failed file write that is logged but the app continues with a partial file.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).