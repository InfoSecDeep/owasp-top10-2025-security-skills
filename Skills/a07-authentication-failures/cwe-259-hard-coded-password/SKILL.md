
name: cwe-259-hard-coded-password
description: Use when a web auth flaw matches cwe-259.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-259, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-259 - Use of Hard-Coded Password

CWE-259: a password is hard-coded in source, config, or a static file, so anyone who can read the file can log in.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-259 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a password is embedded in source code or a static file (hard-coded).

## Detection & Test

1. **Search for passwords.** Grep source, config, and static files for password-shaped constants.
2. **Identify the hard-coded value.** Confirm it is a fixed literal, not a variable.
3. **Attempt login.** Use the hard-coded password to authenticate.
4. **Confirm access.** Verify the login succeeds and grants access.
5. **Document the file, value, and proof.

## Example Findings

- `password = "admin"` in a source file.
- A static config with `auth_password: supersecret`.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).