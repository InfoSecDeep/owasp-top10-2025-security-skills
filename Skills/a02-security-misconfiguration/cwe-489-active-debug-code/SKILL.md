
name: cwe-489-active-debug-code
description: Use when debug/test endpoints or handlers are live in prod.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-489, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-489 - Active Debug Code

CWE-489: Active Debug Code - the application ships with debug/test handlers enabled in a production environment.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-489 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when debug/test endpoints or handlers are enabled in production.

## Detection & Test

1. Enumerate common debug endpoints (`/phpinfo.php`, `/debug`, `/test`, `/console`).
2. Confirm the endpoint is reachable in production.
3. Check that it returns verbose info (stack traces, file paths, version).
4. Look for a `?debug=1` flag that enables a debug handler.

## Example Requests

```http
GET /phpinfo.php (200 in production)
```
```http
GET /debug?debug=1
```

## Bypass Tricks

- Hit a `?debug=1` flag that bypasses the auth check.
- Exploit a `/test` route that exposes a verbose admin API.
- Use a `/console` endpoint that returns a stack trace.
- Bypass a `Server` header that hides the debug state.

## Impact

- Information disclosure and potential privilege escalation via a live debug handler.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).