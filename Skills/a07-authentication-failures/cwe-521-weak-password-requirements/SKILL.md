
name: cwe-521-weak-password-requirements
description: Use when a web auth flaw matches cwe-521.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-521, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-521 - Weak Password Requirements

CWE-521: the password requirements are weak (too short, no complexity, no uniqueness), allowing easy brute-force or guess attacks.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-521 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the password requirements (length, complexity, uniqueness) are weak.

## Detection & Test

1. **Map the requirements.** Identify the password length, complexity, and uniqueness rules.
2. **Test a weak password.** Use a short, simple password that meets the weak requirements.
3. **Confirm acceptance.** Show the password is accepted and can be used.
4. **Escalate.** Use the weak password to log in or brute-force.
5. **Document the requirements, the weak password, and proof.

## Example Findings

- A password policy that accepts 4 characters.
- A policy that requires no special characters or uppercase letters.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).