
name: cwe-539-sensitive-data-in-persistent-cookies
description: Use when a web design flaw matching cwe-539 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-539, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-539 - Sensitive Information in Persistent Cookie

CWE-539: a cookie that persists on the client (persistent, not session) stores sensitive information, letting an attacker who reaches the client read it.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-539 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a persistent cookie stores sensitive data (a token, profile, or credential).

## Detection & Test

1. **Identify persistent cookies.** Look for cookies with a long expiry set on the client.
2. **Check contents.** Confirm the persistent cookie holds sensitive data.
3. **Confirm client reachability.** Show the cookie value is readable from the client (storage, disk).
4. **Escalate.** Use the extracted cookie value.
5. **Document the cookie, the data, and the proof.

## Example Findings

- A persistent cookie containing a session token readable from the browser's cookie store.
- A `remember-me` cookie with a user ID or token.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).