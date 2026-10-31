
name: cwe-615-sensitive-info-code-comments
description: Use when code comments leak secrets or sensitive hints.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-615, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-615 - Sensitive Information in Code Comments

CWE-615: Comment Injection (Information Exposure) - comments in source/HTML/JS contain sensitive info that aids an attacker.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-615 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when comments in HTML/JS/PHP leak secrets or hints about the app.

## Detection & Test

1. Fetch HTML/JS/PHP responses; inspect comments.
2. Search comments for secrets, TODO hints, or internal paths.
3. Confirm the leaked comment enables further attacks.
4. Check for comments in served code (not just build artifacts).

## Example Requests

```http
GET /app.js (// api_key=...)
```
```http
GET /style.css (admin panel path)
```

## Bypass Tricks

- Read the served HTML/JS and search for `//`, `<!-- -->`, `/* */` blocks.
- Grep for `api_key`, `secret`, `password`, `TODO`, `FIXME`.
- Exploit a minifier that failed to strip comments.
- Read source-maps that include the commented source.


## Impact

- Sensitive data/hints exposed in comments.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).