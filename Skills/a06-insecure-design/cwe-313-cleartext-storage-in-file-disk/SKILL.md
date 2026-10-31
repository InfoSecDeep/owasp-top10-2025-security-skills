
name: cwe-313-cleartext-storage-in-file-disk
description: Use when a web design flaw matching cwe-313 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-313, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-313 - Cleartext Storage of Sensitive Information in a File or Disk on System Expected to Protect It

CWE-313: sensitive data is written to a file or disk in cleartext, even though the system should protect it, letting an attacker who reaches the disk read it.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-313 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When sensitive data is written to a file or disk without encryption.

## Detection & Test

1. **Find where sensitive data is persisted.** Check for config files, logs, caches, and temp files that might hold secrets.
2. **Read the file.** If it exists and is readable, confirm the data is cleartext.
3. **Confirm the disk protection.** Determine whether the system was supposed to protect the file (chmod, filesystem encryption, temp).
4. **Escalate.** Use the extracted secret.
5. **Document the file, data, and the protection that was missing.

## Example Findings

- A session token written to a world-readable temp file.
- A config file with an API key stored in cleartext.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).