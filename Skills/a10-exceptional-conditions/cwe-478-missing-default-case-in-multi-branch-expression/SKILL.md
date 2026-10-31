
name: cwe-478-missing-default-case-in-multi-branch-expression
description: Use when testing cwe-478 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-478, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-478 - Missing Default Case in Multi-Branch Expression

CWE-478: a multi-branch expression (a switch, an if-else chain) has no default case, so an unexpected value falls through to an unsafe path.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-478 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a switch or if-else chain has no default case, so an unexpected value reaches an unsafe path.

## Detection & Test

1. **Find the multi-branch expression.** Identify the switch or if-else that branches on a value.
2. **Send an unexpected value.** Use a value not in the documented set.
3. **Observe the fall-through.** Confirm the value reaches the fall-through path.
4. **Confirm the unsafe behavior.** Show the fall-through path performs an unsafe action.
5. **Document the expression, the value, and the unsafe path.

## Example Findings

- A switch on `status` with no default, so an unknown status falls through to the grant path.
- An if-else on `role` with no default, so an unknown role is treated as admin.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).