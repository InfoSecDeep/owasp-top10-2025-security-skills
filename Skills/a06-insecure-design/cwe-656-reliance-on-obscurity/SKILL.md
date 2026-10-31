
name: cwe-656-reliance-on-obscurity
description: Use when a web design flaw matching cwe-656 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-656, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-656 - Reliance on Obscurity

CWE-656: a control relies on something being secret or non-obvious (a guessed path, a hidden endpoint, an undocumented parameter), so an attacker who discovers it bypasses the control with no real protection.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-656 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a control relies on an attacker not knowing a path, endpoint, or parameter.

## Detection & Test

1. **Identify obscurity-based controls.** Find endpoints, paths, or parameters used as a control (a hidden `/console`, an undocumented route).
2. **Enumerate.** Guess or brute-force the hidden value.
3. **Confirm the bypass.** Show reaching the resource (no real authn/authz behind the obscurity).
4. **Escalate.** Use the hidden resource.
5. **Document the control, the hidden value, and proof.

## Example Findings

- A `/console` endpoint that is reached by guessing the path.
- A hidden admin route that is only "protected" by being undocumented.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).