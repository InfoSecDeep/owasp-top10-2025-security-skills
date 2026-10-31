
name: cwe-359-exposure-of-ppi
description: Use when PII is exposed to an actor who should not see it.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-359, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-359 - Exposure of Private Personal Information

CWE-359: Exposure of Private Personal Information - private PII (name, SSN, email, phone, etc.) is unintentionally exposed in URL, tokens, error messages, or logs.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-359 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when PII is exposed (params, error messages, logs) to an actor who should not receive it.

## Detection & Test

1. Enumerate endpoints/params that carry identifiers or profile data.
2. Trigger errors/metadata to see if PII leaks in messages or tokens.
3. Check tokens for encoded PII; verify it is not sent in cleartext parameters.
4. Confirm two actors where one receives another's PII.

## Example Requests

```http
GET /api/profile?full_name=&email=
```
```http
GET /error/{pii} -> 200 PII
```

## Bypass Tricks

- Trigger a verbose error that echoes PII (name, email, phone).
- Read PII embedded in a token or cookie.
- Use a second account to pull another user's profile.
- Check API list endpoints for over-exposed fields.


## Impact

- Unauthorized disclosure of personal identifying information.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).