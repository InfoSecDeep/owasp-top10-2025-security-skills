
name: cwe-522-insufficiently-protected-credentials
description: Use when a web design flaw matching cwe-522 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-522, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-522 - Insufficiently Protected Credentials

CWE-522: credentials are transmitted or stored without adequate protection (cleartext, reversibly encoded, or no integrity), exposing them to capture or reverse.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-522 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When credentials (passwords, tokens) are sent in cleartext or stored without protection.

## Detection & Test

1. **Find the credential path.** Identify how credentials are sent and stored.
2. **Check cleartext.** Confirm the credential is sent over http:// or in the URL/query.
3. **Check storage.** If stored, confirm it is plaintext or reversibly encoded.
4. **Confirm exposure.** Show the credential can be read.
5. **Document the credential, the gap, and the fix.

## Example Findings

- A password in the URL over http://.
- A stored password in reversibly-encoded cleartext.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).