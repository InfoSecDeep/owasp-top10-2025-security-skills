
name: cwe-382-j2ee-use-of-system-exit
description: Use when a web design flaw matching cwe-382 is suspected.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-382, design, a06, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a06-insecure-design
---

# CWE-382 - J2EE Use of System.exit()

CWE-382: a J2EE application uses System.exit() to control application flow, bypassing the container's lifecycle management (destruction hooks, resource cleanup), which can leave the app or its resources in an inconsistent or unsafe state.

## Parent Skill

This is a sub-skill of `owasp-a06-insecure-design` (OWASP A06 Insecure Design, Top 10 2025).
Load the parent for overall A06 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-382 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a J2EE app calls System.exit() for control flow (common in a CLI-style main inside a servlet or bean).

## Detection & Test

1. **Find System.exit() calls.** Locate them in the app's Java code.
2. **Assess the impact.** Determine whether the call skips cleanup, finalizers, or container hooks (resource release, shutdown logic).
3. **Prove the defect.** Trigger the path and confirm the app continues or fails cleanup unexpectedly.
4. **Escalate.** Use the inconsistent state to bypass cleanup-based protection (e.g. a gate that should close the connection).
5. **Document the call site, the skipped step, and the proof.

## Example Findings

- A servlet's init calls System.exit(), so the container never unloads the app, leaving cached credentials alive.

## Impact

- Privilege escalation or unauthorized access through the design flaw.
- Business-logic abuse (double spend, price manipulation, workflow bypass).
- Persistence until the design (boundary, locking, rate limit) is corrected.
- Lateral impact when the same flaw repeats across the app.

## See Also

- `owasp-a06-insecure-design` - parent skill (A06 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).