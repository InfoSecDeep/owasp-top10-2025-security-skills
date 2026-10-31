
name: cwe-65-windows-hard-link
description: Use when a Windows file param resolves a hard link target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-65, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-65 - Windows Hard Link

CWE-65: Windows Hard Link Exploitation - a hard link (multiple directory entries to the same inode) is used to access a file outside the intended directory scope on a Windows filesystem.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-65 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when the target is Windows and a file parameter can resolve a hard link to an unintended resource.

## Detection & Test

1. Assess file-upload/download handlers on Windows hosts; verify the filesystem supports hard links (NTFS, ReFS).
2. Create a hard link to a sensitive file inside an attacker-writable scope and request it via the parameter.
3. Confirm resolution: the returned content matches the linked (privileged) file.
4. Look for APIs that treat the path by name without verifying the intended scope.

## Example Requests

```http
mklink link.txt ..\..\..\Windows\System32\config\SAM
```
```http
GET /download?file=link.txt
```

## Bypass Tricks

- Create a hard link (`mklink /H`) to a privileged file within a writable scope.
- Exploit NTFS alternate data streams on a linked file.
- Link into `System32\config` or `\Windows\WinSxS`.
- Race a rename/move to win the inode.


## Impact

- Read privileged files on Windows via hard link dereferencing.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).