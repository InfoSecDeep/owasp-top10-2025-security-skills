
name: cwe-538-sensitive-info-external-file
description: Use when sensitive data lands in a file an actor can reach.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-538, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-538 - Sensitive Information in Externally-Accessible File

CWE-538: Insertion of Sensitive Information into Externally-Accessible File or Directory - sensitive data is stored in a file/zip that external parties can read (e.g., a downloadable archive).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-538 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when sensitive data is written to a file on disk that an external actor (web/FTP/network) can access.

## Detection & Test

1. Inspect downloads/exports/archives for sensitive content.
2. Retrieve a file/archive the attacker shouldn't access; check its contents.
3. Confirm the archive/file is externally reachable (web + FTP/network).
4. Verify permissions of the source and the archive.

## Example Requests

```http
GET /download/export.zip (contains credentials)
```

## Bypass Tricks

- Download the externally-accessible archive and inspect its contents.
- Exploit a writable temp/export file that lands in a public path.
- Read a log file written to a web-accessible location.
- Fuzz for a downloadable `.zip`/`.tar` that bundles secrets.


## Impact

- Sensitive data readable via an external-accessible file/archive.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).