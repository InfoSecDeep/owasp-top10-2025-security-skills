
name: cwe-20-improper-input-validation
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-20, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-20 - Improper Input Validation

CWE-20: Improper Input Validation - the app accepts input it should reject, allowing it to reach a sink (DB, shell, template, header) unneutralized.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-20 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Any parameter where input validation looks absent or inconsistent (different rules per field, per encoding).

## Detection & Test

1. **Map validation rules.** Send boundary values (empty, 1, 999, unicode, whitespace) to each field and note accepted/rejected.
2. **Compare encodings.** Test the same boundary URL-encoded, double-encoded, in a header, and in the body.
3. **Find the sink.** Identify where the input lands: SQL query, command, template, redirect, file path.
4. **Prove injection.** Mutate the input to change sink behavior (query, command, output) and show a difference.
5. **Confirm negative control.** Send a value that must be treated as a string; confirm no side effect.

## Example Findings

- A numeric `page` field accepts `page=1;DROP TABLE users`.
- An email field accepts `a@b.com
Set-Cookie: pwned=1`.
- A JSON array field accepts an object where a string is expected.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).