
name: cwe-94-code-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-94, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-94 - Code Injection

CWE-94: user input is treated as executable code (eval, template, dynamic language features), allowing the attacker to run arbitrary code.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-94 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Any parameter that is passed to `eval()`, a template engine, `new Function()`, or a dynamic code evaluator.

## Detection & Test

1. **Find the code sink.** Look for `eval()`, `new Function()`, template rendering, `exec()`, or `setTimeout(user_input)`.
2. **Inject a code expression.** Send `{{7*7}}`, `${7*7}`, `#{7*7}`, or a language-specific expression.
3. **Confirm execution.** Verify the expression evaluates (49 instead of the literal string).
4. **Escalate.** If confirmed, try to read environment variables, access the filesystem, or run a command.
5. **Document the sink, payload, and proof.

## Example Findings

- `{{7*7}}` in a Jinja2 template renders as 49.
- `#{7*7}` in a Thymeleaf template renders as 49.
- `new Function(user_input)()` where input = `return process.env`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).