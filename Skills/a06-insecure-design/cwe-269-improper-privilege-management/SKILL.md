
name: cwe-269-improper-privilege-management
description: Use when a web design flaw matching cwe-269 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-269, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-269 - Improper Privilege Management

CWE-269: the assignment, verification, or revocation of privileges is handled incorrectly, letting an actor hold a privilege they should not (or keep one they lost).

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-269 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When privileges are assigned, verified, or revoked incorrectly (e.g. stale privileges, missing re-authentication).

## Detection & Test

1. **Map privilege lifecycle.** Identify how privileges are assigned, checked, and revoked.
2. **Test stale privileges.** Log in as user A, log in as user B without logging out, and check whether A's privilege persists.
3. **Verify re-assignment.** Confirm a privilege is re-checked after a state change (elevated action, session renewal).
4. **Escalate.** Use a leftover privilege to perform a privileged action.
5. **Document the lifecycle gap, payload, and impact.

## Example Findings

- Switching users in the same session keeps the previous user's elevated privilege.
- An elevated action is not re-verified after a privilege change.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).