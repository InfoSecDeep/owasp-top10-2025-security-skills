
name: cwe-219-sensitive-file-webroot
description: Use when a webroot file (info.php/.bak) is reachable.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-219, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-219 - Sensitive File Stored Under Web Root

CWE-219: Sensitive File Stored Under Web Root - an attacker finds and retrieves a sensitive file located in a web-accessible directory.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-219 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a webroot contains a file (e.g. info.php, .bak, source) reachable via HTTP and disclosure leaks sensitive content.

## Detection & Test

1. Enumerate webroot for info.php, index.php.bak, .git, .env, *.bak, *.sql, debug pages.
2. Access known/debug paths (Test Procedure step 9); confirm 200 with sensitive content.
3. Check for source/backup files exposed by misconfiguration (directory listing, default docs).
4. Verify the web server serves raw source instead of executing it.

## Example Requests

```http
GET /info.php
```
```http
GET /index.php.bak
```
```http
GET /.git/HEAD
```
```http
GET /config.sql
```

## Bypass Tricks

- Fuzz common debug/info files: `info.php`, `index.php.bak`, `.git/`, `.env`, `web.config`, `server-status`.
- Use a backup-file wordlist (`*.bak`, `*.old`, `~`, `.swp`).
- Exploit `?` query to force raw source: `/file.php?x` on some misconfigured servers.
- Try without extension to reach the raw file: `/file`.
- Check for a `.git` leak to reconstruct the whole source.


## Impact

- Full disclosure of server source, configs, credentials, and backups exposed via HTTP.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).