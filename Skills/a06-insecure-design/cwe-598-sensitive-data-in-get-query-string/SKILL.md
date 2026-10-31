
name: cwe-598-sensitive-data-in-get-query-string
description: Use when a web design flaw matching cwe-598 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-598, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-598 - Sensitive Information in GET Request Query String

CWE-598: sensitive information is transmitted in a GET request query string (URL), exposing it to the browser history, referrer, proxy logs, and server logs.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-598 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When sensitive data (a password, token, PII) is sent in a GET query string instead of a POST body.

## Detection & Test

1. **Find sensitive GET requests.** Identify endpoints that put sensitive data in the URL.
2. **Confirm placement.** Verify the sensitive data is in the query string (not the body).
3. **Confirm exposure.** Show where it leaks (history, referrer, logs).
4. **Escalate.** If the data is a credential, capture it from a log or referrer.
5. **Document the endpoint, the data, and the leak path.

## Example Findings

- A password sent in `?password=secret` in a GET.
- A token in the URL that leaks to the referrer.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).