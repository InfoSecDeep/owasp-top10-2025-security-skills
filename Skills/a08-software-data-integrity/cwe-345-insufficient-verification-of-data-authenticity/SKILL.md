
name: cwe-345-insufficient-verification-of-data-authenticity
description: Use when testing cwe-345 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-345, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-345 - Insufficient Verification of Data Authenticity

CWE-345: the application accepts data from an untrusted source without verifying its authenticity, so a malicious or tampered value is trusted.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-345 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the application accepts data without checking its authenticity.

## Detection & Test

1. **Find the unvalidated data source.** Identify where the app accepts data (cookie, header, parameter) without authenticity verification.
2. **Send a tampered value.** Modify the value to a different, untrusted one.
3. **Confirm the tampered value is accepted.** Show the app processes the value without verification.
4. **Escalate.** Use the tampered value to reach a security decision.
5. **Document the data, the tamper, and proof.

## Example Findings

- A cookie that holds a role value that is not signed or validated.
- A parameter that accepts a user ID that is not verified against the session.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).