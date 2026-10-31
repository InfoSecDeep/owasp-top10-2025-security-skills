
name: cwe-532-insertion-of-sensitive-information-into-log-file
description: Use when testing cwe-532 logging on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-532, logging, a09, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a09-logging-alerting-failures
---

# CWE-532 - Insertion of Sensitive Information into Log File

CWE-532: the application writes sensitive data (a password, a token, a card number) into a log file, so anyone who can read the log can access the sensitive value.

## Parent Skill

This is a sub-skill of `owasp-a09-logging-alerting-failures` (OWASP A09 Security Logging & Alerting Failures, Top 10 2025).
Load the parent for overall A09 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-532 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the application writes sensitive data into a log file, so the log contains a password, token, card number, or PII.

## Detection & Test

1. **Find the sensitive data in the request.** Identify where a password, token, or card number is sent (a form field, a header, a JSON body).
2. **Trigger the log write.** Perform the action that generates a log entry.
3. **Read the log file.** Open the log file and search for the sensitive value.
4. **Confirm the value is present.** Show the sensitive data appears in the log.
5. **Document the log file, the value, and proof.

## Example Findings

- A log file that contains a password in plaintext: `[2026-10-30 12:00:00] login user=admin pass=secret123`.
- An access log that includes a Bearer token: `GET /api/data Authorization: Bearer eyJhbGci...`

## Impact

- Log injection lets an attacker forge or hide entries, or add markup that alters parsing (CWE-117).
- Omission of security-relevant information removes the audit trail needed to detect or attribute an incident (CWE-221/223).
- Sensitive data in a log leaks credentials, tokens, or PII to anyone with file access (CWE-532).
- Insufficient logging means key events (auth failures, admin actions) are not detected in a timely manner (CWE-778).

## See Also

- `owasp-a09-logging-alerting-failures` - parent skill (A09 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).