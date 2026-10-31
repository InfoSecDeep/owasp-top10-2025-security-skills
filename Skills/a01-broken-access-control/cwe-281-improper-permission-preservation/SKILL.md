
name: cwe-281-improper-permission-preservation
description: Use when a move/rename drops permissions, exposing a file.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-281, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-281 - Improper Preservation of Permissions

CWE-281: Improper Preservation of Permissions - operations (move/copy) drop or fail to propagate permissions that protect a resource.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-281 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when moving/renaming files loses security-critical permissions, letting a privileged resource become accessible.

## Detection & Test

1. Identify file move/copy/rename operations into untrusted or public scopes.
2. Confirm a moved privileged file's permissions are reset to world-accessible.
3. Reproduce: a copy of a protected file becomes accessible via the public path.
4. Check whether permission bits propagate across boundaries (mount points, app->public).

## Example Requests

```http
POST /move {src:'/secure/x', dst:'/public/x'} -> public access returns file
```

## Bypass Tricks

- Move a privileged file into a public dir and request it; confirm perms were not carried.
- Copy (not move) to test whether the copy inherits the source ACL.
- Move across mount points/filesystems where ACLs reset to the target's default.


## Impact

- A privileged resource becomes publicly readable after a move/copy operation.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).