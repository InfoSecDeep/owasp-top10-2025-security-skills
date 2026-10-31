
name: cwe-451-user-interface-issues
description: Use when a web design flaw matching cwe-451 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-451, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-451 - User Interface Issues

CWE-451: a UI flaw (an input left visible, a value displayed that should be hidden) lets an attacker capture or manipulate privileged data.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-451 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a UI element is visible or exposed that should be hidden (a field containing a secret or a privileged value).

## Detection & Test

1. **Inspect the UI.** Identify form fields that should be hidden but are shown (password, token, private id).
2. **Confirm exposure.** Note whether the field is visible to the user and, if captured, to an attacker.
3. **Test reading it.** Retrieve the field's value (DOM inspection, HTML source).
4. **Escalate.** Use the captured value to perform a privileged action.
5. **Document the field, the exposure, and the proof.

## Example Findings

- A hidden password field that is actually rendered in the DOM.
- A private user ID displayed in a profile URL that others can read.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).