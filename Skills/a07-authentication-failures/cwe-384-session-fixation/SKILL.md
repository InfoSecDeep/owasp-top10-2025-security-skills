
name: cwe-384-session-fixation
description: Use when a web auth flaw matches cwe-384.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-384, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-384 - Session Fixation

CWE-384: a session ID is not rotated after login, so an attacker can set a known session ID before login and replay it after the victim logs in.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-384 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a session ID is not rotated after login (an attacker can set a known session ID).

## Detection & Test

1. **Set a session ID.** Use a cookie or token to set a known session ID.
2. **Log in.** Authenticate with valid credentials.
3. **Confirm the session ID is preserved.** Check whether the session ID changed after login.
4. **Escalate.** Use the fixed session ID to access the victim's session.
5. **Document the session ID, the fixation, and proof.

## Example Findings

- A session cookie that is not rotated after login.
- A token that the attacker sets and reuses after the victim authenticates.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).