
name: cwe-260-password-in-configuration-file
description: Use when a credential is plaintext in a config file.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-260, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-260 - Password in Configuration File

CWE-260: Password in Configuration File - the application stores a password in a configuration file without encryption, allowing it to be read by an untrusted actor.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-260 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a connection string or credential is stored in plaintext in a config file that can be read.

## Detection & Test

1. Fetch the config file (`web.config`, `application.properties`, `config.yaml`).
2. Look for `password=`, `pwd=`, `secret=` keys.
3. Confirm the value is plaintext (not encrypted).
4. Check a backup/old version of the config that is still accessible.

## Example Requests

```http
GET /application.properties (password=...)
```
```http
GET /config.yaml
```

## Bypass Tricks

- Read a `.bak`/`.old` config that holds the password.
- Exploit a directory listing that exposes the config.
- Use a `.git` leak to read the config history.
- Fetch the config via a misconfigured static-file route.

## Impact

- Recover plaintext credentials from the configuration file.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).