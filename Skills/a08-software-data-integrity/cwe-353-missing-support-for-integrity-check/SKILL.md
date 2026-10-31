
name: cwe-353-missing-support-for-integrity-check
description: Use when testing cwe-353 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-353, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-353 - Missing Support for Integrity Check

CWE-353: an integrity check is not performed on data or a resource, so a tampered or corrupted value is processed without detection.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-353 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an integrity check (hash, checksum, signature) is missing on a resource or data.

## Detection & Test

1. **Find the resource that should be integrity-checked.** Identify the asset or data that should have a hash or signature.
2. **Tamper the resource.** Modify the resource or data.
3. **Confirm no integrity check is performed.** Show the tampered resource is accepted or processed.
4. **Escalate.** Use the tampered resource to reach a security decision.
5. **Document the resource, the tamper, and proof.

## Example Findings

- A script file that is not integrity-checked (no SRI hash) before the browser executes it.
- A file download that has no checksum or signature verification.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).