
name: cwe-506-embedded-malicious-code
description: Use when testing cwe-506 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-506, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-506 - Embedded Malicious Code

CWE-506: the application embeds malicious code into a legitimate resource (a file, a page, a module), so the malicious code is executed when the resource is loaded.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-506 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When malicious code is embedded into a legitimate resource that the app loads.

## Detection & Test

1. **Identify the resource.** Find the file, page, or module where malicious code could be embedded.
2. **Embed the malicious code.** Inject a script, a handler, or a module into the resource.
3. **Confirm the code is executed.** Show the app loads the resource and executes the malicious code.
4. **Escalate.** Use the embedded code to achieve RCE, data access, or state change.
5. **Document the resource, the code, and proof.

## Example Findings

- A script tag injected into a trusted HTML file, so the malicious JS runs on page load.
- A module that is loaded at startup and contains a malicious handler.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).