
name: cwe-1390-weak-authentication
description: Use when a web auth flaw matches cwe-1390.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1390, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-1390 - Weak Authentication

CWE-1390: authentication is weak in a general sense (a weak algorithm, a weak check, or a flawed flow), so the authn check is easily bypassed.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-1390 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the authentication is weak in a general sense (a weak algorithm, a weak check, a flawed flow).

## Detection & Test

1. **Identify the weakness.** Find the weak algorithm, check, or flow in the authentication.
2. **Exploit the weakness.** Use the flaw to bypass the authn.
3. **Confirm the bypass.** Show the resource is accessible.
4. **Escalate.** Use the bypass to reach a protected resource.
5. **Document the weakness, the exploit, and proof.

## Example Findings

- A password check that uses a weak hash.
- An authn flow that trusts a client-side value.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).