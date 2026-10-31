
name: cwe-614-cookie-without-secure
description: Use when an auth cookie lacks Secure and goes over HTTP.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-614, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-614 - Sensitive Cookie without 'Secure' Attribute

CWE-614: Sensitive Cookie without 'Secure' Attribute - the application sets a sensitive cookie without the `Secure` attribute, allowing it to be sent over cleartext HTTP.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-614 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an authentication cookie is missing the `Secure` attribute, so it can be sent over HTTP.

## Detection & Test

1. Inspect `Set-Cookie` for the `Secure` attribute.
2. Confirm the cookie is sent over HTTP (not just HTTPS).
3. Read the cookie value from the browser storage.
4. Use a second host to see if the cookie is echoed.

## Example Requests

```http
curl -v /login (Set-Cookie: session=...; no Secure)
```

## Bypass Tricks

- Force the cookie to be sent over HTTP (no `Secure`).
- Exploit a load balancer that terminates TLS but forwards cleartext.
- Use a downgrade attack to strip the `Secure` flag.
- Read the cookie from browser storage.

## Impact

- Session/credential theft via a cookie sent over HTTP.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).