
name: cwe-915-improperly-controlled-modification-of-dynamically-determined-object-attributes
description: Use when testing cwe-915 integrity on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-915, integrity, a08, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a08-software-data-integrity
---

# CWE-915 - Improperly Controlled Modification of Dynamically-Determined Object Attributes (Mass Assignment)

CWE-915: the application accepts object attributes from user input and modifies the object without restricting which attributes can be set, so an attacker can set privileged fields (role, balance, status) to change the object's state.

## Parent Skill

This is a sub-skill of `owasp-a08-software-data-integrity` (OWASP A08 Software or Data Integrity Failures, Top 10 2025).
Load the parent for overall A08 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-915 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the application accepts object attributes from user input and modifies the object without restricting which fields can be set (mass assignment).

## Detection & Test

1. **Find the create/update endpoint.** Identify the endpoint that accepts object data (a form, an API POST/PUT).
2. **Add a privileged field.** Include a field that should not be user-settable (role, isAdmin, balance, ownerId, status).
3. **Confirm the field is persisted.** Read the object back to verify the privileged field was set.
4. **Escalate.** Use the modified field to escalate privileges or change state.
5. **Document the field, the value, and the read-back proof.

## Example Findings

- A user update endpoint that accepts `role=admin` and persists it.
- An order create endpoint that accepts `totalDiscount=100%` and applies it.
- A profile update that accepts `balance=999999` and sets the user's balance.

## Impact

- Code execution via deserialization or a malicious code path (CWE-502/494/506/509).
- Privilege escalation via mass assignment (CWE-915).
- Authentication/authorization bypass via a tampered cookie (CWE-565/784).
- Persistence or lateral spread from a replicated component (CWE-509/830).
- Search-path or untrusted-sphere abuse leading to arbitrary code execution (CWE-426/427/829).

## See Also

- `owasp-a08-software-data-integrity` - parent skill (A08 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).