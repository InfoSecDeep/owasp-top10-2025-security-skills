
name: cwe-525-sensitive-data-in-browser-cache
description: Use when a web design flaw matching cwe-525 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-525, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-525 - Sensitive Information in Browser Cache Not Protected

CWE-525: sensitive information is stored in a browser cache that is not adequately protected (missing `no-store`), letting an attacker who reaches the cache read it.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-525 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When sensitive data is cached in the browser without `no-store` protection.

## Detection & Test

1. **Identify sensitive responses.** Find responses with credentials, tokens, or PII.
2. **Check Cache-Control.** Confirm whether `no-store` and related headers are present.
3. **Confirm the cache.** If cacheable, retrieve the response from the browser cache.
4. **Escalate.** Use the cached sensitive data.
5. **Document the response, the header gap, and proof.

## Example Findings

- A profile page with PII cached without `no-store`.
- A token returned in a response that the browser caches.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).