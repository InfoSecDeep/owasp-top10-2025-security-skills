
name: cwe-312-cleartext-storage-in-memory
description: Use when a web design flaw matching cwe-312 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-312, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-312 - Cleartext Storage of Sensitive Information in Memory

CWE-312: sensitive data is stored in cleartext in memory (buffers, variables), where a memory dump, error, or crash can expose it.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-312 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When sensitive data (a key, token, or credential) is kept in cleartext memory.

## Detection & Test

1. **Identify the in-memory secret.** Look for credentials, keys, or tokens held in process memory.
2. **Trigger a dump.** Use a crash, error, or known memory-exposure mechanism to surface the in-memory data.
3. **Confirm the cleartext is sensitive.** Show the exposed value is a secret.
4. **Escalate.** Use the exposed in-memory secret.
5. **Document the secret, the exposure vector, and proof.

## Example Findings

- A password held in an unencrypted buffer that an attacker can read via a heap read.
- A session token echoed to a log after a partial decryption error.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).