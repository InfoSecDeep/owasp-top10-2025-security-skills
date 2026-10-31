
name: cwe-602-client-side-enforcement-of-server-side-security
description: Use when a web design flaw matching cwe-602 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-602, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-602 - Client Side Enforcement of Server Side Security

CWE-602: the application relies on a client-side security check, so disabling the client (JS) or spoofing it lets an attacker bypass a server-side control.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-602 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a server-side control depends on a client-side check (JS validation, a client-decided action).

## Detection & Test

1. **Find client-side enforcement.** Identify where the client decides something the server should (a privilege, an action, a value).
2. **Disable the client.** Turn off JS or spoof the client and replay the privileged action.
3. **Confirm the bypass.** Show the privileged action succeeds without the client-side check.
4. **Escalate.** Perform the action the client-side check was supposed to gate.
5. **Document the client check, the bypass, and proof.

## Example Findings

- A JS check hides an admin button; disabling JS still reaches the admin action.
- A payment flow that the client validates but the server doesn't re-check.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).