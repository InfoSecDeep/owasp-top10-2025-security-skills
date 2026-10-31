
name: cwe-1391-weak-credentials
description: Use when a web auth flaw matches cwe-1391.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1391, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-1391 - Use of Weak Credentials

CWE-1391: the credentials are weak (a short password, a common password, a predictable value), allowing easy brute-force or guess attacks.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-1391 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the credentials (a password, a token) are weak (short, common, or predictable).

## Detection & Test

1. **Map the credentials.** Identify the password, token, or credential in use.
2. **Assess the weakness.** Check whether it is short, common, or predictable.
3. **Attempt brute-force or guess.** Use a wordlist or a pattern to guess the credential.
4. **Confirm access.** Verify the login succeeds.
5. **Document the credential, the weakness, and proof.

## Example Findings

- A password that is `123456` (common).
- A token that is a sequential number (predictable).

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).