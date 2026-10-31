
name: cwe-302-auth-bypass-assumed-immutable-data
description: Use when a web auth flaw matches cwe-302.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-302, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-302 - Authentication Bypass by Assumed-Immutable Data

CWE-302: a value that the app assumes is immutable (a session ID, user ID, or role) is modified by the attacker to bypass authentication.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-302 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a value assumed immutable (a session ID, user ID, or role) can be modified to bypass authn.

## Detection & Test

1. **Find the immutable value.** Identify a value the app treats as immutable (a session ID, user ID, or role).
2. **Modify the value.** Change the value to a different one.
3. **Confirm the bypass.** Show the app accepts the modified value.
4. **Escalate.** Use the modified value to reach a protected resource.
5. **Document the value, the modification, and proof.

## Example Findings

- A session ID that the app treats as immutable but the attacker modifies.
- A user ID field that is changed in a request to bypass a check.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).