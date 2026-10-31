
name: cwe-61-unix-symbolic-link
description: Use when a file param dereferences a symlink to a target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-61, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-61 - UNIX Symbolic Link (Symlink)

CWE-61: UNIX Symbolic Link Exploitation - the application follows symlinks (created on the server or via upload) to reach files outside the intended directory.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-61 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a file/dir parameter can be manipulated to dereference a UNIX symlink and expose its target.

## Detection & Test

1. Check upload/download parameters and temp paths (/tmp, /var/tmp); place a symlink to a sensitive file where the app reads.
2. Confirm the server dereferences symlinks (most Linux do); test readlink-like disclosure in errors.
3. For time-gap bugs, link-then-move: point a symlink at /etc/passwd, then delete/rename to capture the resolved bytes.
4. Verify the resolved target's content differs from the unlinked file (proves dereferencing).

## Example Requests

```http
ln -s /etc/passwd tmp/leak
```
```http
GET /download?file=tmp/leak
```

## Bypass Tricks

- Create a symlink in an attacker-writable dir the app reads (`/tmp`, `/var/tmp`).
- TOCTOU: replace a file with a symlink between the app's check and its read.
- Symlink to a dotfile or out-of-webroot target the app's glob includes.
- Use `ln -s` to point a served filename at `/etc/passwd`.
- Dangling symlink with a predictable name to race a write.


## Impact

- Read arbitrary server files reachable via a symlink.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).