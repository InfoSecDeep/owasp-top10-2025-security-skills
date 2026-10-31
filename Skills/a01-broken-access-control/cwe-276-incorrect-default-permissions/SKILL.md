
name: cwe-276-incorrect-default-permissions
description: Use when permissive defaults expose resources to low roles.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-276, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-276 - Incorrect Default Permissions

CWE-276: Incorrect Default Permissions - insecure/overly permissive default permissions are set on a file, directory, account, or resource.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-276 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when application defaults let an unprivileged actor access/modify resources because of overly permissive defaults.

## Detection & Test

1. Assess default user/account roles on first run (admin enabled, no first-time password reset required).
2. Check default file/dir permissions of the application and its data store.
3. Inspect whether shared/ephemeral resources (ephemeral admin accounts, temp dirs) inherit world access.
4. Enumerate default credentials or default-open resources on a fresh deployment.

## Example Requests

```http
First login gives admin by default
```
```http
GET /secret -> 200 on fresh install
```

## Bypass Tricks

- On a fresh install, log in and confirm the default role (often admin).
- Enumerate the default credentials from the product docs.
- Check a default-open port or debug endpoint enabled out of the box.
- Look for a default admin user with no forced password reset.


## Impact

- Privilege abuse on unmodified deployments; data tampering / account takeover.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).