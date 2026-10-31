
name: cwe-552-files-external-accessible
description: Use when public-reachable files hold out-of-scope data.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-552, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-552 - Files or Directories Accessible to External Parties

CWE-552: Files or Directories Always Accessible to External Parties - files/dirs meant to be private remain accessible to untrusted parties (web-accessible data, configs, sessions).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-552 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when files/dirs a public actor can reach hold data beyond that actor's scope.

## Detection & Test

1. Locate data files/dirs (config, sessions, backups) reachable via HTTP.
2. Access one expected to be private; confirm 200 with content.
3. Verify the directory listing exposes private files.
4. Check the web root for misplaced data/config/session files.

## Example Requests

```http
GET /data/sessions/ (leaks session data)
```

## Bypass Tricks

- Access a session/config file directly via its web path.
- Use a directory listing to enumerate the private files.
- Read a misplaced data file under the webroot.
- Exploit a static-file route that serves a private directory.


## Impact

- Private data accessible to an external actor.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).