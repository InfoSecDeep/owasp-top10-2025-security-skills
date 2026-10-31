
name: cwe-116-improper-encoding-escaping
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-116, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-116 - Improper Encoding or Escaping of Output

CWE-116: the app encodes or escapes output, but the encoding doesn't match the output context (e.g. HTML-encodes for a JS context), so the escape is bypassed.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-116 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When output encoding is applied but not matched to the destination context (HTML, JS, URL, attribute, CSS).

## Detection & Test

1. **Identify the output context.** Determine where the output goes: HTML body, HTML attribute, JavaScript, URL, CSS.
2. **Test the encoding.** Send a value that is encoded for the wrong context (e.g. HTML entities in a JS context).
3. **Confirm the bypass.** Verify the value reaches the context unencoded or with the wrong encoding.
4. **Document the context, payload, and proof.

## Example Findings

- A value HTML-encoded (`&lt;script&gt;`) that is output into a `<script>` block where `&lt;` is not special.
- A URL value that is HTML-escaped but not URL-escaped, allowing a `#` to truncate the URL.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).