
name: cwe-23-relative-path-traversal
description: Use when ../ traversal reads files outside the app dir.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-23, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-23 - Relative Path Traversal

CWE-23: Relative Path Traversal - the attacker uses a path relative to a known/derived base directory (not an absolute filesystem root) to reach files outside the intended scope.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-23 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when traversal works via relative '../' sequences relative to an app directory or file parameter.

## Detection & Test

1. Locate a parameter that resolves relative to the app root, webroot, or the served file's own directory (e.g. ?lang=en, ?page, ?doc).
2. Derive the base from the control response, then walk up with '../' until files/dirs outside the scope appear.
3. Layer multiple '../' and mix with the base; some APIs resolve '../' per-path-segment the attacker can partially control.
4. Check for log/stack-trace responses that reveal the resolved base path.

## Example Requests

```http
GET /include?page=../../secret
```
```http
GET /load?path=../../../../../../../etc/passwd
```
```http
GET /page?../../config
```

## Bypass Tricks

- Chain `../` beyond the intended base; many frameworks resolve it against the app root.
- Mix relative with absolute fragments: `../../secret/../secret`.
- Use a known base path from an error/stack trace to walk up precisely.
- Double-encode the base to bypass a single-normalization pass.
- Leverage a trailing-slash base: `base//../../file`.
- Try `..;/` (semicolon) on servlet containers that treat it as a path segment.
- Use `;` as a path separator on IIS: `..;..;file`.


## Impact

- Read files that share the application's directory scope (config, templates, sibling files).

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).