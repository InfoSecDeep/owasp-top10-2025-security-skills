
name: cwe-16-configuration
description: Use when a general permissive misconfiguration is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-16, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-16 - Configuration (General)

CWE-16: Configuration - an application or system is configured with a wrong default or a permissive setting that weakens security.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-16 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a general, non-specific misconfiguration is suspected (wrong default, permissive setting).

## Detection & Test

1. Enumerate the application's default settings on a fresh install.
2. Check the default debug/console state.
3. Inspect the default CORS/CSRF settings.
4. Look for a default-open endpoint (e.g., `/metrics`).

## Example Requests

```http
GET /metrics (default-open)
```
```http
First run shows admin enabled
```

## Bypass Tricks

- Access a default-open metrics/console endpoint.
- Exploit a default admin account that wasn't renamed.
- Bypass a default CORS `*` policy.
- Use a default debug page.

## Impact

- A default setting that exposes data or privileges.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).