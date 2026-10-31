
name: cwe-784-cookies-without-validation-in-a-security-decision
description: Use when testing cwe-784 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-784, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-784 - Cookies Without Validation in a Security Decision

CWE-784: a cookie is used in a security decision without validation, so a tampered or forged cookie changes the security outcome.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-784 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a cookie is used in a security decision without validation.

## Detection & Test

1. **Find the cookie in the security decision.** Identify where the app reads a cookie and uses it for authn or authz.
2. **Tamper the cookie.** Modify the cookie's value to a different one.
3. **Confirm the security decision is changed.** Show the tampered cookie leads to a different security outcome.
4. **Escalate.** Use the tampered cookie to bypass authn or escalate privileges.
5. **Document the cookie, the tamper, and the security decision.

## Example Findings

- A cookie that holds `isAdmin=true` that is not validated before a check.
- A session cookie that is not verified, so it can be reused after logout.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).