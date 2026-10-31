
name: cwe-215-sensitive-information-in-debugging-code
description: Use when testing cwe-215 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-215, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-215 - Sensitive Information in Debugging Code

CWE-215: debugging code left in the application exposes sensitive information (a config, a log, a breakpoint) that reveals internals or state.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-215 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When debugging code (a dev tools endpoint, a debug flag, a code comment) exposes sensitive data.

## Detection & Test

1. **Find the debugging artifact.** Search for a debug endpoint, a `?debug` flag, or a leftover code comment.
2. **Access the artifact.** Send a request to the debug endpoint or set the debug flag.
3. **Confirm the sensitive data is exposed.** Show the artifact reveals config, state, or internals.
4. **Document the endpoint, the flag, and the exposed data.

## Example Findings

- A `?debug=1` flag that dumps the application config.
- A left-over debug endpoint at `/debug/info` that shows the session and request details.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).