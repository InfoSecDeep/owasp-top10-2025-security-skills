
name: cwe-540-sensitive-info-in-source
description: Use when secrets/keys in source or JS are exposed over HTTP.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-540, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-540 - Sensitive Information in Source Code

CWE-540: Inclusion of Sensitive Information in Source Code - secrets (passwords, API keys) are embedded in source code accessible over the network (JS bundles, exposed sources).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-540 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when secrets/keys are found in source code or JS exposed via HTTP.

## Detection & Test

1. Enumerate exposed source and JS bundles (Test Procedure step 9).
2. Search for secrets: password, secret, key, token literals.
3. Confirm the code is network-accessible and unobfuscated.
4. Decode/trace the secret's use; confirm it authenticates.

## Example Requests

```http
GET /app.js (apiKey=...)
```
```http
secret in source
```

## Bypass Tricks

- Fetch the unminified JS bundle and grep for keys/passwords.
- Read a `.git` leak to extract source with secrets.
- Inspect a source-map (`*.js.map`) that maps back to readable source.
- Look for secrets in commented-out code.


## Impact

- Recoverable credentials/keys embedded in code.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).