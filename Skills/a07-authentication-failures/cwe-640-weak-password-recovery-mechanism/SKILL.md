
name: cwe-640-weak-password-recovery-mechanism
description: Use when a web auth flaw matches cwe-640.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-640, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-640 - Weak Password Recovery Mechanism

CWE-640: the password recovery mechanism is weak (guessable tokens, IDOR on the recovery endpoint, no rate limit), allowing the attacker to recover a password.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-640 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the password recovery mechanism (reset link, token) is weak (guessable, IDOR, no rate limit).

## Detection & Test

1. **Find the recovery endpoint.** Identify the password reset or recovery endpoint.
2. **Test token strength.** Check whether the token is guessable, short, or predictable.
3. **Test IDOR.** Send the recovery request with another user's token or ID.
4. **Confirm the recovery.** Show the attacker can reset the password.
5. **Document the token, the weakness, and proof.

## Example Findings

- A reset token that is a sequential number (IDOR).
- A recovery endpoint with no rate limit to brute-force a token.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).