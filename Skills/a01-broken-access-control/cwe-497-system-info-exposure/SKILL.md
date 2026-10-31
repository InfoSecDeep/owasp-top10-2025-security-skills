
name: cwe-497-system-info-exposure
description: Use when an app leaks OS/version/network details in output.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-497, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-497 - Exposure of Sensitive System Information

CWE-497: Exposure of Sensitive System Information - OS, network configuration, or software version info is exposed via headers, error messages, or logs, aiding further attacks.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-497 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an app leaks OS/version/network/system details in headers, banners, or error messages.

## Detection & Test

1. Inspect HTTP headers and Server banner for OS/version.
2. Trigger errors that leak network config, IPs, version.
3. Log the response to see if system info is exposed.
4. Enumerate info that narrows the target for a follow-up attack.

## Example Requests

```http
GET / (Server: Apache/2.4.7 (Ubuntu))
```
```http
GET /error -> OS/version in body
```

## Bypass Tricks

- Read the `Server` header for OS/version.
- Trigger a 500 to leak a stack trace with paths/versions.
- Inspect verbose error banners for network config.
- Use the exposed version to look up known CVEs.


## Impact

- Fingerprinting that enables targeted follow-up attacks.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).