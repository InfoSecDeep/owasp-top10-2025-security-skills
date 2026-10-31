
name: cwe-99-resource-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-99, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-99 - Resource Injection

CWE-99: user input selects a resource (file, database, template) that is outside the intended set, allowing the attacker to use an unintended resource.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-99 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter selects a file, database, template, or other resource by name without validating it's in the expected set.

## Detection & Test

1. **Find the resource selector.** Identify which parameter selects a resource (file name, DB name, template name).
2. **Test out-of-set resources.** Send a resource name that should not be valid (e.g. `db=internal_db`).
3. **Confirm the resource is used.** Verify the app uses the unintended resource (different data, different template).
4. **Document the parameter, payload, and proof.

## Example Findings

- `db=users` where valid values are `sales` and `marketing`, but `users` is also accepted.
- `template=admin` where valid values are `home` and `about`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).