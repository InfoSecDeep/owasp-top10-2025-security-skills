
name: cwe-256-unprotected-storage-of-credentials
description: Use when a web design flaw matching cwe-256 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-256, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-256 - Unprotected Storage of Credentials

CWE-256: credentials are stored without adequate protection (plaintext, weakly hashed, or in a location accessible to unprivileged actors).

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-256 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When stored credentials are reachable (passwords, tokens, API keys) without adequate protection.

## Detection & Test

1. **Locate credential storage.** Identify where credentials are persisted (config, DB, file, cookie, shared memory).
2. **Assess protection.** Check whether the credential is plaintext, weakly hashed, or accessible to an unprivileged context.
3. **Attempt extraction.** If unprotected, read the credential directly (config dump, DB export, file read).
4. **Escalate.** Use the extracted credential to reach a privileged system.
5. **Document the storage, what was found, and how to fix it.

## Example Findings

- A stored password `admin:password123` in a config file.
- A session token persisted in a shared memory cookie accessible to a subprocess.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).