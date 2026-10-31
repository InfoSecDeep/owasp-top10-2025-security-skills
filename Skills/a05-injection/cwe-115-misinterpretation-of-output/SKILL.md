
name: cwe-115-misinterpretation-of-output
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-115, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-115 - Misinterpretation of Output

CWE-115: the app produces output that is later misinterpreted by another component (parser, template, browser), causing an injection or logic error.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-115 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a component's output is consumed by another component without proper encoding or interpretation.

## Detection & Test

1. **Find the output boundary.** Identify where component A's output becomes component B's input.
2. **Inject at the boundary.** Send a value that component A outputs in a way that component B misinterprets.
3. **Confirm the misinterpretation.** Verify component B processes the value differently than intended.
4. **Document the boundary, payload, and proof.

## Example Findings

- A CSV export field containing `value,with,commas` that breaks the CSV parser on import.
- A JSON API that returns `text/html` with a `<script>` tag that the browser executes.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).