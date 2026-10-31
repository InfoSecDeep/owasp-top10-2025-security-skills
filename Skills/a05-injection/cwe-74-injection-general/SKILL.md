
name: cwe-74-injection-general
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-74, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-74 - Improper Neutralization of Special Elements in Output (Injection, General)

CWE-74: Improper Neutralization of Special Elements used in an Output - untrusted data reaches a parser/interpreter (SQL, shell, template) with special characters active.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-74 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- General injection where the sink is not a specific named type (SQL, shell, LDAP, XPath, etc.).

## Detection & Test

1. **Identify the sink type.** Determine whether the input is interpreted by a database, shell, template engine, or other parser.
2. **Inject a marker.** Insert a value that changes parser behavior (a quote, a comment, a special character).
3. **Observe the difference.** Compare responses to a neutral value and the injected value.
4. **Confirm data or code execution.** Prove the injection changes data returned or code executed.
5. **Document the sink and payload.** Record the exact parameter, payload, and response diff.

## Example Findings

- A `name` field injects a `--` SQL comment.
- A template variable evaluates `{{7*7}}` as 49.
- A config value containing `;` executes a shell command.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).