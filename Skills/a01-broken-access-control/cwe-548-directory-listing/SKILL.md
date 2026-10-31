
name: cwe-548-directory-listing
description: Use when a directory listing reveals restricted files.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-548, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-548 - Exposure Through Directory Listing

CWE-548: Exposure of Information Through Directory Listing - a directory listing on the network exposes files/dirs the actor should not access.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-548 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a directory is listed, revealing restricted files.

## Detection & Test

1. Request directories lacking an index (/images/, /backup/).
2. Confirm 200 with an index listing file/dir names.
3. Check the listed resources for sensitive content.
4. Verify the web server has autoindexing enabled.

## Example Requests

```http
GET /backup/ -> listing of files
```

## Bypass Tricks

- Request a directory without an index file to trigger autoindex.
- Fuzz common dirs (`/backup/`, `/img/`, `/tmp/`).
- Use a trailing-slash path to force the listing.
- Exploit the listing to discover sensitive filenames.


## Impact

- Restricted files discovered via directory listing.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).