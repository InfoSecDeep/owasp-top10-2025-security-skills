
name: cwe-97-ssi-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-97, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-97 - Server-Side Include (SSI) Injection

CWE-97: user input is written to a file served by a Server-Side Include processor, allowing the attacker to execute server-side code.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-97 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter is written to a file that is processed by SSI (Apache, IIS, etc.) or a template engine with SSI-like features.

## Detection & Test

1. **Find the SSI sink.** Identify which file or template is processed by an SSI engine (look for `<!--#include-->`, `<!--#exec-->` directives).
2. **Inject an SSI directive.** Send `<!--#exec cmd="id" -->` or `<!--#include file="/etc/passwd" -->` into the parameter.
3. **Confirm execution.** Verify the directive executes on the server (response shows the command output).
4. **Document the file, payload, and proof.

## Example Findings

- `<!--#exec cmd="cat /etc/passwd" -->` in a user profile page.
- `<!--#include file="/etc/passwd" -->` in a template.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).