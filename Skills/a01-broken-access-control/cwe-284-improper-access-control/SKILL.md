
name: cwe-284-improper-access-control
description: Use when authorization relies on a client/untrusted party.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-284, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-284 - Improper Access Control (General)

CWE-284: Improper Access Control - security decisions wrongly rely on a non-authoritative, non-trusted entity (typically the client) instead of the server's authority.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-284 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when authorization is enforced by the client or an untrusted party, or a general access-control bypass is suspected.

## Detection & Test

1. Find authorization decisions driven by client input (role flags, auth tokens from client).
2. Flip client-side controls (role, auth flags) and confirm the server authorizes based on them.
3. Test whether removing server-side checks changes the outcome.
4. Use the parent Test Procedure (steps 1-3) to demonstrate the bypass.

## Example Requests

```http
Role flag in POST: {"role":"admin"}
```
```http
Client-auth bypass to privileged page
```

## Bypass Tricks

- Flip a client-side `role`/`auth` flag and confirm the server trusts it.
- Remove or reorder an auth header to bypass a client-enforced check.
- Exploit a UI-only 'disabled' button by calling the endpoint directly.
- Use the browser dev tools to toggle a client-side permission.


## Impact

- Server trusts an untrusted entity for authorization decisions.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).