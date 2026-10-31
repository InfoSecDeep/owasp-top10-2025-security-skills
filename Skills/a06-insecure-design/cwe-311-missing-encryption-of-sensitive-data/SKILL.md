
name: cwe-311-missing-encryption-of-sensitive-data
description: Use when a web design flaw matching cwe-311 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-311, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-311 - Missing Encryption of Sensitive Data

CWE-311: sensitive data is not encrypted at some mandatory point (storage, transmission, or both), exposing it to an attacker who can read it.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-311 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When sensitive data (passwords, PII, tokens) is stored or transmitted without encryption.

## Detection & Test

1. **Identify sensitive data.** Find fields like passwords, tokens, PII, or financial data.
2. **Check encryption at rest.** Query the database or read files; confirm the data is plaintext or reversibly encoded.
3. **Check encryption in transit.** Confirm the field is sent over HTTPS, not cleartext HTTP.
4. **Confirm exposure.** Show an attacker can read the data.
5. **Document the data, the gap, and the fix.

## Example Findings

- A stored API key in plaintext in a database column.
- A password transmitted in the URL over http://.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).