
name: cwe-1125-excessive-attack-surface
description: Use when a web design flaw matching cwe-1125 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1125, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-1125 - Excessive Attack Surface

CWE-1125: the app exposes more functionality, endpoints, or configuration than required (debug tools, admin panels, legacy APIs), giving attackers an enlarged target.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-1125 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an app exposes unjustified functionality (debug endpoints, admin tools, legacy APIs, unused configs).

## Detection & Test

1. **Enumerate surface.** Find debug endpoints, admin tools, legacy APIs, and config files.
2. **Confirm exposure.** Reach each and check whether it is required and protected.
3. **Assess protection.** If a resource is public and unjustified, flag it as excessive surface.
4. **Escalate.** If the surface is unprotected, use it to reach privileged data or actions.
5. **Document the surface, exposure, and the justification gap.

## Example Findings

- A `/console` endpoint exposed to the public.
- A legacy API endpoint with no auth and privileged data.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).