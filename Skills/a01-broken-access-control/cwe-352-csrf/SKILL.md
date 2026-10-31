
name: cwe-352-csrf
description: Use when a state-changing action lacks CSRF protection.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-352, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-352 - Cross-Site Request Forgery (CSRF)

CWE-352: Cross-Site Request Forgery - a malicious site coerces an authenticated user's browser into sending a state-changing request that the server treats as authorized.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-352 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a state-changing action lacks CSRF protection (token, SameSite, Origin/Referer check).

## Detection & Test

1. Find state-changing endpoints: POST/PUT/DELETE on accounts, settings, payments.
2. Confirm absence of token/SameSite/Origin-Referer check (Test Procedure step 6).
3. Replay the change request from a foreign origin; verify it succeeds.
4. Verify the server-side protection really distinguishes origin.

## Example Requests

```http
<form action='/transfer' method=POST> (no token; replays as victim)
```

## Bypass Tricks

- Send the state-changing request from a `fetch` with `mode:'no-cors'`.
- Exploit a missing `Origin`/`Referer` check on `application/x-www-form-urlencoded`.
- Use a JSON CSRF on an endpoint that accepts `application/json` without a token.
- Craft a form on attacker.com that auto-submits to the target.
- Bypass a token that is only read from the cookie, not the body.
- Exploit a double-submit cookie pattern with an attacker-controllable value.


## Impact

- Unwanted state change performed in the victim's authenticated context.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).