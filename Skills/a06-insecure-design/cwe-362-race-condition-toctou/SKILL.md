
name: cwe-362-race-condition-toctou
description: Use when a web design flaw matching cwe-362 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-362, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-362 - Race Condition (TOCTOU)

CWE-362: an application checks a condition and then uses it later, allowing a concurrent request to change the state in between (TOCTOU), causing a race.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-362 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a shared resource (balance, coupon, inventory) is read and then modified without locking.

## Detection & Test

1. **Find the shared resource.** Identify what can be consumed once or is finite (balance, coupon, inventory, one-time code).
2. **Fire concurrent requests.** Send many parallel requests (checkout, redemption, transfer) against the resource.
3. **Measure the delta.** Compare the parallel total to a sequential baseline; a mismatch proves the race.
4. **Escalate.** If confirmed, confirm the race yields a gain (double-spent funds, excess credit).
5. **Document the resource, concurrency, proof, and delta.

## Example Findings

- Sending 50 parallel checkout requests spends the balance more times than available.
- A one-time coupon redeemed concurrently before it is consumed.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).