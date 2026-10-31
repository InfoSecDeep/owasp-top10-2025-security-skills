
name: cwe-305-auth-bypass-by-primary-weakness
description: Use when a web auth flaw matches cwe-305.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-305, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-305 - Authentication Bypass by Primary Weakness

CWE-305: authentication is bypassed by exploiting a primary weakness in the authn system (a primary credential that is weak, a primary check that is flawed).

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-305 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the primary authentication mechanism (the main credential or check) has a flaw that allows bypass.

## Detection & Test

1. **Identify the primary weakness.** Find the main credential or check that is flawed.
2. **Exploit the weakness.** Use the flaw to bypass the primary authn.
3. **Confirm the bypass.** Show the resource is accessible.
4. **Escalate.** Use the bypass to reach a protected resource.
5. **Document the weakness, the exploit, and proof.

## Example Findings

- A primary password that is weak or hard-coded.
- A primary check that trusts a client-side value.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).