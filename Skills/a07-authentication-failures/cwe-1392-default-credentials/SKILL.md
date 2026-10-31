
name: cwe-1392-default-credentials
description: Use when a web auth flaw matches cwe-1392.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1392, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-1392 - Use of Default Credentials

CWE-1392: default credentials (the out-of-box username and password) are not changed, so anyone who knows the default can log in.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-1392 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the default credentials (out-of-box username and password) are not changed.

## Detection & Test

1. **Identify the default credentials.** Find the out-of-box username and password.
2. **Attempt login.** Use the default credentials to authenticate.
3. **Confirm access.** Verify the login succeeds and grants access.
4. **Escalate.** Use the default credentials to reach a protected resource.
5. **Document the credentials, the default, and proof.

## Example Findings

- A default `admin/admin` on a login page.
- An out-of-box `root/password` on a database.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).