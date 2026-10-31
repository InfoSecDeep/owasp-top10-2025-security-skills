
name: cwe-830-web-functionality-from-an-untrusted-source
description: Use when testing cwe-830 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-830, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-830 - Web Functionality from an Untrusted Source

CWE-830: the application loads web functionality (a script, a widget, a component) from an untrusted source without validation, so the untrusted functionality affects the app's security.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-830 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When web functionality (a script, a widget) is loaded from an untrusted source without validation.

## Detection & Test

1. **Find the untrusted web functionality.** Identify where the app loads a script, widget, or component from an external source.
2. **Check the validation.** Confirm there is no SRI, origin check, or allowlist.
3. **Replace the functionality with a malicious version.** Serve a malicious version of the script or component.
4. **Confirm the malicious functionality is executed.** Show the app loads and executes the malicious code.
5. **Document the source, the missing check, and proof.

## Example Findings

- A script loaded from `https://cdn.trusted.com` without an SRI hash, so a tampered script is executed.
- A widget that is loaded from an untrusted URL without an origin check.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).