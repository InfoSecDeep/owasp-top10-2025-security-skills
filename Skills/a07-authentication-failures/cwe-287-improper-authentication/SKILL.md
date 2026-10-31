
name: cwe-287-improper-authentication
description: Use when a web auth flaw matches cwe-287.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-287, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-287 - Improper Authentication

CWE-287: authentication is missing or broken, so a request reaches a resource without a valid identity check.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-287 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an endpoint is reachable without authentication, or the auth check is flawed.

## Detection & Test

1. **Find the resource.** Identify a resource or endpoint that requires authentication.
2. **Access it unauthenticated.** Send a request without credentials.
3. **Confirm the resource is reached.** Show the resource is accessible or the check is bypassed.
4. **Escalate.** Use the unauthenticated access to read data or perform an action.
5. **Document the resource, the missing check, and proof.

## Example Findings

- An API endpoint returning data without a token.
- A page that loads without a session cookie.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).