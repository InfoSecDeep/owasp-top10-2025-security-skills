
name: cwe-307-improper-restriction-of-excessive-attempts
description: Use when a web auth flaw matches cwe-307.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-307, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-307 - Improper Restriction of Excessive Authentication Attempts

CWE-307: excessive authentication attempts (failed logins, MFA attempts) are not restricted, allowing brute-force attacks.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-307 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When excessive authentication attempts (failed logins) are not restricted (no rate limit, no lockout).

## Detection & Test

1. **Find the auth endpoint.** Identify the login or MFA endpoint.
2. **Send many failed attempts.** Fire a burst of failed logins.
3. **Confirm no restriction.** Show there is no 429, lockout, or CAPTCHA.
4. **Escalate.** Use the unlimited attempts to brute-force a credential.
5. **Document the endpoint, the burst, and the absence of a limit.

## Example Findings

- Login with unlimited failed attempts to brute-force a password.
- An MFA endpoint with no rate limit to brute-force a code.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).