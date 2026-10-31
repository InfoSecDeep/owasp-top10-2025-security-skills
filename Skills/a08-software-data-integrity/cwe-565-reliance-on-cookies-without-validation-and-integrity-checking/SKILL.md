
name: cwe-565-reliance-on-cookies-without-validation-and-integrity-checking
description: Use when testing cwe-565 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-565, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-565 - Reliance on Cookies Without Validation and Integrity Checking

CWE-565: the application relies on a cookie for a security decision without validating its contents or integrity, so a tampered cookie changes the security outcome.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-565 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a cookie is used in a security decision without validation or integrity checking.

## Detection & Test

1. **Find the security-critical cookie.** Identify the cookie that holds a value used in a security decision (a role, a flag, a token).
2. **Tamper the cookie.** Modify the cookie's value to a different, untrusted one.
3. **Confirm the tampered cookie is accepted.** Show the app processes the tampered value without validation.
4. **Escalate.** Use the tampered cookie to reach a security decision.
5. **Document the cookie, the tamper, and proof.

## Example Findings

- A cookie that holds `role=user` that is not signed, so it can be set to `role=admin`.
- A token cookie that is base64-encoded but not MAC-verified, so the payload can be modified.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).