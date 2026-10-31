
name: cwe-282-improper-ownership-management
description: Use when a file's ownership is mismanaged, granting control.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-282, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-282 - Improper Ownership Management

CWE-282: Improper Ownership Management - ownership of a resource is set improperly or not validated, so an attacker can gain control.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-282 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an application mismanages file/ownership metadata, letting an actor gain ownership/control of a resource.

## Detection & Test

1. Inspect upload/import paths that accept or rewrite ownership (owner, owner_id, ownership).
2. Set ownership of a downloaded/moved file to a privileged owner/role and re-serve it.
3. Confirm the app trusts user-supplied ownership without validating it.
4. Check for chown-style behavior on user-controlled targets.

## Example Requests

```http
POST /import {file, owner:admin_id}
```
```http
GET /file -> ownership now admin
```

## Bypass Tricks

- Supply an `owner` field pointing at a privileged account on upload/import.
- Rename or chown the backing file and re-request it as the new owner.
- Exploit a 'share to user' action that trusts a user-supplied owner id.


## Impact

- Unauthorized control/ownership of files, accounts, or resources.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).