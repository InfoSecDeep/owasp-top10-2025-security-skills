
name: cwe-926-improper-export-of-android-application-components
description: Use when testing cwe-926 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-926, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-926 - Improper Export of Android Application Components

CWE-926: an Android application component (Activity, Service, BroadcastReceiver, ContentProvider) is exported without proper access control, so a malicious app can interact with it.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-926 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an Android component is exported (accessible from other apps) without proper access control.

## Detection & Test

1. **Find the exported component.** Identify the Activity, Service, BroadcastReceiver, or ContentProvider that is exported in the AndroidManifest.
2. **Check the access control.** Confirm there is no permission, intent filter, or data restriction.
3. **Interact with the component from a malicious app.** Send an intent or query the component.
4. **Confirm the component is accessible.** Show the malicious app can invoke or read the component.
5. **Document the component, the export, and proof.

## Example Findings

- An exported Activity that shows the user's PII and is accessible from any app.
- A ContentProvider that exports the user's database and has no permission check.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).