
name: cwe-636-not-failing-securely
description: Use when testing cwe-636 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-636, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-636 - Not Failing Securely

CWE-636: when an error occurs, the application fails open (allows the request) instead of failing closed (denies the request), so the security control is bypassed.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-636 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an error or failure causes the security control to allow the request (fail open) instead of deny it (fail closed).

## Detection & Test

1. **Identify the security control.** Find the authorization check, rate limit, signature check, or file validation that should enforce protection.
2. **Force the underlying failure.** Trigger the condition that makes the check fail (a missing upstream, a null token, a timeout).
3. **Observe the default action.** Confirm the default is to allow the request (fail open).
4. **Confirm the bypass.** Show the security control is bypassed and the action is permitted.
5. **Document the control, the failure, and the fail-open behavior.

## Example Findings

- An authorization check that calls a remote service; on timeout, the check defaults to allow.
- A signature verification that fails to parse the signature, so it defaults to valid.
- A file type check that fails to read the MIME, so it defaults to allowed.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).