
name: cwe-476-null-pointer-dereference
description: Use when testing cwe-476 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-476, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-476 - NULL Pointer Dereference

CWE-476: the application dereferences a null pointer, causing a crash or an unsafe read.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-476 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a null pointer (a null object, a missing field) is dereferenced, causing a crash or an unsafe read.

## Detection & Test

1. **Find the dereference.** Identify where the app uses an object that can be null.
2. **Make it null.** Send input that omits the field, causing the null.
3. **Observe the crash or read.** Confirm the app crashes or reads an unsafe value.
4. **Confirm the impact.** Show the dereference leads to a crash, a disclosure, or a state change.
5. **Document the object, the input, and the outcome.

## Example Findings

- A null `user` object that is dereferenced to read `user.balance`, causing a crash.
- A missing `session` field that is dereferenced, causing a null-reference error with a stack trace.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).