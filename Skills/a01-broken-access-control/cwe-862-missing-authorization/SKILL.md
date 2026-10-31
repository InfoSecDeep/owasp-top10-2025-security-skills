
name: cwe-862-missing-authorization
description: Use when an endpoint exposes functionality with no authz.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-862, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-862 - Missing Authorization

CWE-862: Missing Authorization - the application does not check authorization before granting access to a resource (no authz middleware).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-862 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an endpoint exposes functionality with no authorization check at all.

## Detection & Test

1. Identify endpoints with no authz layer.
2. Directly request the endpoint as an unauthenticated/unprivileged actor.
3. Confirm the server returns privileged data/behavior.
4. Check for routes bypassing authorization middleware entirely.

## Example Requests

```http
GET /api/admin/users (no token) -> 200 privileged data
```

## Bypass Tricks

- Request the endpoint with no token at all.
- Hit the route as an unauthenticated user.
- Bypass a route that forgot its auth middleware.
- Access a newly added endpoint before authz was wired up.


## Impact

- Privileged resource reachable with no authorization.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).