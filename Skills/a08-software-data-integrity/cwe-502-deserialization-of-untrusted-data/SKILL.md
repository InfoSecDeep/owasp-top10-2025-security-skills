
name: cwe-502-deserialization-of-untrusted-data
description: Use when testing cwe-502 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-502, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-502 - Deserialization of Untrusted Data

CWE-502: the application deserializes untrusted data (a serialized object, a binary blob, a JSON payload) without verifying its origin or integrity, so a malicious payload is executed or processed.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-502 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the application deserializes data from an untrusted source (a serialized object, a binary, a JSON payload).

## Detection & Test

1. **Find the deserialization sink.** Identify where the app deserializes data (a `unserialize`, a `pickle.loads`, a `JSON.parse`).
2. **Send a malicious payload.** Use a stack-appropriate gadget or a crafted serialized object.
3. **Confirm the payload is processed.** Show the deserialization succeeds and the malicious object is created.
4. **Escalate.** Use the deserialized object to achieve RCE, auth bypass, or data access.
5. **Document the sink, the payload, and proof.

## Example Findings

- A Java object that deserializes and invokes a gadget chain leading to RCE.
- A Python pickle that deserializes and executes arbitrary code.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).