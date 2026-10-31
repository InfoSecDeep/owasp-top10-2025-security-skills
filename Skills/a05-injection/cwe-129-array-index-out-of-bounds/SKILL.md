
name: cwe-129-array-index-out-of-bounds
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-129, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-129 - Improper Validation of Array Index

CWE-129: user input is used as an array index without validation, allowing out-of-bounds access that can read or write unintended memory.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-129 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter is used as an array index (e.g. `items[user_input]`) without bounds checking.

## Detection & Test

1. **Find the array access.** Look for array indexing with a user-controlled index.
2. **Test out-of-bounds indices.** Send `-1`, `0`, `999`, and `items.length` as the index.
3. **Confirm the out-of-bounds access.** Verify the app reads or writes an unintended array element.
4. **Document the array, index, and proof.

## Example Findings

- `GET /items?i=-1` returns a different item than `i=0`.
- `POST /cart {"items":[{"id":1,"qty":0}],"index":999}` writes to a wrong cart slot.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).