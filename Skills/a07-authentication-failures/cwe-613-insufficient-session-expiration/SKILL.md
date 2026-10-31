
name: cwe-613-insufficient-session-expiration
description: Use when a web auth flaw matches cwe-613.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-613, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-613 - Insufficient Session Expiration

CWE-613: a session does not expire after the stated timeout, so the session remains valid past the expected window.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-613 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a session does not expire after the stated idle or absolute timeout.

## Detection & Test

1. **Identify the session timeout.** Find the stated idle or absolute timeout.
2. **Wait past the timeout.** Send a request after the timeout period.
3. **Confirm the session is still valid.** Show the session is not invalidated.
4. **Escalate.** Use the session to access a protected resource.
5. **Document the timeout, the replay, and proof.

## Example Findings

- A session that is still valid 24 hours after the 15-minute idle timeout.
- A token that is not invalidated after the stated absolute timeout.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).