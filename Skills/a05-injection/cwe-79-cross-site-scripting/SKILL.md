
name: cwe-79-cross-site-scripting
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-79, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-79 - Cross-Site Scripting (XSS)

CWE-79: untrusted input is included in web page content without proper output encoding, allowing script execution in the victim's browser.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-79 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Any reflected, stored, or DOM-based context where input reaches HTML, JS, or attribute output.

## Detection & Test

1. **Map output contexts.** Identify where user input appears: HTML body, HTML attribute, JavaScript, URL, JSON.
2. **Break context.** Use the context-appropriate payload: `"><script>alert(1)</script>` for HTML body, `" onmouseover="alert(1)` for attributes.
3. **Confirm execution.** Open the payload in a browser and confirm the script runs.
4. **Escalate.** Steal the session cookie, perform an admin action, or pivot to DOM XSS via a message handler.
5. **Document context, payload, and proof (screenshot or HAR).

## Example Findings

- Reflected: `GET /search?q=<script>alert(1)</script>`.
- Stored: a comment with `"><img src=x onerror=alert(1)>`.
- DOM: `window.location.hash` used in `innerHTML`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).