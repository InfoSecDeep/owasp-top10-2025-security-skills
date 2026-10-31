
name: cwe-379-insecure-temp-file-creation
description: Use when temp files are world-readable/writable, poisonable.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-379, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-379 - Creation of Temporary File with Insecure Permissions

CWE-379: Creation of Temporary File with Insecure Permissions - a temp file is created in an insecure location or with world-readable/writable permissions.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-379 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when temp files are created with world-readable/writable permissions allowing read or poisoning.

## Detection & Test

1. Locate temp files the app creates; inspect permissions.
2. Read a world-readable temp file (disclosure) or pre-write (poison).
3. Confirm the permissions allow an unprivileged actor to read or modify.
4. Check for usage on a shared/public path (e.g., webroot).

## Example Requests

```http
App writes /var/tmp/x to 666 -> attacker reads it
```

## Bypass Tricks

- Read a world-readable temp file directly via the webroot.
- Pre-write the temp file to poison the app's read.
- Create a symlink where the temp file will be placed.
- Check the temp dir's default umask on the host.


## Impact

- Read or corrupt data written into a permissive temp file.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).