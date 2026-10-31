
name: cwe-315-cleartext-cookie
description: Use when a session cookie is unencrypted or lacks Secure.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-315, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-315 - Cleartext Storage of Sensitive Information in a Cookie

CWE-315: Cleartext Storage of Sensitive Information in a Cookie - the application stores a sensitive value in a cookie that is sent in cleartext.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-315 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an authentication/session cookie is stored without encryption or the `Secure` flag.

## Detection & Test

1. Inspect `Set-Cookie` for `Secure`, `HttpOnly`, `SameSite` attributes.
2. Confirm the cookie is sent over HTTP (not just HTTPS).
3. Read the cookie value and check if it's base64/encoded (not encrypted).
4. Use a second host to see if the cookie is echoed.

## Example Requests

```http
curl -v /login (Set-Cookie: session=...; no Secure)
```

## Bypass Tricks

- Force the cookie to be sent over HTTP (no `Secure`).
- Exploit a load balancer that terminates TLS but forwards cleartext.
- Read the cookie from browser storage if it's not `HttpOnly`.
- Use a downgrade attack to strip the `Secure` flag.

## Impact

- Session/credential theft via a cleartext cookie.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).