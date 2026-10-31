
name: cwe-657-violation-of-secure-design-principles
description: Use when a web design flaw matching cwe-657 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-657, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-657 - Violation of Secure Design Principles

CWE-657: the application violates a secure design principle (minimum privilege, defense in depth, separation of duties, least function), making a security property weak or absent.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-657 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an app violates a secure design principle: minimum privilege, defense in depth, separation of duties, or least privilege.

## Detection & Test

1. **Identify the principle.** Determine which principle is at risk (minimum privilege, defense in depth, etc.).
2. **Test the design.** Send inputs that exercise the principle (e.g. a low-privilege actor reaching a privileged resource).
3. **Confirm the violation.** Show the principle is violated (the actor succeeds where it shouldn't).
4. **Escalate.** Use the violation to bypass a control.
5. **Document the principle, the design, and proof.

## Example Findings

- A low-privilege user reaching a privileged resource.
- A single actor able to both request and approve a change.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).