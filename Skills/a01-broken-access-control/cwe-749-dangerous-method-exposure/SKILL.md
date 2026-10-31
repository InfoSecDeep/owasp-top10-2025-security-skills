
name: cwe-749-dangerous-method-exposure
description: Use when a dangerous method/endpoint is attacker-callable.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-749, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-749 - Exposed Dangerous Method or Function

CWE-749: Exposed Dangerous Method or Function - an attacker can invoke a function/method/action designed for privileged use (admin/debug/console).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-749 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a dangerous internal method/endpoint is exposed and callable by an attacker.

## Detection & Test

1. Enumerate dangerous endpoints (admin/debug/console/tests).
2. Call a privileged method as an unprivileged actor.
3. Confirm the method is reachable from the web layer.
4. Check for enabled-but-unprotected debug or admin actions.

## Example Requests

```http
GET /console
```
```http
POST /tests/run
```
```http
GET /debug
```

## Bypass Tricks

- Call a privileged method directly as an unprivileged user.
- Enable a disabled debug/console endpoint.
- Invoke an internal test/admin route via its URL.
- Exploit an exposed REST method that maps to a privileged function.


## Impact

- Privileged function called by an unprivileged actor.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).