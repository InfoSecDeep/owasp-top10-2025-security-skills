
name: cwe-547-hardcoded-security-constant
description: Use when a key/token/salt is hard-coded in source or JS.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-547, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-547 - Hard-coded Security-Relevant Constant

CWE-547: Hard-coded Security-Relevant Constant - the application hardcodes a security-relevant constant (API key, salt, token) in source code.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-547 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a security-relevant value (key, token, salt) is hardcoded in source or JS.

## Detection & Test

1. Enumerate JS bundles and source files for hardcoded keys.
2. Grep for `apiKey`, `secretKey`, `salt`, `token` literals.
3. Confirm the constant is used for authentication/encryption.
4. Check for a hardcoded IV/salt that weakens the encryption.

## Example Requests

```http
GET /app.js (apiKey='abc123')
```
```http
secret in source
```

## Bypass Tricks

- Grep a JS bundle for `apiKey=`.
- Exploit a hardcoded salt to precompute a hash table.
- Read a `.git` leak to find the constant's history.
- Use the hardcoded value to forge a token.

## Impact

- Recover a hardcoded key/token/salt that weakens the app.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).