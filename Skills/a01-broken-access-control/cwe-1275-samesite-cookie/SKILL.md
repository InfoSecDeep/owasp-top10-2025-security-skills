
name: cwe-1275-samesite-cookie
description: Use when an auth cookie lacks SameSite, easing theft/CSRF.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1275, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-1275 - Sensitive Cookie with Improper SameSite

CWE-1275: Sensitive Cookie with Improper SameSite - an authentication cookie for a protected resource is missing SameSite, enabling token theft (phishing/bug) and CSRF.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-1275 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an authentication/protected cookie lacks SameSite to mitigate CSRF via cookie theft.

## Detection & Test

1. Inspect the auth/protected cookie's SameSite flag.
2. Confirm it is missing SameSite or set to permissive (None) for a protected resource.
3. Verify an untrusted context can read/use the cookie (CSRF via cookie).
4. Check that the cookie is flagged for a protected resource only.

## Example Requests

```http
Set-Cookie: session=... SameSite=None
```
```http
Cookie sent on cross-origin request
```

## Bypass Tricks

- Send the auth cookie on a cross-origin request (CSRF via cookie).
- Exploit `SameSite=None` without `Secure` (cookie sent over HTTP).
- Craft a cross-origin form/fetch that carries the cookie.
- Phish a victim and read the cookie in the attacker's context.
- Bypass by forcing the cookie to be sent with `credentials:'include'`.


## Impact

- Authentication cookie usable cross-origin (CSRF / cookie theft).

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).