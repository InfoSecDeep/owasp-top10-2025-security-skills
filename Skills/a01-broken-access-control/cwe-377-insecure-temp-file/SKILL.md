
name: cwe-377-insecure-temp-file
description: Use when temp files use predictable names/locations.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-377, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-377 - Insecure Temporary File

CWE-377: Insecure Temporary File - an application uses a predictable, insecurely located temp file that a local attacker can access or corrupt.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-377 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when the app reads/writes temp files using predictable names or locations an attacker can access or poison.

## Detection & Test

1. Detect temp-file creation for uploads, exports, caching.
2. Guess/predict the temp filename or location (write-then-read or pre-create with same name).
3. Pre-create the temp file to intercept or read the app's write.
4. Confirm the temp path is predictable/under the webroot or world-writable.

## Example Requests

```http
Predictable path /tmp/app_<pid>.tmp
```
```http
Pre-create -> read next user's data
```

## Bypass Tricks

- Predict the temp filename (pid, fixed name) and pre-create it.
- Create a directory at the temp path to change the behavior.
- Symlink the temp path to a sensitive file (on Unix).
- Exploit a fixed temp path under the webroot.


## Impact

- Local disclosure/corruption of temp-file contents.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).