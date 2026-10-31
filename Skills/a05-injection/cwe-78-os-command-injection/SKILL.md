
name: cwe-78-os-command-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-78, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-78 - OS Command Injection

CWE-78: user input is passed directly to an OS command without filtering, allowing the attacker to execute arbitrary OS commands.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-78 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter reaches `system()`, `popen()`, `exec()`, backticks, or a shell script on the server OS.

## Detection & Test

1. **Identify the OS.** Determine Linux vs Windows (different metacharacters and file paths).
2. **Test injection points.** Send `;`, `|`, `&&`, `$(...)`, backticks, `%0a` into the parameter.
3. **Confirm with OOB or delay.** Use a time delay or an out-of-band callback to confirm execution.
4. **Escalate to file read or RCE.** Read a known file or write a webshell if the app is file-writable.
5. **Document the exact payload and OS context.

## Example Findings

- Linux: `host=127.0.0.1; cat /etc/passwd`.
- Windows: `host=127.0.0.1&dir C:\`.
- A `mail` function that runs `sendmail -t < /dev/stdin` with user input in the body.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).