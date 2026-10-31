
name: cwe-566-idor-sql-key
description: Use when a resource ID/key reaches another actor's object.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-566, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-566 - IDOR (Authorization Bypass via User-Controlled SQL Key)

CWE-566: Authorization Bypass via User-Controlled SQL Key - an in-scope ID parameter can be modified (stepped) to authorize access to a record belonging to another entity (classic IDOR).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-566 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an in-scope ID parameter (user/order/invoice) can be stepped/changed to access another actor's record.

## Detection & Test

1. Identify an ID parameter (user/order/invoice/doc).
2. Fetch a record as actor A; then step the ID to another actor's value (Test Procedure step 2).
3. Confirm the server returned the other actor's record.
4. Prove actor B truly lacked privilege (not just a different status code).

## Example Requests

```http
GET /api/order/1001 (as user 1) -> returns order 2002 data
```

## Bypass Tricks

- Step the numeric ID by ±1 to reach the adjacent record.
- Swap the ID for another user's known value.
- Use a UUID/long ID from another session.
- Modify the ID in a PUT/PATCH to claim the resource.


## Impact

- Unauthorized access to another actor's record via ID manipulation.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).