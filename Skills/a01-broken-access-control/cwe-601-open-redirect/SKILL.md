
name: cwe-601-open-redirect
description: Use when a redirect param points to an attacker domain.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-601, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-601 - Open Redirect

CWE-601: Open Redirect - the application uses user-controlled input to build a redirect, sending the victim's browser to an attacker host.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-601 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a redirect URL parameter points to an attacker-controlled host.

## Detection & Test

1. Find redirect parameters (url, to, next, dest, redirect).
2. Set the value to an attacker host; confirm the response is a 3xx redirect to it.
3. Use open redirect for phishing, token theft (OAuth redirect), or session fixation.
4. Verify the target host is attacker-controlled and the redirect is sent.

## Example Requests

```http
GET /redirect?url=https://attacker.com/
```
```http
GET /logout?next=//attacker.com
```

## Bypass Tricks

- Bypass a domain allowlist with `//attacker.com`, `\\attacker.com`, `https:attacker.com`.
- Use tab/newline injection: `https://trusted.com\nhttps://attacker.com`.
- Exploit a subdomain of the target: `https://attacker.target.com/`.
- Use a trusted domain that itself redirects (e.g., a URL shortener).
- Truncate with `?` or `#`: `https://trusted.com?redirect=attacker.com`.


## Impact

- Victim's browser redirected to an attacker-controlled host.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).