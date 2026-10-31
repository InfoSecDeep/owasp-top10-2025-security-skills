
name: cwe-294-auth-bypass-capture-replay
description: Use when a web auth flaw matches cwe-294.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-294, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-294 - Authentication Bypass by Capture-Replay

CWE-294: a captured authentication token (cookie, header, token) can be replayed to re-authenticate, so the attacker logs in with the captured value after the legitimate user logs out.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-294 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an authentication token can be replayed (a session that doesn't rotate or a token that's reused).

## Detection & Test

1. **Capture a valid token.** Get a session cookie, Bearer token, or auth header from a valid login.
2. **Replay the token.** Send the captured token in a new request.
3. **Confirm the replay.** Show the token authenticates without a fresh login.
4. **Escalate.** Use the replayed token to access a protected resource.
5. **Document the token, the replay, and proof.

## Example Findings

- A session cookie that works after the user logs out (not invalidated).
- A Bearer token that is replayed in a new request after the original session ends.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).