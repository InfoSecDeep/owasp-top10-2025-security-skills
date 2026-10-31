
name: cwe-419-unprotected-primary-channel
description: Use when a web design flaw matching cwe-419 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-419, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-419 - Unprotected Primary Channel

CWE-419: a client communicates over a primary channel but a secondary channel is available that is easier to reach or less protected, allowing the attacker to use the weaker path instead of the primary one.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-419 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an app has a secondary channel (a fallback endpoint, an insecure port) that is less protected than the primary.

## Detection & Test

1. **Identify channels.** Map the primary and secondary channels (http vs https, port 80 vs 443, alternate endpoints).
2. **Switch to the secondary channel.** Send the same request over the secondary channel.
3. **Confirm reduced security.** Show the secondary channel lacks the primary's protection (cleartext, no auth, no validation).
4. **Escalate.** Use the secondary channel to bypass the primary's controls.
5. **Document the channels, the switch, and the gap.

## Example Findings

- An API over https:// that also serves the same data over http://.
- A fallback endpoint on port 8080 without the primary's access check.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).