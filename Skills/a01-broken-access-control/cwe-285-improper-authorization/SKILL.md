
name: cwe-285-improper-authorization
description: Use when a user can act beyond their assigned privilege.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-285, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-285 - Improper Authorization

CWE-285: Improper Authorization - the application does not correctly establish/validate a user's identity and privileges before granting access or performing an action.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-285 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a user is allowed to perform actions or access resources beyond their assigned privilege (privilege escalation).

## Detection & Test

1. Identify a resource/endpoint; attempt the action as a lower-privilege actor (Test Procedure step 1).
2. Confirm the server enforced authorization (not just the UI).
3. Vary by endpoint, role, and resource ID; check enforcement at every layer.
4. Prove the actor truly lacked the privilege (not just a different status code).

## Example Requests

```http
GET /admin -> 200 as user_id=2
```
```http
POST /api/admin/role as non-admin
```

## Bypass Tricks

- Replay a privileged request with a low-priv token (BOLA).
- Bump a numeric role value (1→2) in the request.
- Access a higher-role page/endpoint directly via URL.
- Use an expired but not-yet-invalidated session.


## Impact

- Privilege escalation: lower-privilege actor performs privileged actions.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).