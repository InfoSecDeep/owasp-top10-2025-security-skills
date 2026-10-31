
name: cwe-798-hard-coded-credentials
description: Use when credentials are hard-coded in source/config/JS.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-798, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-798 - Use of Hard-Coded Credentials

CWE-798: hard-coded credentials (username and password) are embedded in source or a static file, so anyone who can read the file can log in.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-798 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When hard-coded credentials (username and password) are embedded in source or a static file.

## Detection & Test

1. **Search for credentials.** Grep source, config, and static files for username and password pairs.
2. **Identify the hard-coded value.** Confirm it is a fixed literal.
3. **Attempt login.** Use the hard-coded credentials to authenticate.
4. **Confirm access.** Verify the login succeeds and grants access.
5. **Document the file, the credentials, and proof.

## Example Findings

- `user = "admin"; pass = "password"` in a source file.
- A config with `db_user: root` and `db_pass: secret`.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).