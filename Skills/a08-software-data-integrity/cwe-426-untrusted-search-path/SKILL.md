
name: cwe-426-untrusted-search-path
description: Use when testing cwe-426 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-426, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-426 - Untrusted Search Path

CWE-426: the application uses an untrusted search path (e.g., a system path, an include directory) to locate a resource, so a malicious resource on the path is loaded.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-426 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the application loads a resource via a search path that includes untrusted directories.

## Detection & Test

1. **Identify the search path.** Find where the app resolves a resource name (a library, a binary, an include file).
2. **Place a malicious resource on the path.** Create a file with the same name in a directory on the untrusted path.
3. **Confirm the malicious resource is loaded.** Show the app loads the untrusted file.
4. **Escalate.** Use the malicious resource to gain code execution or data access.
5. **Document the path, the file, and proof.

## Example Findings

- A system path that includes a user-writable directory, so a malicious `libfoo.so` is loaded.
- An include directory that the app scans, so a malicious file is found first.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).