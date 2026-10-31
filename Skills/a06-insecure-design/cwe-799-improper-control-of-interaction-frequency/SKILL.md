
name: cwe-799-improper-control-of-interaction-frequency
description: Use when a state-changing action lacks rate limiting.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-799, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-799 - Improper Control of Interaction Frequency

CWE-799: the application does not limit the frequency of an interaction (a login, an OTP, an API call), enabling repeated attacks (brute force, spam, DoS).

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-799 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an endpoint has no rate limiting on a repeated action (login, OTP, API).

## Detection & Test

1. **Find the interaction.** Identify the repeated action (login, OTP verification, an API endpoint).
2. **Send sustained requests.** Fire many requests in a short window.
3. **Confirm no limit.** Show there is no 429, throttle, or lockout.
4. **Escalate.** Use the unlimited frequency to brute-force a credential or OTP.
5. **Document the endpoint, the sustained requests, and the absence of a limit.

## Example Findings

- Login with unlimited attempts to brute-force a password.
- An OTP endpoint with no rate limit to brute-force a code.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).