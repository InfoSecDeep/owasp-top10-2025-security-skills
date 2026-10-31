
name: cwe-1174-aspnet-improper-model-validation
description: Use when model binding accepts input bypassing validation.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1174, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-1174 - ASP.NET Misconfiguration - Improper Model Validation

CWE-1174: ASP.NET Misconfiguration - Improper Model Validation - the ASP.NET model binding accepts input that bypasses the intended validation.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-1174 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an ASP.NET model binding accepts unexpected input that bypasses validation.

## Detection & Test

1. Send an unexpected field in the model binding (e.g., an extra property).
2. Confirm the app accepts the field and changes its behavior.
3. Check for a `Bind` attribute that allows all properties.
4. Exploit a mass-assignment to set a privileged property.

## Example Requests

```http
POST /api/user {"name":"x","isAdmin":true}
```
```http
ASP.NET model binding accepts extra field
```

## Bypass Tricks

- Send an extra property (`isAdmin=true`) that the model binding accepts.
- Exploit a `Bind` attribute that allows all properties.
- Use a nested model to set a privileged field.
- Bypass a `Required` attribute with an empty string.

## Impact

- Privilege escalation or data tampering via mass-assignment.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).