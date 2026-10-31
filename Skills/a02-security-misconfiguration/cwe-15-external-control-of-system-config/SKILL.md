
name: cwe-15-external-control-of-system-config
description: Use when user input changes a setting that is internal.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-15, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-15 - External Control of System or Configuration Setting

CWE-15: External Control of System or Configuration Setting - the application allows untrusted input to influence a configuration value (e.g., log level, debug flag, timezone).

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-15 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a user-controlled input changes a system or application setting that should be internal.

## Detection & Test

1. Find parameters that map to config keys (`debug=`, `verbose=`, `log_level=`).
2. Set the value to a privileged/verbose state.
3. Confirm the app honors the input and changes its behavior.
4. Check for a config endpoint that accepts a JSON/URL body.

## Example Requests

```http
GET /api/config?debug=true
```
```http
POST /config {"log_level":"TRACE"}
```

## Bypass Tricks

- Supply a `debug=1` flag that enables verbose mode.
- Use a header (`X-Debug-Mode`) the app checks but doesn't validate.
- Set a timezone/locale to trigger a verbose error.
- Exploit a config endpoint that accepts `?verbose=1`.

## Impact

- Information disclosure or weakened security from a user-tunable config.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).