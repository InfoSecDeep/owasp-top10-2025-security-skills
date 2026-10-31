
name: cwe-436-interpretation-conflict
description: Use when a web design flaw matching cwe-436 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-436, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-436 - Interpretation Conflict

CWE-436: a parameter is interpreted by two different components differently (e.g. one as an integer, one as a filename), letting the attacker send a value that one component treats as a literal and the other as a special value.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-436 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a parameter is parsed by multiple components (web layer vs. app vs. database) with different rules.

## Detection & Test

1. **Find parameters with dual interpretation.** Look for a parameter used as both a number and a filename, or parsed by two layers.
2. **Send an adversarial value.** Send a value that is an integer in one context but a path or special value in another.
3. **Confirm divergence.** Show the two components behave differently with the same value.
4. **Escalate.** Use the divergence to bypass a numeric check (e.g. `0x2f` is 47 to one component, `//` to another).
5. **Document the parameter, the dual parsing, and proof.

## Example Findings

- A `page` parameter: 47 is numeric to one layer, `../` to another.
- A value parsed as an integer by the front-end and as a path by the back-end.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).