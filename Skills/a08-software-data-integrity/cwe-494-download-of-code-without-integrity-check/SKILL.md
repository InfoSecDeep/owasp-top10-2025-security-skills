
name: cwe-494-download-of-code-without-integrity-check
description: Use when testing cwe-494 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-494, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-494 - Download of Code Without Integrity Check

CWE-494: code is downloaded from a remote source without an integrity check, so a malicious or tampered version of the code is executed.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-494 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When code (a script, a library, a binary) is downloaded and executed without a hash, signature, or integrity check.

## Detection & Test

1. **Find the code download.** Identify where the app loads code from a remote source.
2. **Check for an integrity check.** Confirm there is no hash, signature, or version check.
3. **Replace the code with a malicious version.** Serve a tampered version of the code.
4. **Confirm the malicious code is executed.** Show the app runs the malicious code.
5. **Document the download, the missing check, and proof.

## Example Findings

- A script loaded from a CDN without an SRI hash, so a tampered script is executed.
- A plugin that is downloaded from a URL without a signature check.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).