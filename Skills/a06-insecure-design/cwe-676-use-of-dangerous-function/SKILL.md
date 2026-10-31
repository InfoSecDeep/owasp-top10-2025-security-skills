
name: cwe-676-use-of-dangerous-function
description: Use when a web design flaw matching cwe-676 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-676, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-676 - Use of Potentially Dangerous Function

CWE-676: a function that has known dangerous behavior (DoS, infinite loop, memory issue) is called on untrusted input (e.g. a pathological regex, an unbounded loop over user data).

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-676 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a dangerous function is called on untrusted input: pathological regex, unbounded loop, unbounded allocation.

## Detection & Test

1. **Find the dangerous function.** Identify calls on untrusted input (regex, unbounded loop, unbounded allocation).
2. **Send a pathological input.** Inject input that triggers the danger (a large input, a regex-failure input).
3. **Confirm the effect.** Show the function misbehaves (crash, hang, memory exhaustion).
4. **Escalate.** Use the effect for DoS or memory corruption.
5. **Document the function, input, and effect.

## Example Findings

- A pathological regex on user input that causes a catastrophic backtracking hang.
- An unbounded loop that exhausts memory with a large user input.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).