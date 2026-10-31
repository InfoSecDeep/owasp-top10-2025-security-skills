
name: cwe-289-auth-bypass-alternate-name
description: Use when a web auth flaw matches cwe-289.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-289, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-289 - Authentication Bypass by Alternate Name

CWE-289: authentication accepts an alternate name or case variation of the expected credential (admin vs Admin vs ADMIN), allowing the attacker to log in with a slightly different value.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-289 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the authentication check is case-insensitive or accepts alternate forms of the credential.

## Detection & Test

1. **Identify the credential.** Find the expected username/password/role value.
2. **Send case variations.** Try `Admin`, `ADMIN`, `aDmin` and other case variations.
3. **Confirm the bypass.** Show the authentication accepts the variant.
4. **Escalate.** Log in with the alternate name.
5. **Document the credential, the variant, and proof.

## Example Findings

- `admin` accepted as `Admin` or `ADMIN`.
- An email `user@example.com` accepted as `User@Example.COM`.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).