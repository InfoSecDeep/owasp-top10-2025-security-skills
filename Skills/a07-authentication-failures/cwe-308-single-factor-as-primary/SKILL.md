
name: cwe-308-single-factor-as-primary
description: Use when a web auth flaw matches cwe-308.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-308, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-308 - Single-Factor Authentication

CWE-308/309: single-factor (password-only) is the primary authentication method, without a second factor (MFA), so a compromised password grants full access.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-308 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the primary authentication is single-factor (password-only) without MFA.

## Detection & Test

1. **Identify the primary factor.** Find the main authentication method (a password, a token).
2. **Check for a second factor.** Confirm whether MFA is required.
3. **Bypass with single factor.** Log in with only the password.
4. **Confirm the bypass.** Show the single factor is sufficient for access.
5. **Document the factor, the missing second factor, and proof.

## Example Findings

- A login that works with only a password, no MFA.
- An API that accepts only a Bearer token, no MFA.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).