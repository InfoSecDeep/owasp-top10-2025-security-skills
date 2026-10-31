
name: cwe-402-resource-wrong-sphere
description: Use when an internal resource leaks via IDOR/forced browse.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-402, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-402 - Resource Leak to New/Wrong Sphere

CWE-402: Exposure of Resource to New Sphere - an application exposes an internal resource to a new sphere (new attack surface), creating a bypass.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-402 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an internal resource leaks to a new sphere via a control (IDOR/forced browse) or a new entry point.

## Detection & Test

1. Identify internal resources reachable from a new entry point.
2. Access an internal resource that should be confined (Test Procedure steps 2, 4).
3. Confirm the resource is now reachable from outside its sphere.
4. Check new/ephemeral entry points that expose internal APIs.

## Example Requests

```http
GET /internal/api/whoami (reachable from web)
```

## Bypass Tricks

- Reach an internal API via a new public entry point.
- Expose a resource through a second, less-protected URL alias.
- Exploit a new feature endpoint that forwards to an internal service.


## Impact

- Internal resources disclosed to a new/external sphere.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).