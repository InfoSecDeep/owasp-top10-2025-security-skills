
name: cwe-642-external-control-of-critical-state-data
description: Use when a web design flaw matching cwe-642 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-642, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-642 - External Control of Critical State Data (Remote Override)

CWE-642: untrusted input can override a critical state value (a privilege, a role, or a security state) that the server should own.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-642 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a critical state value (privilege, role, or security state) is set from user-controlled input.

## Detection & Test

1. **Find critical state.** Identify privileged or security state values (a role, a flag, a privilege).
2. **Send an adversarial override.** Submit a privileged value via the user-controlled input.
3. **Confirm the override.** Verify the server uses the attacker-supplied value.
4. **Escalate.** Use the overridden state to perform a privileged action.
5. **Document the state field, payload, and proof.

## Example Findings

- A `privilege` field overridden in a profile update.
- A `flag` that grants elevated access, set from a request.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).