
name: cwe-424-improper-alt-path
description: Use when an alternate path/ftp/second API bypasses control.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-424, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-424 - Improper Protection of Alternate Path

CWE-424: Improper Protection of Alternate Path - an application's access control permits access via an alternate path that circumvents the protection.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-424 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an alternate path (e.g. ftp://, alternate filesystem, or secondary API endpoint) bypasses access control.

## Detection & Test

1. Find alternate access methods (ftp, smb, second API, file://).
2. Access the protected resource via the alternate path bypassing the primary control.
3. Confirm the primary control is not enforced on the alternate path.
4. Probe file://, ftp://, and secondary endpoints for the same resource.

## Example Requests

```http
ftp://protected/file
```
```http
GET /api/secondary/file
```

## Bypass Tricks

- Use an alternate protocol (`file://`, `ftp://`) to reach the protected resource.
- Hit a secondary API endpoint (e.g., `/api/v2/`) that lacks the primary's authz.
- Access via a different hostname or virtual host that skips the control.
- Use a path alias or trailing-slash variant to bypass the check.


## Impact

- Access control bypassed through a secondary/alternate path.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).