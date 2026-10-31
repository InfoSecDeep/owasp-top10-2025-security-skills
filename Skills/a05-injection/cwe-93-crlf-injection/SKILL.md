
name: cwe-93-crlf-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-93, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-93 - CRLF Injection (HTTP Response Splitting)

CWE-93: user input containing CR (`\r`) and LF (`\n`) is written to an HTTP header or log, allowing the attacker to inject new headers or split the response.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-93 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter is written to an HTTP header, a redirect Location, or a log entry without stripping CR/LF.

## Detection & Test

1. **Find the header sink.** Identify which parameter reaches an HTTP header (Set-Cookie, Location, X-Custom).
2. **Inject CRLF.** Send `%0d%0a` (URL-encoded CR LF) or literal `\r\n` into the parameter.
3. **Confirm header injection.** Check if a new header (e.g. `Set-Cookie: pwned=1`) appears in the response.
4. **Test response splitting.** If the injection is in the first header, try to split the response into two.
5. **Document the header, payload, and proof (response with injected header).

## Example Findings

- `Set-Cookie: session=user_input` where input = `abc%0d%0aInjected: 1`.
- A redirect `Location: /user_input` where input = `x%0d%0aSet-Cookie: pwned=1`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).