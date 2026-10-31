
name: cwe-274-improper-handling-of-insufficient-privileges
description: Use when testing cwe-274 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-274, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-274 - Improper Handling of Insufficient Privileges

CWE-274: the application does not handle a condition of insufficient privileges, so it either continues with elevated access or fails open.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-274 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the application does not handle insufficient privileges (a dropped root, a read-only FS) and fails open.

## Detection & Test

1. **Drop the privileges.** Run the process with lower privileges (drop root, use a non-writable dir).
2. **Observe the behavior.** Confirm the app does not detect the failure and continues with elevated access.
3. **Confirm the unsafe behavior.** Show the app performs an action it should not with the dropped privileges.
4. **Document the privilege drop, the action, and proof.

## Example Findings

- A process that drops root but still reads `/etc/shadow` because the file descriptor is inherited.
- A service that fails to write to a log but continues processing sensitive data.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).