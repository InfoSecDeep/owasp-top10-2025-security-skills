
name: cwe-807-untrusted-input-in-security-decision
description: Use when a web design flaw matching cwe-807 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-807, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-807 - Untrusted Input in a Security Decision

CWE-807: untrusted input is used in a security decision (authn, authz, or a privilege), so an attacker can influence the decision and bypass the control.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-807 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When untrusted input influences a security decision (a privilege, an authn check, or an authz decision).

## Detection & Test

1. **Find the security decision.** Identify where the app decides authn, authz, or a privilege.
2. **Find the input.** Confirm untrusted input reaches the decision.
3. **Send an adversarial value.** Inject a value that changes the decision (grant access, skip a check).
4. **Confirm and escalate.** Verify the decision changed to the attacker's benefit.
5. **Document the decision, the input, and proof.

## Example Findings

- A security check that trusts a client-side value.
- A privilege decision influenced by a request parameter.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).