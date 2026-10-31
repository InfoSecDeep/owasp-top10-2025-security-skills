
name: cwe-1393-default-password
description: Use when a web auth flaw matches cwe-1393.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1393, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-1393 - Use of Default Password

CWE-1393: a default password is not changed on a service or account, so anyone who knows the default can log in.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-1393 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a default password is not changed on a service or account.

## Detection & Test

1. **Identify the default password.** Find the out-of-box password for the service or account.
2. **Attempt login.** Use the default password to authenticate.
3. **Confirm access.** Verify the login succeeds and grants access.
4. **Escalate.** Use the default password to reach a protected resource.
5. **Document the service, the default password, and proof.

## Example Findings

- A default `password` on a service account.
- An out-of-box `secret` on a database user.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).