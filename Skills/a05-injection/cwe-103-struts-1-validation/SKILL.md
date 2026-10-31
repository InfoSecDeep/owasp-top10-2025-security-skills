
name: cwe-103-struts-1-validation
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-103, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-103 - Struts 1 Validation Deficiency

CWE-103 (A05 context): in Struts 1, the framework's input validation can be bypassed by sending the same parameter in both the body and the query string, or by using a different content type than expected.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-103 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When testing a Struts 1 application where the action's input validation can be bypassed by inconsistent HTTP request interpretation.

## Detection & Test

1. **Identify the Struts 1 action.** Find the `.do` URL or action mapping.
2. **Send the parameter twice.** Put the parameter in both the query string and the POST body.
3. **Observe the discrepancy.** Check if the action uses the query-string value instead of the body value.
4. **Bypass validation.** If the body value is validated but the query-string value is used, send a valid body value and an invalid query-string value.
5. **Document the action, parameters, and proof.

## Example Findings

- `GET /login.do?user=admin` + `POST user=guest` where the action uses the query-string `user=admin`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).