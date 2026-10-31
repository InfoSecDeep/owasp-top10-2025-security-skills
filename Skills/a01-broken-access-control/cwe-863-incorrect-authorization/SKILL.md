
name: cwe-863-incorrect-authorization
description: Use when an authorization check exists but is bypassed.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-863, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-863 - Incorrect Authorization

CWE-863: Incorrect Authorization - the mechanism that checks authorization is wrong or bypassable (e.g., checks the wrong variable).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-863 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when authorization appears present but is bypassed (broken check, wrong comparison).

## Detection & Test

1. Confirm an authorization layer exists but is flawed.
2. Trigger an unexpected authorization outcome (Test Procedure step 1).
3. Check for common bypass: checking wrong field, comparing wrong variable, bypassed middleware.
4. Verify the actor truly lacks the privilege; confirm the bypass.

## Example Requests

```http
GET /admin?role=admin (flawed check -> 200)
```

## Bypass Tricks

- Exploit a check that compares the wrong variable.
- Bypass a middleware that only checks presence, not validity, of a header.
- Trigger the authz with a malformed value the check accepts.
- Replay a valid-but-out-of-scope token to hit the wrong comparison.


## Impact

- Bypassed authorization (flawed mechanism).

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).