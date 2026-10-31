
name: cwe-221-information-loss-of-omission
description: Use when testing cwe-221 logging on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-221, logging, a09, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a09-logging-alerting-failures
---

# CWE-221 - Information Loss of Omission

CWE-221: the application omits information that should be preserved (logged, audited, or retained) because it is not considered important, so a security-relevant event is lost or forgotten.

## Parent Skill

This is a sub-skill of `owasp-a09-logging-alerting-failures` (OWASP A09 Security Logging & Alerting Failures, Top 10 2025).
Load the parent for overall A09 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-221 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a security-relevant event (a change, a deletion, an exception) is not logged or audited, so the information is lost.

## Detection & Test

1. **Find the omitted information.** Identify a security-relevant event that should be logged or audited (a config change, a data deletion).
2. **Trigger the event.** Perform the action that should generate a log entry.
3. **Confirm the omission.** Check that no log entry or audit trail is generated.
4. **Document the omission.** Show the security-relevant event was not captured.
5. **Record the impact.** Explain how the missing log entry reduces the ability to detect or respond to an incident.

## Example Findings

- A config change that is not logged, so an attacker can modify settings without leaving a trace.
- A data deletion that is not audited, so the original state cannot be recovered or verified.

## Impact

- Log injection lets an attacker forge or hide entries, or add markup that alters parsing (CWE-117).
- Omission of security-relevant information removes the audit trail needed to detect or attribute an incident (CWE-221/223).
- Sensitive data in a log leaks credentials, tokens, or PII to anyone with file access (CWE-532).
- Insufficient logging means key events (auth failures, admin actions) are not detected in a timely manner (CWE-778).

## See Also

- `owasp-a09-logging-alerting-failures` - parent skill (A09 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).