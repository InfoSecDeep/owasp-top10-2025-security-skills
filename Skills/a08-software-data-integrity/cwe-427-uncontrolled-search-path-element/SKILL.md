
name: cwe-427-uncontrolled-search-path-element
description: Use when testing cwe-427 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-427, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-427 - Uncontrolled Search Path Element

CWE-427: an element of a search path (a directory, a path component) is controllable by the attacker, so a malicious resource on the path is loaded.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-427 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a directory or path component in a search path is user-controllable.

## Detection & Test

1. **Identify the controllable path element.** Find where the app uses a user-supplied value in a path.
2. **Set the value to a malicious directory.** Use a path that points to a directory with a malicious resource.
3. **Confirm the malicious resource is loaded.** Show the app resolves the resource from the attacker's directory.
4. **Escalate.** Use the malicious resource to gain code execution or data access.
5. **Document the path, the value, and proof.

## Example Findings

- A `dir` parameter that sets the include directory, so a malicious file is loaded from `attacker_dir`.
- A `path` parameter that points to a user-controlled directory with a malicious library.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).