
name: cwe-493-public-method-without-final
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-493, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-493 / CWE-500 - Public Method/Variable Without Final Keyword

CWE-493/500: a public method or variable that should be immutable is not marked `final` (or equivalent), allowing a subclass or other code to override or modify it.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-493 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a public API method or variable is not marked `final` and a subclass or external code can override or modify it.

## Detection & Test

1. **Find the public API.** Identify which public methods or variables are not marked `final`.
2. **Create a subclass.** In the same language/framework, create a subclass that overrides the method or modifies the variable.
3. **Confirm the modification.** Verify the subclass's version is used instead of the parent's.
4. **Document the method/variable, subclass, and proof.

## Example Findings

- A public `getConfig()` method that is not `final`, allowing a subclass to return a different config.
- A public `MAX_RETRIES` variable that is not `final`, allowing a subclass to set it to 0.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).