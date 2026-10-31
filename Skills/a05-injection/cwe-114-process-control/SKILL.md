
name: cwe-114-process-control
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-114, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-114 - Process Control

CWE-114: user input controls a process's lifecycle (start, stop, restart) or its parameters without validation, allowing the attacker to control the process behavior.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-114 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter controls a process (a daemon, a job, a service) without validating the input.

## Detection & Test

1. **Find the process control.** Identify which parameter controls a process (a `/restart` endpoint, a `?stop=true` parameter).
2. **Test parameter manipulation.** Send unexpected values for the process parameter (e.g. `process=../other_process`).
3. **Confirm the process is affected.** Verify the wrong process was started, stopped, or restarted.
4. **Document the parameter, payload, and proof.

## Example Findings

- `?action=restart&process=user_input` where input = `web_server` instead of `worker_1`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).