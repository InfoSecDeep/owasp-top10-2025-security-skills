
name: cwe-644-http-header-scripting-syntax
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-644, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-644 - HTTP Header Scripting Syntax Injection

CWE-644: user input is written to an HTTP header without neutralizing scripting syntax, allowing the attacker to inject script or alter header parsing.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-644 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter is written to an HTTP header and the header value can contain scripting syntax that changes how the header is parsed.

## Detection & Test

1. **Find the header sink.** Identify which parameter reaches an HTTP header.
2. **Inject scripting syntax.** Send a value that contains a script-like syntax in the header.
3. **Confirm the header is altered.** Verify the header is parsed differently (e.g. a new script is executed from the header value).
4. **Document the header, payload, and proof.

## Example Findings

- `X-Forwarded-For: user_input` where input = `1.1.1.1, alert(1)` in a header that is later evaluated.
- A `Set-Cookie` header that contains a script-like value that the browser interprets.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).