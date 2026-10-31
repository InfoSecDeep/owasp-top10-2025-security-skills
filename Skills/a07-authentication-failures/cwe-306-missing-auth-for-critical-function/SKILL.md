
name: cwe-306-missing-auth-for-critical-function
description: Use when a web auth flaw matches cwe-306.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-306, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-306 - Missing Authentication for Critical Function

CWE-306: a critical function (delete, transfer, admin action) is accessible without authentication, so anyone can perform it.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-306 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a critical function (delete, transfer, admin action) is accessible without authentication.

## Detection & Test

1. **Identify the critical function.** Find the function that should require authn (delete, transfer, admin).
2. **Access it unauthenticated.** Send a request without credentials.
3. **Confirm the function is performed.** Show the function executes without authn.
4. **Escalate.** Use the function to perform the action.
5. **Document the function, the missing authn, and proof.

## Example Findings

- A `/delete` endpoint that works without a token.
- A `/transfer` endpoint that processes a transfer without authn.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).