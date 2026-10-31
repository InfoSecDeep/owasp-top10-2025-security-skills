
name: cwe-88-argument-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-88, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-88 - Argument Injection or Parameter Injection

CWE-88: user input is used as an argument to a command or tool, and the attacker injects an option or flag that changes the tool's behavior (option injection).

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-88 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter is passed as an argument to a command-line tool (grep, curl, find, convert, etc.).

## Detection & Test

1. **Identify the tool and its options.** Determine which CLI tool receives the user input.
2. **Inject dangerous options.** Send `--`, `-`, and known dangerous flags (`-f`, `-o`, `-I`, `--header`).
3. **Confirm behavior change.** Show the tool behaves differently with the injected option.
4. **Escalate.** Use option injection to read a file, write a file, or change output format.
5. **Document the tool, option, and proof.

## Example Findings

- `grep user_input file` where input = `--color=always` or `-f /etc/passwd`.
- `curl user_input` where input = `-I` (headers only) or `-o /tmp/x`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).