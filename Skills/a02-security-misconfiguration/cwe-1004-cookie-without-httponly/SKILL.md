
name: cwe-1004-cookie-without-httponly
description: Use when an auth cookie lacks HttpOnly, so JS can read it.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1004, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-1004 - Sensitive Cookie without 'HttpOnly' Flag

CWE-1004: Sensitive Cookie without 'HttpOnly' Flag - the application sets a sensitive cookie without the `HttpOnly` flag, allowing JavaScript to read it.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-1004 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an authentication cookie is missing the `HttpOnly` flag, so JS can read it.

## Detection & Test

1. Inspect `Set-Cookie` for the `HttpOnly` attribute.
2. Confirm the cookie is readable from the browser's `document.cookie`.
3. Exploit an XSS to read the cookie.
4. Check for a `Secure` flag as well (compound misconfiguration).

## Example Requests

```http
curl -v /login (Set-Cookie: session=...; no HttpOnly)
```

## Bypass Tricks

- Exploit an XSS to read the cookie from `document.cookie`.
- Use a `fetch` from an untrusted context to read the cookie.
- Read the cookie from browser storage if it's not `HttpOnly`.
- Combine with a missing `Secure` flag for cleartext + JS access.

## Impact

- Session/credential theft via a cookie readable by JavaScript.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).