
name: cwe-620-unverified-password-change
description: Use when a web auth flaw matches cwe-620.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-620, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-620 - Unverified Password Change

CWE-620: a password change is not verified, so a change with a stolen or interim token is accepted.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-620 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a password change is not verified (a change with a stolen or interim token is accepted).

## Detection & Test

1. **Find the password change flow.** Identify the endpoint or action for changing a password.
2. **Use a stolen token.** Send the change request with a stolen or interim token.
3. **Confirm the change is accepted.** Show the password is changed without proper verification.
4. **Escalate.** Use the new password to log in or lock out the original user.
5. **Document the flow, the token, and proof.

## Example Findings

- A password change endpoint that accepts a request with a stolen session token.
- A change that locks out the original user without re-authentication.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).