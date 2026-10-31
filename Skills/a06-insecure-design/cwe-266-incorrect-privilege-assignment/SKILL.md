
name: cwe-266-incorrect-privilege-assignment
description: Use when a web design flaw matching cwe-266 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-266, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-266 - Incorrect Privilege Assignment

CWE-266: a privilege or role is assigned to a user based on user-controlled or untrusted input (e.g. admin roles granted client-side), without server-side verification.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-266 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a privilege, role, or permission is set from client-side or user-controllable state.

## Detection & Test

1. **Map the privilege assignment.** Identify where roles or privileges are granted (a role field, a cookie, a parameter).
2. **Send adversarial values.** Submit `role=admin`, `level=owner`, or a higher privilege than authorized.
3. **Confirm enforcement.** Verify the app grants the privilege (an admin page loads, a privileged action succeeds).
4. **Escalate.** Perform a privileged action or access privileged data.
5. **Document the field, payload, and impact.

## Example Findings

- `?role=admin` grants admin in a user profile update.
- A cookie `privilege=superuser` accepted by an API.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).