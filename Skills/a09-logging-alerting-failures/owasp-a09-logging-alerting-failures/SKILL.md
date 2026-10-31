
name: owasp-a09-logging-alerting-failures
description: Use when testing A09 Logging/Alerting Failures on web.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [owasp, top10-2025, a09, logging, cwe, pentest]
category: pentesting-skills
related_skills:
  - owasp-top10-2025-testing
---

# A09 - Security Logging & Alerting Failures

OWASP Top 10 2025 category A09 (retained from 2021; renamed to emphasize alerting). Covers log injection, sensitive data in logs, and insufficient logging/alerting of security events. The parent skill `owasp-top10-2025-testing` holds scope, reporting, and the full CWE reference.

## When to Use
- When you need to assess whether security events are logged, whether logs can be injected or dumped, or whether alerting is wired to the events that matter.

## Mapped CWEs (5)

- CWE-117: Improper output neutralization for logs (log injection)
- CWE-221: Information loss of omission
- CWE-223: Omission of security-relevant information
- CWE-532: Insertion of sensitive information into log file
- CWE-778: Insufficient logging

## Test Procedure

1. **Log injection.** Inject CRLF plus a fake log line in parameters and headers; look for the honored line in a later response, error page, or exposed log surface (CWE-117).
2. **Log exposure.** Probe /logs, /log/, /var/log/*, /actuator/logfile, /audit, /access.log. Any 200 with structured entries is a finding; then mine it for credentials and paths (CWE-532).
3. **Sensitive data in errors.** Trigger errors with tokens or passwords in the request; check error bodies and log dumps for raw values (CWE-532).
4. **Coverage check.** For each key event - authentication failure, authorization failure, failed file upload, admin action, deserialization attempt, rate-limit trip - trigger it within scope. No observable logging or alerting indicates a CWE-778 gap; if you cannot see logs directly, label the finding as likely and cite the evidence you did see.
5. **Log tampering.** If logs are exposed over HTTP, test for read/write/delete access on log entries.

## Validation / Negative Control

- Log injection proven by the injected line appearing outside the original request data (the newline was honored, not just echoed).
- Sensitive-log findings require the actual leaked value, not just an accessible 403-protected path.

## See Also

- `owasp-top10-2025-testing` - parent skill (scope, reporting, full CWE reference).

## CWE Sub-Skills

Each mapped CWE has a dedicated sub-skill with focused detection steps, example findings, and expected impact. Load the relevant sub-skill via `skill_view(name)` when a finding or test case matches one of these.

| CWE | Sub-skill |
|---|---|
| CWE-117 | `cwe-117-improper-output-neutralization-for-logs` |
| CWE-221 | `cwe-221-information-loss-of-omission` |
| CWE-223 | `cwe-223-omission-of-security-relevant-information` |
| CWE-532 | `cwe-532-insertion-of-sensitive-information-into-log-file` |
| CWE-778 | `cwe-778-insufficient-logging` |