
name: cwe-117-improper-output-neutralization-for-logs
description: Use when testing cwe-117 logging on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-117, logging, a09, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a09-logging-alerting-failures
---

# CWE-117 - Improper Output Neutralization for Logs (Log Injection)

CWE-117: the application writes untrusted input into a log without neutralizing special characters, so an attacker can inject fake log lines, headers, or markup into the log stream.

## Parent Skill

This is a sub-skill of `owasp-a09-logging-alerting-failures` (OWASP A09 Security Logging & Alerting Failures, Top 10 2025).
Load the parent for overall A09 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-117 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When user-supplied data (parameter, header, body) is written to a log without stripping or encoding newlines, CRLF, or log markup.

## Detection & Test

1. **Find the log sink.** Identify where user input is logged (a form field, a URL parameter, an HTTP header).
2. **Inject CRLF plus a fake line.** Send a value containing `%0d%0a` (CRLF) followed by a fake log entry.
3. **Confirm the fake line is honored.** Show the injected line appears as a separate log entry, not as part of the original value.
4. **Escalate.** Use the injected line to add a fake auth event, hide a real event, or add markup that alters log parsing.
5. **Document the sink, the payload, and proof.

## Example Findings

- A form field that logs the raw input, so `%0d%0a[2026-10-30 12:00:00] admin login` creates a fake log line.
- An HTTP header value that is logged verbatim, allowing a CRLF injection into the access log.

## Impact

- Log injection lets an attacker forge or hide entries, or add markup that alters parsing (CWE-117).
- Omission of security-relevant information removes the audit trail needed to detect or attribute an incident (CWE-221/223).
- Sensitive data in a log leaks credentials, tokens, or PII to anyone with file access (CWE-532).
- Insufficient logging means key events (auth failures, admin actions) are not detected in a timely manner (CWE-778).

## See Also

- `owasp-a09-logging-alerting-failures` - parent skill (A09 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).