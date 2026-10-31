
name: cwe-280-improper-handling-of-insufficient-permissions
description: Use when testing cwe-280 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-280, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-280 - Improper Handling of Insufficient Permissions

CWE-280: the application does not handle a permission failure, so it either continues with unsafe access or fails open.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-280 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a permission check fails and the application does not handle it (continues, fails open).

## Detection & Test

1. **Set the permission to deny.** Restrict the permission (chmod 000, remove a role).
2. **Attempt the action.** Send the request that requires the permission.
3. **Observe the behavior.** Confirm the app does not detect the permission failure and continues.
4. **Confirm the unsafe behavior.** Show the app performs the action despite the permission failure.
5. **Document the permission, the action, and proof.

## Example Findings

- A file permission set to 000, but the app still reads it because it was opened before the chmod.
- A user role removed, but the app still allows the action because the session token was not re-validated.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).