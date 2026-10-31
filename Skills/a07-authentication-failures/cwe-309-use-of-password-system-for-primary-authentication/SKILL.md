
name: cwe-309-use-of-password-system-for-primary-authentication
description: Use when password primary auth is weak, reused, or sole.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-309, owasp, top10-2025, pentest]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-309 - Use of Password System for Primary Authentication

CWE-309: passwords are used as the primary authentication factor with insufficient strength, lifecycle, and isolation (shared with other systems), so password compromise equals full account takeover.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (A07 Authentication Failures, OWASP Top 10 2025). Load the parent for overall category scope, the shared test procedure, and validation criteria (negative control). This skill covers the CWE-309 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- Passwords are the sole/primary authentication factor; they are reused across systems, stored or tested weakly, and lack rate limiting and entropy.

## Detection & Test

1. Brute-force the login endpoint (absent lockout feeds CWE-307) against common/weak password lists.
2. Check for weak or absent password policy, no MFA, password reuse with a credential provider, and cached default credentials.
3. Search code/config for plaintext or hard-coded credentials feeding auth (hardcoded-credential-hunt style).

## Example Findings

- Common weak password pairs log in against /login and the admin panel.
- A credential reused with a third-party auth source yields full account access.

## Impact

- Full account takeover via password compromise (brute force, cracking, reuse).
- Horizontal escalation: reused passwords across systems open sibling accounts.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, test procedure, validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full CWE table, priority order).