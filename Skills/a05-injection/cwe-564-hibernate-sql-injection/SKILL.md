
name: cwe-564-hibernate-sql-injection
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-564, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-564 - SQL Injection through Hibernate (HQL / Native Query)

CWE-564: user input is concatenated into a Hibernate HQL or native SQL query without parameterization, enabling SQL injection through the ORM layer.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-564 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a Hibernate query (HQL, JPQL, or native SQL) is built from user input without using parameterized queries.

## Detection & Test

1. **Find the HQL sink.** Look for `createQuery`, `createNativeQuery`, or `getSession().createSQLQuery` with a user-controlled string.
2. **Inject into HQL.** Send `' OR 1=1 --`, `;`, and Hibernate-specific syntax into the parameter.
3. **Confirm the injection.** Verify the query returns more data than expected.
4. **Document the query, payload, and proof.

## Example Findings

- `createQuery("from User where name = '" + userInput + "'")` where input = `admin' OR 1=1 --`.
- A native query with `"select * from t where id = " + id`.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).