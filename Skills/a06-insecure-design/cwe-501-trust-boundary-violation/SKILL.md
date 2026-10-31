
name: cwe-501-trust-boundary-violation
description: Use when a web design flaw matching cwe-501 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-501, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-501 - Trust Boundary Violation

CWE-501: identity or origin is verified by a component on the wrong side of a boundary (e.g. client-side, or an untrusted boundary), so an attacker can cross the boundary without a real verification.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-501 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a security check (identity, origin, signature) is verified client-side or on an untrusted boundary.

## Detection & Test

1. **Map boundaries.** Identify each boundary (client-API, API-DB, cloud, third-party).
2. **Test client-side checks.** Disable JS or spoof the origin and confirm a client-side check is not re-verified server-side.
3. **Cross the boundary.** Send a request that should require server-side authn to an internal resource.
4. **Confirm.** Verify the resource was reached without a real cross-boundary check.
5. **Document the boundary, the skipped check, and proof.

## Example Findings

- A client-side check confirms a user, then the server trusts it without re-authenticating.
- An internal API is reached from the client with a spoofed header.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).