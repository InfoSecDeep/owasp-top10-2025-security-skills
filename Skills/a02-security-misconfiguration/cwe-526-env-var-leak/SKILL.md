
name: cwe-526-env-var-leak
description: Use when a response/debug endpoint leaks env vars/secrets.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-526, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-526 - Exposure of Sensitive Information Through Environmental Variables

CWE-526: Exposure of Sensitive Information Through Environmental Variables - the application exposes OS environment variables or secrets in a response.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-526 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a response or debug endpoint leaks OS environment variables or secrets.

## Detection & Test

1. Fetch a debug/verbose endpoint that dumps the environment.
2. Check the response headers and body for `API_KEY`, `SECRET`, `TOKEN`.
3. Confirm the value is a real secret (not a placeholder).
4. Look for a `.env` leak that exposes the same values.

## Example Requests

```http
GET /debug/env (leaks AWS_SECRET_KEY)
```
```http
GET /.env
```

## Bypass Tricks

- Fetch a `/debug/env` endpoint that dumps the full environment.
- Exploit a `.env` leak to read the same secrets.
- Use a verbose error that includes the env path.
- Check a `config.yaml` that interpolates env vars.

## Impact

- Recover secrets (API keys, DB passwords) from environment variables.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).