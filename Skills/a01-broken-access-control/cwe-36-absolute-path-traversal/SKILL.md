
name: cwe-36-absolute-path-traversal
description: Use when a file param takes an absolute path to read files.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-36, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-36 - Absolute Path Traversal

CWE-36: Absolute Path Traversal - untrusted input is used to construct an absolute path (starting at the filesystem root), granting direct access to any file the server can read.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-36 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a parameter can be set to an absolute filesystem path (leading /) to read arbitrary files.

## Detection & Test

1. Find parameters that accept a full path or a filename, then test absolute paths (/etc/passwd).
2. Send control /tmp/ok vs. /etc/passwd; confirm different content / different HTTP status / file-name in error message.
3. Test absolute path with extension, with Windows style (C:\windows\...), and combined with filter bypasses (trailing chars, null bytes).
4. Probe whether absolute paths are accepted directly or only after bypassing a whitelist.

## Example Requests

```http
GET /download?file=/etc/passwd
```
```http
GET /file?f=C:\windows\system32\config\SAM
```
```http
GET /read?path=/etc/shadow
```

## Bypass Tricks

- Leading `/` or `\`: `/etc/passwd`, `\etc\passwd`.
- Windows drive letter: `C:\Windows\Win.ini`.
- UNC path: `\\\server\share\secret`.
- Bypass a leading-slash filter with `./` prefix: `./etc/passwd`.
- Use a backslash on Unix where the app splits on `/`.
- Wrap the absolute path in a relative prefix that resolves to root: `/./etc/passwd`.


## Impact

- Direct disclosure of any absolute path readable by the webserver (configs, source, secrets).

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).