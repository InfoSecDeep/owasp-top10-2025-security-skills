
name: cwe-1021-improper-restriction-of-rendered-ui-layers
description: Use when a web design flaw matching cwe-1021 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-1021, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-1021 - Improper Restriction of Rendered UI Layers or Frames (Clickjacking)

CWE-1021: an attacker layers a UI (via iframes, overlays) over a protected element, tricking a victim into clicking it (clickjacking).

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-1021 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a page can be embedded in an attacker's frame/overlay and expose a clickable protected element.

## Detection & Test

1. **Find embeddable pages.** Identify pages that are framed or overlaid (login, confirm, payment).
2. **Test framing.** Load the page in a frame from a foreign origin and check the defense.
3. **Confirm exposure.** If the frame is not blocked, a clickjacking risk exists.
4. **Escalate.** Use the frame to trick the victim into a privileged action.
5. **Document the page, the framing, and the proof.

## Example Findings

- A login page framed by an attacker to capture credentials.
- A confirmation button that can be triggered from a hidden frame.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).