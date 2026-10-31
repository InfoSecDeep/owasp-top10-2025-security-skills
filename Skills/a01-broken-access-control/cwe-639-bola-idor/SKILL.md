
name: cwe-639-bola-idor
description: Use when a resource ID/key reaches another actor's object.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-639, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-639 - Authorization Bypass via User-Controlled Key (BOLA/IDOR)

CWE-639: Authorization Bypass via User-Controlled Key - an in-scope ID/parameter (key) can be changed to authorize access to or modification of another entity's resource (BOLA).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-639 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a resource ID/key can be changed to access/modify another actor's resource (BOLA).

## Detection & Test

1. Identify a resource keyed by an in-scope value.
2. Fetch as actor A; change the key to actor B's value.
3. Confirm access/modification of actor B's resource.
4. Demonstrate the real privilege difference (Test Procedure steps 1-3).

## Example Requests

```http
GET /api/user/{uid} as session A -> B's data
```
```http
PUT /api/user/{uid} as A -> B
```

## Bypass Tricks

- Change the resource key to another actor's value and re-request.
- Step an auto-incrementing key.
- Use a key from an error message or another session.
- Modify the key on write (PUT/PATCH) to take over the resource.


## Impact

- Unauthorized access/modification of another actor's resource.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).