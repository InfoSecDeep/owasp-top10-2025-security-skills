
name: cwe-646-reliance-on-file-name-extension-of-external-file
description: Use when a design permits more inputs than required.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-646, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-646 - Reliance on File Name or Extension of an Externally-Supplied File

CWE-646: an app relies on the extension of an externally-supplied file to decide if it is safe, letting the attacker bypass the check (double extension, MIME mismatch).

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-646 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an upload's safety is decided by its extension or name alone.

## Detection & Test

1. **Find the upload extension check.** Identify where the extension decides safety.
2. **Test double extensions.** Upload `shell.php.jpg` or `shell.jpg.php`.
3. **Test MIME mismatch.** Upload a PHP file with a `image/jpeg` MIME type.
4. **Confirm serving.** If the served/executed file is treated as its extension, the check is bypassed.
5. **Document the check, the bypass, and proof.

## Example Findings

- A `photo.php.jpg` upload served as PHP.
- An SVG uploaded as `image/svg+xml` but executed as HTML.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).