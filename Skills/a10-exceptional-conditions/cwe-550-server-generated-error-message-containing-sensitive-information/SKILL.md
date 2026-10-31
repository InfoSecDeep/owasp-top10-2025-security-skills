
name: cwe-550-server-generated-error-message-containing-sensitive-information
description: Use when testing cwe-550 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-550, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-550 - Server-Generated Error Message Containing Sensitive Information

CWE-550: a server-generated error message (a framework default, a library error) contains sensitive information (a path, a version, a stack trace) that discloses internals.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-550 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a server-generated error message (a framework 404, a library error) leaks sensitive information.

## Detection & Test

1. **Trigger the error.** Send a request that causes a framework or library error (a 404, a 500).
2. **Read the error message.** Look for file paths, class names, versions, or stack traces.
3. **Confirm the disclosure.** Verify the internals are present.
4. **Map the leak to a target.** Note the framework, version, or path revealed.
5. **Document the endpoint, the message, and the internal data.

## Example Findings

- A Tomcat 404 page that shows the full path and the Tomcat version.
- An Express default 500 page that shows the route, the stack, and the Node version.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).