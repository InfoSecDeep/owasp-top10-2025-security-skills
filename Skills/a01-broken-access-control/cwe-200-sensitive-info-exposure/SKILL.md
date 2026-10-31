
name: cwe-200-sensitive-info-exposure
description: Use when a response, log, or header leaks data to an actor.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-200, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-200 - Exposure of Sensitive Information to Unauthorized Actor

CWE-200: Exposure of Sensitive Information - information the code must protect for privacy/legal reasons is inadvertently exposed (to the network, logs, traces, errors, or the wrong actor).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-200 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a response or log leaks credentials, keys, tokens, or personal data to an actor who should not receive it.

## Detection & Test

1. Inspect responses/headers/cookies/logs for secrets: passwords, API keys, JWTs, private keys, session tokens.
2. Force error paths (wrong input, 500s) to see if the server leaks keys/paths/SQL.
3. Compare two roles; ensure a low-priv actor does not receive data scoped to a higher role.
4. Check response bodies, HTTP headers, Server, and logs for hardcoded secrets.

## Example Requests

```http
GET /api/whoami  (200 reveals passwordHash)
```
```http
GET /api/user?id=999999  (500 with stack/keys)
```

## Bypass Tricks

- Trigger 500s to force verbose stack traces that name keys/paths.
- Inspect verbose error `Server` headers and custom headers that echo secrets.
- Request with `Accept-Encoding` to coax plaintext responses.
- Overlook `Set-Cookie` / auth headers that leak a session token to a lower-priv caller.
- Use a second account to diff responses and catch cross-role leakage.


## Impact

- Unauthorized disclosure of credentials, keys, or PII that the app was supposed to protect.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).