
name: cwe-460-improper-cleanup-on-thrown-exception
description: Use when testing cwe-460 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-460, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-460 - Improper Cleanup on Thrown Exception

CWE-460: when an exception is thrown mid-operation, the application does not clean up resources (a file, a connection, a lock), leaving them in an inconsistent state.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-460 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an exception is thrown and the application does not clean up (a partial file, an open connection, a held lock).

## Detection & Test

1. **Find the operation.** Identify the multi-step operation (an upload, a transfer, a write).
2. **Trigger the exception mid-operation.** Send input that causes the failure between steps.
3. **Observe the state.** Confirm the partial state (a half-written file, an open connection).
4. **Confirm the incomplete cleanup.** Show the resource is not cleaned up and the state is inconsistent.
5. **Document the operation, the exception, and the leftover state.

## Example Findings

- A file upload that fails mid-write, leaving a partial file that a later request can read.
- A DB transaction that fails, leaving a partial row that a query can see.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).