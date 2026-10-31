
name: cwe-286-incorrect-user-management
description: Use when a web design flaw matching cwe-286 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-286, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-286 - Incorrect User Management

CWE-286: user management (registration, activation, role assignment, or deletion) is handled incorrectly, allowing an actor to gain a role or identity they should not.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-286 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When user registration, activation, or role assignment can be manipulated to grant an unintended role.

## Detection & Test

1. **Map user management flows.** Identify registration, activation, email verification, and role changes.
2. **Bypass verification.** Skip the email activation step, replay the activation token, or reuse a registration flow.
3. **Test role assignment.** Submit a privileged role during registration or a later profile update.
4. **Confirm and escalate.** Log in with the elevated role and perform a privileged action.
5. **Document the flow, payload, and impact.

## Example Findings

- An account is activated without verifying the email link.
- A new user can register with `role=admin`.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).