
name: cwe-96-static-code-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-96, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-96 - Static Code Injection

CWE-96: user input is included in a statically-loaded code file (JS, HTML, template) in a way that changes the code's behavior.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-96 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a static asset (JS file, HTML template) loads or references user-controlled content.

## Detection & Test

1. **Find the static sink.** Identify which static file includes user input (a template with `{{include user_input}}`, a JS file with `var x = user_input`).
2. **Inject a code directive.** Send a template directive or JS expression that changes the static file's behavior.
3. **Confirm behavior change.** Verify the static file now behaves differently (includes a new script, changes a variable).
4. **Document the file, payload, and proof.

## Example Findings

- A template with `{% include user_input %}` where input = `evil.html`.
- A JS config file with `var mode = user_input` where input = `admin`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).