
name: cwe-86-invalid-chars-in-identifiers
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-86, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-86 - Injection of Code that Runs in an Unanticipated Context (Special Character in Identifier)

CWE-86: an identifier or code identifier accepts special characters it shouldn't, allowing injection into an unexpected context.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-86 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an identifier field (username, file name, order ID) accepts characters outside its expected alphabet.

## Detection & Test

1. **Map the expected alphabet.** Determine what characters the identifier should contain (alphanumeric, hex, UUID).
2. **Inject special characters.** Send quotes, backticks, `#`, `//`, `--`, and shell metacharacters.
3. **Confirm the context shift.** Show the identifier is interpreted in a new context (SQL, shell, template).
4. **Prove impact.** Use the special character to change behavior (comment out the rest of a query, execute code).
5. **Document the identifier, payload, and impact.

## Example Findings

- A `username` field accepts `admin'#`, altering a SQL query.
- A file name accepts `report.pdf;rm -rf /` in a shell context.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).