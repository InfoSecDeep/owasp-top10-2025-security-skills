
name: cwe-922-insecure-storage
description: Use when secrets/tokens/cookies are stored insecurely.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-922, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-922 - Insecure Storage of Sensitive Information

CWE-922: Insecure Storage of Sensitive Information - an application stores protected data (passwords, tokens) insecurely (plaintext, weak encryption, predictable cookies).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-922 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when secrets (passwords, tokens, cookies) are stored or persisted insecurely on the server.

## Detection & Test

1. Check stored secrets: plaintext passwords, weak hashing, weak encryption.
2. Inspect cookie storage for cleartext/weakly-encoded secrets (Test Procedure step 7).
3. Confirm the stored secret can be recovered by an unauthorized actor.
4. Verify cookies for proper flags and encryption.

## Example Requests

```http
Cookie: token=plaintext_base64
```
```http
GET /config -> stored plaintext password
```

## Bypass Tricks

- Read a cookie/session stored in cleartext or weak encoding.
- Inspect a stored plaintext password in a config or DB dump.
- Exploit weak/unsalted hash by reversing it.
- Read a token stored in a log or temp file.
- Check for secrets in `.bak`/`.old` files.


## Impact

- Recoverable stored secrets (cookies, DB, files).

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).