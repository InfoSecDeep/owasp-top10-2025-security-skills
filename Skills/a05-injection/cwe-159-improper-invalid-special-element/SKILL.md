
name: cwe-159-improper-invalid-special-element
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-159, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-159 - Improper Handling of Invalid Special Element

CWE-159: the app does not handle an invalid special element (e.g. a null byte, a lone surrogate, an overlong UTF-8) correctly, causing a crash, truncation, or unexpected behavior.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-159 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter contains an invalid or unusual special element (null byte, lone surrogate, overlong encoding) that the app doesn't handle gracefully.

## Detection & Test

1. **Find the special element handling.** Identify which special elements the app processes (null byte, backslash, quote, etc.).
2. **Send an invalid variant.** Send a null byte (`%00`), a lone surrogate (`%ed%a0%80`), or an overlong UTF-8 sequence.
3. **Observe the behavior.** Check for a crash, truncation, or unexpected response.
4. **Document the special element, payload, and observed behavior.

## Example Findings

- A file name with a null byte truncates the extension check: `file=shell.php%00.jpg`.
- A user name with a lone surrogate causes a Unicode decode error in the log.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).