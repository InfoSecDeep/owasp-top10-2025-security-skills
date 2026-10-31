
name: cwe-628-function-call-with-incorrect-arguments
description: Use when a web design flaw matching cwe-628 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-628, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-628 - Function Call with Incorrect Arguments (SSRF-specific)

CWE-628: a function is called with arguments that the attacker controls in a way that changes its behavior, such as passing a URL or host that the function fetches (a server-side request forgery variant).

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-628 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a function (especially a fetch or URL handler) is called with a user-controlled argument.

## Detection & Test

1. **Find the function call.** Identify functions called with a URL, host, or path argument.
2. **Send an adversarial argument.** Send an internal URL or an unexpected path.
3. **Confirm behavior change.** Show the function fetches or acts on the internal resource.
4. **Escalate.** Use the SSRF-style access to reach an internal service.
5. **Document the function, the argument, and proof.

## Example Findings

- A `fetch(url)` where url is an internal endpoint.
- A function called with a user-controlled argument that triggers SSRF.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).