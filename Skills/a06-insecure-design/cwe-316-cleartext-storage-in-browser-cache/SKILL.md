
name: cwe-316-cleartext-storage-in-browser-cache
description: Use when a web design flaw matching cwe-316 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-316, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-316 - Cleartext Storage of Sensitive Information in a Browser Cache

CWE-316: sensitive data is stored in a browser cache without protection, letting an attacker who reaches the cache read it.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-316 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When sensitive data is cached in the browser without protection (missing Cache-Control headers on sensitive pages).

## Detection & Test

1. **Identify sensitive pages.** Find pages containing credentials, tokens, or PII.
2. **Check cache headers.** Confirm whether `Cache-Control: no-store` (and friends) is sent on those pages.
3. **Confirm the cache.** If the page is cacheable, read it from the browser cache or an HTTP cache.
4. **Escalate.** Use the cached sensitive data.
5. **Document the page, the header gap, and proof.

## Example Findings

- An account balance page cached without `no-store`, readable from browser history.
- A password reset response stored in the browser cache.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).