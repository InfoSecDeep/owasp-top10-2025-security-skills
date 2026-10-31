
name: cwe-653-insufficient-compartmentalization
description: Use when a design permits more inputs than required.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-653, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-653 - Insufficient Compartmentalization

CWE-653: a low-privilege component can access a high-privilege component's resources or functions (weak isolation), so a compromise of one bypasses the other's protection.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-653 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a low-privilege component can reach a high-privilege resource (weak sandboxing or layering).

## Detection & Test

1. **Identify privilege levels.** Identify components at different privilege levels.
2. **Find the shared access.** Determine where a low-privilege component can reach a high-privilege resource.
3. **Trigger the access.** Use the low-privilege path to reach the high-privilege resource.
4. **Escalate.** Confirm the resource was reached and extract sensitive data.
5. **Document the levels, the shared access, and proof.

## Example Findings

- A low-privilege worker can read a high-privilege component's database.
- A weak sandbox that a low-privilege component can escape.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).