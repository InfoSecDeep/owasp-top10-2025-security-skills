
name: cwe-917-expression-language-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-917, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-917 - Expression Language Injection

CWE-917: user input is evaluated as an Expression Language expression (JSP EL, JSTL, OGNL), allowing the attacker to execute code or read data through the EL engine.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-917 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter is passed to a JSP EL expression (`${...}`, `#{...}`), a JSTL tag, or an OGNL expression.

## Detection & Test

1. **Find the EL sink.** Look for `${...}` in JSP, `#{...}` in Spring, or OGNL expressions with user input.
2. **Inject an EL expression.** Send `${7*7}`, `#{7*7}`, or `OGNL: #{7*7}` into the parameter.
3. **Confirm evaluation.** Verify the expression evaluates (49 instead of the literal string).
4. **Escalate.** Use the EL to read environment variables, access the servlet context, or run a command.
5. **Document the EL type, payload, and proof.

## Example Findings

- `${7*7}` in a JSP EL expression evaluates to 49.
- `#{applicationScope['java.lang.Class'].forName('java.lang.Runtime')}` in a Spring EL expression.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).