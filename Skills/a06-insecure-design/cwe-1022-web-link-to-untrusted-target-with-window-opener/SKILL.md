
name: cwe-1022-web-link-to-untrusted-target-with-window-opener
description: Use when a web design flaw matching cwe-1022 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1022, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-1022 - Web Link to Untrusted Target with window.opener Access

CWE-1022: a link to an untrusted target keeps the `window.opener` relationship, so the target page can manipulate the origin page (a tabnabbing / cross-origin manipulation vector).

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-1022 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a link to an external target keeps `window.opener` (target can modify the opener page).

## Detection & Test

1. **Find links to external targets.** Identify links with `target="_blank"` and no noopener/noopener.
2. **Confirm the opener relationship.** Send the victim to a link that keeps `window.opener` and have the target access `window.opener`.
3. **Confirm manipulation.** Show the target can set `window.opener.location`, navigate the origin page, or access DOM.
4. **Escalate.** Use the opener to redirect the victim or inject content.
5. **Document the link, the opener access, and proof.

## Example Findings

- A link `target="_blank"` (no noopener) where the target sets `window.opener.location`.
- A target page that changes the origin page's content via `window.opener`.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).