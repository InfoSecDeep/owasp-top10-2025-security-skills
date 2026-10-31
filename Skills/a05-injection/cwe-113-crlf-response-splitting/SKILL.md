
name: cwe-113-crlf-response-splitting
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-113, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-113 - CRLF Injection / HTTP Response Splitting

CWE-113: user input containing CRLF is written to an HTTP response header, allowing the attacker to split the response into two separate responses.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-113 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter reaches an HTTP response header and CRLF characters are not stripped.

## Detection & Test

1. **Find the header sink.** Identify which parameter is written to an HTTP response header.
2. **Inject CRLF.** Send `%0d%0a` into the parameter.
3. **Confirm response splitting.** Check if the response contains two sets of headers (the injected header creates a new response).
4. **Exploit the split.** Use the split to cache a malicious response or inject a second HTML body.
5. **Document the header, payload, and proof (response with two header blocks).

## Example Findings

- `Set-Cookie: session=user_input` where input = `abc%0d%0aContent-Type: text/html%0d%0a%0d%0a<p>Injected</p>`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).