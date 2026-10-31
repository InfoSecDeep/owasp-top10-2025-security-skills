
name: cwe-209-error-message-containing-sensitive-information
description: Use when testing cwe-209 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-209, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-209 - Error Message Containing Sensitive Information

CWE-209: an error message contains sensitive information (a stack trace, a path, a version, a DB name) that an attacker can use to target the system.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-209 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an error response leaks internal details (a stack trace, a file path, a version, a DB name).

## Detection & Test

1. **Trigger the error.** Send a request that causes a 500, a 404 with details, or a framework error page.
2. **Read the error body.** Look for stack traces, file paths, class/DB names, or version numbers.
3. **Confirm the disclosure.** Verify the internal data is present and not just an error code.
4. **Map the leak to a target.** Note which component, version, or path the message reveals.
5. **Document the endpoint, the message, and the specific internal data.

## Example Findings

- A 500 page that shows a full PHP stack trace with file paths in `/var/www`.
- A 404 that reveals the framework name and version (Laravel, ASP.NET Core).

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).