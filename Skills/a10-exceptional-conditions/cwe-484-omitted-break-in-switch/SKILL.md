
name: cwe-484-omitted-break-in-switch
description: Use when testing cwe-484 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-484, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-484 - Omitted Break in Switch

CWE-484: a switch statement omits a break, so the code falls through to the next case and performs an unintended action.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-484 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a switch statement omits a break, causing fall-through to the next case.

## Detection & Test

1. **Find the switch.** Identify the switch statement and its cases.
2. **Trigger the fall-through.** Send a value that matches a case without a break.
3. **Observe the fall-through.** Confirm the code executes the next case's actions.
4. **Confirm the unintended action.** Show the fall-through performs an action (a write, an escalation) not intended for the original value.
5. **Document the case, the value, and the unintended action.

## Example Findings

- A switch on `amount` where the small-amount case omits a break, so the large-amount fee is also applied.
- A switch on `role` where the user case omits a break, so the admin actions also run.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).