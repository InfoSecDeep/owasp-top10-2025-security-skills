
name: cwe-304-missing-critical-step-in-authentication
description: Use when a web auth flaw matches cwe-304.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-304, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-304 - Missing Critical Step in Authentication

CWE-304: a critical step in the authentication flow (a verification, a re-authentication, a check) is missing, so the authn flow is incomplete.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-304 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a critical step in the authentication flow is missing (a step is skipped or in the wrong order).

## Detection & Test

1. **Map the auth flow.** Identify each step (verify identity, check MFA, set session).
2. **Find the missing step.** Identify which step is absent or out of order.
3. **Skip the step.** Send a request that skips the missing step.
4. **Confirm the bypass.** Show the authn flow succeeds without the step.
5. **Document the flow, the missing step, and proof.

## Example Findings

- An MFA check that is skipped after the initial password.
- A session step that is set before the identity is verified.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).