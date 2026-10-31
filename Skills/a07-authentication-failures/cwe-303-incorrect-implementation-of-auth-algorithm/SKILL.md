
name: cwe-303-incorrect-implementation-of-auth-algorithm
description: Use when a web auth flaw matches cwe-303.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-303, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-303 - Incorrect Implementation of Authentication Algorithm

CWE-303: the authentication algorithm is implemented incorrectly (a flawed hash, a missing step, or a broken check), so the authn check fails to protect the resource.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-303 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the authentication algorithm (a hash, a signature check, a comparison) is implemented incorrectly.

## Detection & Test

1. **Identify the algorithm.** Find the authn algorithm (a hash, a signature, a comparison).
2. **Check the implementation.** Look for missing steps, flawed hashing, or broken comparisons.
3. **Exploit the flaw.** Use the implementation flaw to bypass the check.
4. **Confirm the bypass.** Show the resource is accessible.
5. **Document the algorithm, the flaw, and proof.

## Example Findings

- A password hash that is stored as `md5(password)` without salt.
- A signature check that uses `==` instead of constant-time comparison.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).