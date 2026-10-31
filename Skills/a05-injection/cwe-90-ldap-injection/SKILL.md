
name: cwe-90-ldap-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-90, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-90 - LDAP Injection

CWE-90: user input is concatenated into an LDAP query without proper filtering, allowing the attacker to alter the query structure.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-90 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Any parameter that reaches an LDAP search or bind as part of the query string.

## Detection & Test

1. **Find the injection point.** Send `*`, `(`, `)`, `&`, `|`, `\`, and `&` into the parameter.
2. **Test wildcard injection.** Send `*` to see if it matches all entries (e.g. `cn=*` returns all users).
3. **Test filter injection.** Send `)(objectClass=*)` or `(&(objectClass=*)(...))` to alter the filter.
4. **Confirm data disclosure.** Show the injection returns more or different entries than a neutral query.
5. **Document the injection point, payload, and returned data.

## Example Findings

- `cn=john*)(objectClass=*)` returns all users.
- `mail=*(uid=admin)` in a login form bypasses the password check.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).