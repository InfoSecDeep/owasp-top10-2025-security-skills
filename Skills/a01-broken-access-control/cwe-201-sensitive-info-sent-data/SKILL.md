
name: cwe-201-sensitive-info-sent-data
description: Use when a param/token/payload carries secrets/PII onward.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-201, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-201 - Exposure of Sensitive Information Through Sent Data

CWE-201: Exposure of Sensitive Information Through Sent Data - sensitive data (auth info, PII) is unintentionally included in transmitted data (URL params, tokens, logs, network messages).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-201 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an app embeds secrets or PII in parameters, tokens, or payloads that get transmitted or visible to others.

## Detection & Test

1. Enumerate parameters (query, path, cookies, headers, POST); decode tokens (JWT) and check for embedded secrets.
2. Flag sensitive values in cleartext URL params or tokens sent over HTTP.
3. Use the app to read cookies it emits; ensure tokens are HttpOnly, Secure, SameSite.
4. Check for sensitive values logged on the client/server.

## Example Requests

```http
GET /profile?apikey=abcdef123456789
```
```http
curl -v /login  (Set-Cookie=token in cleartext over HTTP)
```

## Bypass Tricks

- Read cleartext `Authorization` / `Cookie` on the wire (HTTP, not HTTPS).
- Decode a JWT to find embedded claims/keys.
- Capture the URL (query string holds the key) in logs and browser history.
- Use a proxy to capture the request/response and inspect the token.
- Check for the key echoed in response headers.


## Impact

- Auth info / PII transmitted visibly and recoverable by an observer or another actor.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).