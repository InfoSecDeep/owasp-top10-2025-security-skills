
name: cwe-104-struts-2-validation
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-104, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-104 - Struts 2 Validation Deficiency

CWE-104 (A05 context): in Struts 2, the framework's input validation can be bypassed by OGNL expression injection in parameters or by sending the same parameter with different content types.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-104 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When testing a Struts 2 application where the action's input validation can be bypassed.

## Detection & Test

1. **Identify the Struts 2 action.** Find the `.action` URL or action mapping.
2. **Test OGNL injection.** Send `${7*7}` or `#{7*7}` into parameters to test if OGNL is evaluated.
3. **Test content-type bypass.** Send the same parameter as `application/x-www-form-urlencoded` and as `application/json`.
4. **Bypass validation.** If the JSON path is less validated, use it to send a payload that bypasses the form validation.
5. **Document the action, payload, and proof.

## Example Findings

- `?name=${7*7}` in a Struts 2 action evaluates OGNL and returns 49.
- A JSON body bypasses the Struts 2 form validation that a form-encoded body would trigger.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).