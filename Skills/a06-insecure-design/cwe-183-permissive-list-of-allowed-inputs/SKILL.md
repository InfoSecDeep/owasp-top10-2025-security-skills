
name: cwe-183-permissive-list-of-allowed-inputs
description: Use when a design permits more inputs than required.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-183, owasp, top10-2025, pentest]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-183 - Permissive List of Allowed Inputs

CWE-183: the app implements a permissive allow-list of inputs, ranges, or options rather than a restrictive one, letting an attacker submit values the designer did not anticipate.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (A06 Insecure Design, OWASP Top 10 2025). Load the parent for overall category scope, the shared test procedure, and validation criteria (negative control). This skill covers the CWE-183 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- Parameters accept a list/range of values (multi-select, batch ids, price, quantity, limit) where the design never bounds what is semantically allowed.

## Detection & Test

1. Submit values far outside the intended domain: huge lists, decimals where integers are expected, signed zeros, scientific notation, unicode digits.
2. Probe multi-value params (ids[]=1&ids[]=2...) and batch endpoints for unanticipated expansion.
3. Test numeric/enum fields with boundary and out-of-range values to see which the server silently accepts.

## Example Findings

- A quantity/limit field accepts -1, 0, 1e9, or unicode digits, causing stock/price corruption.
- A bulk id list accepted for thousands of records when only a few were meaningful.

## Impact

- Business-logic abuse (stock, pricing, redemption, rate limits).
- Cascade effects across unanticipated records - a design hole often pairs with CWE-362 race / CWE-642 state control.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, test procedure, validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full CWE table, priority order).