
name: cwe-89-sql-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-89, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-89 - SQL Injection

CWE-89: user input is concatenated into a SQL query without parameterization, allowing the attacker to alter the query's structure.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-89 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Any parameter that reaches a database query as part of the query string.

## Detection & Test

1. **Find the injection point.** Send `'`, `"`, `;`, `--`, `#`, and `/* */` into the parameter.
2. **Determine the query type.** Is it a SELECT, INSERT, UPDATE, or DELETE? Is it in a WHERE, ORDER BY, or LIMIT clause?
3. **Test error-based and blind SQLi.** Use `AND 1=1` vs `AND 1=2` for blind; use a time delay for out-of-band.
4. **Extract data.** Use `UNION SELECT`, `ORDER BY N`, or `INFORMATION_SCHEMA` to enumerate databases.
5. **Confirm and escalate.** Read a table, write a file, or run a system command if the DB supports it.

## Example Findings

- `GET /user?id=1' OR 1=1 --`.
- `POST /login {"user":"admin'--","pass":"x"}`.
- `ORDER BY 1,2,3` to find column count for UNION-based SQLi.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).