
name: cwe-300-channel-accessible-by-non-endpoint
description: Use when a web auth flaw matches cwe-300.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-300, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-300 - Channel Accessible by Non-Endpoint

CWE-300: a communication channel (API, port, endpoint) is accessible by a non-endpoint (a client that should not reach it), allowing the attacker to send requests to the channel.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-300 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a channel is reachable by an actor that should not be able to reach it (a non-endpoint).

## Detection & Test

1. **Identify the channel.** Find the API, port, or endpoint that should be restricted.
2. **Access it from a non-endpoint.** Send a request from an actor that should not reach it.
3. **Confirm the channel is reachable.** Show the channel processes the request.
4. **Escalate.** Use the channel to reach a protected resource.
5. **Document the channel, the non-endpoint, and proof.

## Example Findings

- An internal API on port 8080 reachable from the public internet.
- A WebSocket endpoint that a static file client can reach.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).