
name: cwe-829-functionality-from-untrusted-control-sphere
description: Use when testing cwe-829 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-829, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-829 - Functionality From an Untrusted Control Sphere

CWE-829: the application relies on functionality from an untrusted control sphere (a third-party module, an external service) without proper validation, so the untrusted functionality affects the app's security.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-829 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the application uses functionality from an untrusted source (a third-party module, an external service).

## Detection & Test

1. **Find the untrusted functionality.** Identify where the app loads or calls a function from an untrusted source.
2. **Check the validation.** Confirm there is no integrity check, signature, or allowlist for the untrusted functionality.
3. **Replace the functionality with a malicious version.** Serve a malicious version of the untrusted function.
4. **Confirm the malicious functionality is used.** Show the app calls the malicious function.
5. **Document the functionality, the source, and proof.

## Example Findings

- A third-party script that is loaded without SRI and can be replaced with a malicious version.
- An external API that is called without a signature check on the response.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).