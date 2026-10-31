
name: cwe-434-unrestricted-upload-of-dangerous-file
description: Use when a web design flaw matching cwe-434 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-434, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-434 - Unrestricted Upload of a Dangerous File Type

CWE-434: an unrestricted upload lets the attacker upload a file type that is executed or embedded as code (PHP, HTML, SVG), enabling code execution or XSS.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-434 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an upload endpoint accepts files and serves or renders them.

## Detection & Test

1. **Find the upload endpoint.** Identify file uploads (avatar, document, image).
2. **Test dangerous types.** Upload `.php`, `.phtml`, `.html`, `.js`, `.svg`.
3. **Confirm where files land.** Determine the upload directory and whether it can execute or embed the file.
4. **Confirm serving.** If served/executed, the upload is a finding (trigger the payload or fetch the file).
5. **Document the type, location, and proof.

## Example Findings

- An avatar upload of `shell.php` served and executed at `/uploads/shell.php`.
- A `<svg onload=alert(1)>` uploaded and rendered.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).