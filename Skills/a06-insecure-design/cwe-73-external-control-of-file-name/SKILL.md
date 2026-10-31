
name: cwe-73-external-control-of-file-name
description: Use when a file/path param controls which file is opened.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-73, owasp, top10-2025, pentest]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-73 - External Control of File Name or Path

CWE-73: the requested file name or path is derived from user input, letting an attacker redirect the server's file selection to an unintended target (file read, include, or download).

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (A06 Insecure Design, OWASP Top 10 2025). Load the parent for overall category scope, the shared test procedure, and validation criteria (negative control). This skill covers the CWE-73 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- A GET/redirect/download/import takes a filename, path, or template name that the server opens, includes, or serves.

## Detection & Test

1. Send controlled path inputs (/etc/passwd, ../.., absolute paths, URL-encoded, backslashes) and observe which file is read or reflected.
2. Enumerate template/include params: index, file, page, tpl, view, route; each is a resolution target.
3. Trigger the resolution and read the served content type; a served /etc/passwd or application source file is confirming.

## Example Findings

- `GET /download?path=/etc/passwd` or `?page=../../../../etc/passwd` returns a non-app file.
- A template param resolving to a server-side file and including it into the rendered response.

## Impact

- Read arbitrary server files (source, secrets, credentials on disk).
- Redirect to an included file and widen to code execution on downstream sinks.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, test procedure, validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full CWE table, priority order).