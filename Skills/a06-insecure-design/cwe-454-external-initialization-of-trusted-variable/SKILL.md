
name: cwe-454-external-initialization-of-trusted-variable
description: Use when a web design flaw matching cwe-454 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-454, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-454 - External Initialization of Trusted Variable or Class

CWE-454: a variable that the code trusts (a role, a privilege, a security state) is initialized or modified by untrusted input.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-454 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a trusted variable (a flag, role, or security state) is set from a cookie, header, or parameter.

## Detection & Test

1. **Find trusted variables.** Identify where the app trusts a variable (a role, privilege, or auth flag).
2. **Identify the source.** Confirm the variable is initialized from untrusted input.
3. **Send an adversarial value.** Set the variable to a privileged value via the untrusted source.
4. **Confirm and escalate.** Verify the trusted variable now has the attacker-controlled value.
5. **Document the variable, its source, and the proof.

## Example Findings

- A `privileged` flag initialized from a cookie.
- An `isAdmin` boolean set from a request parameter.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).