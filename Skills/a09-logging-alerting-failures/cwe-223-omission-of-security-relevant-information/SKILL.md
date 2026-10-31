
name: cwe-223-omission-of-security-relevant-information
description: Use when testing cwe-223 logging on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-223, logging, a09, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a09-logging-alerting-failures
---

# CWE-223 - Omission of Security-Relevant Information

CWE-223: the application omits security-relevant information from a log, report, or response, so a security event or state is not visible to the analyst or user.

## Parent Skill

This is a sub-skill of `owasp-a09-logging-alerting-failures` (OWASP A09 Security Logging & Alerting Failures, Top 10 2025).
Load the parent for overall A09 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-223 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a log, report, or response is missing security-relevant information (a timestamp, a user ID, an error code).

## Detection & Test

1. **Identify the missing information.** Find where a log entry or response should contain a security-relevant field (a timestamp, a user, an event type).
2. **Trigger the event.** Perform the action that should generate the field.
3. **Confirm the field is absent.** Show the log entry or response does not include the field.
4. **Document the omission.** Show the security-relevant information is missing.
5. **Record the impact.** Explain how the missing field reduces the ability to detect or respond to an incident.

## Example Findings

- A log entry that records the event but not the user who triggered it, so the event cannot be attributed.
- An error response that omits the error code, so the type of failure is not known.

## Impact

- Log injection lets an attacker forge or hide entries, or add markup that alters parsing (CWE-117).
- Omission of security-relevant information removes the audit trail needed to detect or attribute an incident (CWE-221/223).
- Sensitive data in a log leaks credentials, tokens, or PII to anyone with file access (CWE-532).
- Insufficient logging means key events (auth failures, admin actions) are not detected in a timely manner (CWE-778).

## See Also

- `owasp-a09-logging-alerting-failures` - parent skill (A09 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).