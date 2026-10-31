
name: cwe-425-direct-request
description: Use when a resource is reachable by guessing its URL.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-425, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-425 - Direct Request (Forced Browsing)

CWE-425: Direct Request - an application allows direct access to a resource whose URL can be guessed or brute-forced (forced browsing), bypassing intended navigation.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-425 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a resource is directly accessible if its URL is guessed/brute-forced (forced browsing).

## Detection & Test

1. Enumerate admin/debug/swagger/actuator routes (Test Procedure step 4).
2. Compare with a random 404 path to rule out a catch-all.
3. Access the discovered route as a lower-privilege actor.
4. Confirm the route returns privileged data when accessed directly.

## Example Requests

```http
GET /admin
```
```http
GET /swagger-ui
```
```http
GET /actuator/env
```

## Bypass Tricks

- Brute-force/guess the admin route URL.
- Use a directory listing or sitemap to discover the resource.
- Access the route as a low-priv or unauthenticated user.
- Fuzz common paths: `/admin`, `/console`, `/swagger`, `/actuator`.


## Impact

- Privileged resource reachable by directly requesting its URL.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).