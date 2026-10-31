
name: cwe-293-auth-bypass-referer-field
description: Use when a web auth flaw matches cwe-293.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-293, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-293 - Using Referer Field for Authentication

CWE-293: authentication relies on the Referer HTTP header, which the attacker can set to any value, bypassing the check.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-293 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the authentication decision is based on the Referer header.

## Detection & Test

1. **Find the Referer-based check.** Identify where the app reads the Referer header for authn.
2. **Set a trusted Referer.** Send the request with `Referer: http://trusted.com`.
3. **Confirm the bypass.** Show the app trusts the Referer and grants access.
4. **Escalate.** Use the spoofed Referer to reach the resource.
5. **Document the Referer value, the check, and proof.

## Example Findings

- A login form that only accepts requests from `http://internal.com` in the Referer.
- An API that checks `Referer` before processing a request.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).