
name: cwe-13-aspnet-password-in-config
description: Use when credentials are plaintext in web.config/app.config.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-13, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-13 - ASP.NET Misconfiguration - Password in Configuration File

CWE-13: ASP.NET Misconfiguration - Password in Configuration File - the application stores sensitive credentials in a plaintext configuration file.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-13 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when connection strings or passwords are stored in `web.config` or `app.config` and can be read.

## Detection & Test

1. Fetch `web.config` or `app.config` via the web root.
2. Look for connection strings with embedded passwords.
3. Check for a `web.config.bak` or `web.config.old` that is world-readable.
4. Confirm the password is plaintext (not encrypted).

## Example Requests

```http
GET /web.config
```
```http
GET /web.config.bak
```
```http
GET /app.config
```

## Bypass Tricks

- Fetch a backup file (`.bak`, `.old`) that holds plaintext passwords.
- Exploit a misconfigured IIS that serves `web.config` raw.
- Read the config from a directory listing.
- Use a `.git` leak to extract the config history.

## Impact

- Recover database/app credentials from the config file.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).