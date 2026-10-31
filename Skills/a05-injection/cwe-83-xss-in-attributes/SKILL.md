
name: cwe-83-xss-in-attributes
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-83, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-83 - Cross-Site Scripting via Injection of Pointers into HTML Markup

CWE-83: a value injected into an HTML attribute breaks out of the attribute and executes script (attribute-breaking XSS).

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-83 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a user value lands inside an HTML attribute (href, src, data-*) and can close the attribute.

## Detection & Test

1. **Find the attribute.** Identify which HTML attribute contains user input (href, src, alt, data-url).
2. **Break the attribute.** Send `" onmouseover="alert(1)` or `' onfocus='alert(1)` to close the attribute.
3. **Confirm execution.** Verify the injected handler fires (hover, focus, load).
4. **Escalate.** Use the attribute-breaking XSS for cookie theft or session hijack.
5. **Document the attribute, payload, and proof.

## Example Findings

- `href="user_input"` where input = `" onmouseover="alert(1)`.
- `src='user_input'` where input = `' onerror='alert(1)'`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).