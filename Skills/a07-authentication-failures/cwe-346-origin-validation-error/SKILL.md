
name: cwe-346-origin-validation-error
description: Use when a web auth flaw matches cwe-346.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-346, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-346 - Origin Validation Error

CWE-346: the origin of a request is not validated properly, so a request from a wrong origin is accepted.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-346 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the origin of a request (a header, a referrer, a host) is not validated.

## Detection & Test

1. **Find the origin check.** Identify where the app validates the origin (a header, a referrer, a host).
2. **Send a wrong origin.** Use a request from an untrusted origin.
3. **Confirm the origin is accepted.** Show the app accepts the wrong origin.
4. **Escalate.** Use the accepted origin to reach the resource.
5. **Document the origin, the wrong value, and proof.

## Example Findings

- A request from `http://attacker.com` that is accepted by a check that expects `http://trusted.com`.
- An origin header that is not validated.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).