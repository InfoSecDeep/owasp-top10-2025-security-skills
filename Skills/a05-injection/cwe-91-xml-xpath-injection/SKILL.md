
name: cwe-91-xml-xpath-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-91, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-91 - XML / XPath Injection

CWE-91: user input is concatenated into an XML or XPath query without proper escaping, allowing the attacker to alter the query structure.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-91 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Any parameter that reaches an XML parse or XPath query as part of the query string.

## Detection & Test

1. **Find the injection point.** Send `<`, `>`, `&`, `'`, `"`, `//`, and `::` into the parameter.
2. **Test XPath operators.** Send `//`, `text()`, `contains()`, and `or true()` to alter the XPath.
3. **Confirm data disclosure.** Show the injection returns nodes it shouldn't.
4. **Test XML entity injection.** If the XML parser supports DTD, test for XXE via `<!DOCTYPE`.
5. **Document the injection point, payload, and returned data.

## Example Findings

- `//user[@name='user_input']` where input = `' or //user[1] = 'x`.
- A SOAP body with `<user>admin' or '1'='1</user>`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).