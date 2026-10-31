
name: cwe-95-eval-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-95, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-95 - Eval Injection

CWE-95: user input is passed to `eval()` or an equivalent dynamic code execution mechanism, allowing the attacker to run arbitrary code in the application's context.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-95 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter is explicitly passed to `eval()`, `Function()`, or a language's dynamic execution primitive.

## Detection & Test

1. **Find the eval sink.** Search for `eval(`, `new Function(`, `setTimeout(` with a string argument, or `atob()` followed by execution.
2. **Inject a code expression.** Send a JS expression that produces a known output (e.g. `1+1` or `typeof document`).
3. **Confirm execution.** Verify the expression evaluates in the app context.
4. **Escalate.** Read `document.cookie`, make an API call, or execute a command via `fetch`.
5. **Document the sink, payload, and proof.

## Example Findings

- `eval(user_input)` where input = `typeof document` returns `object`.
- `setTimeout(user_input, 1000)` where input = `alert(document.domain)`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).