
name: cwe-778-insufficient-logging
description: Use when testing cwe-778 logging on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-778, logging, a09, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a09-logging-alerting-failures
---

# CWE-778 - Insufficient Logging

CWE-778: the application does not log enough security-relevant events, so an incident is not detected or responded to in a timely manner.

## Parent Skill

This is a sub-skill of `owasp-a09-logging-alerting-failures` (OWASP A09 Security Logging & Alerting Failures, Top 10 2025).
Load the parent for overall A09 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-778 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the application does not log enough security-relevant events (auth failures, admin actions, config changes).

## Detection & Test

1. **Identify the missing log events.** Find the security-relevant events that should be logged (auth failures, admin actions, config changes).
2. **Trigger each event.** Perform each action that should generate a log entry.
3. **Check the log for each event.** Open the log and search for the event.
4. **Confirm the missing events.** Show that no log entry was generated for the triggered events.
5. **Document the missing events, the evidence, and the impact on incident detection.

## Example Findings

- A failed login that is not logged, so a brute-force attack is not detected.
- An admin action that is not logged, so a privilege escalation is not detected.
- A config change that is not logged, so a backdoor is not detected.

## Impact

- Log injection lets an attacker forge or hide entries, or add markup that alters parsing (CWE-117).
- Omission of security-relevant information removes the audit trail needed to detect or attribute an incident (CWE-221/223).
- Sensitive data in a log leaks credentials, tokens, or PII to anyone with file access (CWE-532).
- Insufficient logging means key events (auth failures, admin actions) are not detected in a timely manner (CWE-778).

## See Also

- `owasp-a09-logging-alerting-failures` - parent skill (A09 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).