
name: cwe-472-external-control-of-assumed-immutable-web-parameter
description: Use when a web design flaw matching cwe-472 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-472, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-472 - External Control of Assumed-Immutable Web Parameter

CWE-472: a web parameter the app assumes is immutable (e.g. a role or privilege) is actually controlled by the attacker (set in a cookie or request), bypassing the control.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-472 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter assumed immutable (a role, privilege, or auth flag) is set in a cookie or request.

## Detection & Test

1. **Find the immutable parameter.** Identify a role, privilege, or auth flag the app treats as immutable.
2. **Locate where it is set.** Confirm it is set in a cookie or parameter the attacker controls.
3. **Send an adversarial value.** Set the parameter to a privileged value.
4. **Confirm and escalate.** Verify the app acts on the attacker-controlled value.
5. **Document the parameter, source, and proof.

## Example Findings

- A `role` cookie the app treats as immutable but the attacker can set.
- A `privilege` parameter read from a cookie.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).