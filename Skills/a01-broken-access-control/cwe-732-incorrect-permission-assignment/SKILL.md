
name: cwe-732-incorrect-permission-assignment
description: Use when resource permissions are too permissive per actor.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-732, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-732 - Incorrect Permission Assignment for Critical Resource

CWE-732: Incorrect Permission Assignment for Critical Resource - an application assigns too-permissive permissions to a critical resource (file, dir, or object).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-732 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when file/directory/resource permissions are too permissive, granting access beyond the intended actor.

## Detection & Test

1. Inspect permissions of files/dirs/object storage the app manages.
2. Determine whether the assigned ACL is broader than intended.
3. Access the resource as an unprivileged actor; confirm 200.
4. Check default ACLs of newly created managed resources.

## Example Requests

```http
GET /admin/config -> 200 (world-readable)
```

## Bypass Tricks

- Read a world-readable config file via the web path.
- Access the resource as an unprivileged user to confirm the ACL is too broad.
- Check the default ACL of newly created managed resources.
- Exploit a directory with overly permissive execute/read bits.


## Impact

- Over-permissive resource accessible to an unprivileged actor.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).