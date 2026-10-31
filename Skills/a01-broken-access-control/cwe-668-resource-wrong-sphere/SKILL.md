
name: cwe-668-resource-wrong-sphere
description: Use when an internal resource is exposed to a new sphere.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-668, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-668 - Resource in Wrong Sphere

CWE-668: Exposure of Resource to Wrong Sphere - the application does not restrict access to a resource in its original sphere, exposing it via a new sphere (often an SSRF-like new entry point).

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-668 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an internal resource is not restricted and leaks to a new sphere via an untrusted entry point.

## Detection & Test

1. Find new entry points (fetch/import/export) that can reach internal resources.
2. Expose a resource from its original sphere via the new entry point.
3. Confirm the new entry point is untrusted/external.
4. Check outbound fetch parameters that resolve internal hosts.

## Example Requests

```http
GET /fetch?url=http://169.254.169.254/
```

## Bypass Tricks

- Use a new fetch/import endpoint to reach an internal-only resource.
- Point an SSRF-capable parameter at the internal host.
- Exploit an alias that exposes the resource to a new entry point.
- Use a second service that proxies to the original sphere.


## Impact

- Resource escaped its sphere via a new entry point.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).