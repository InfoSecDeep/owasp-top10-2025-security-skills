
name: cwe-941-incorrectly-specified-destination-in-channel
description: Use when a web auth flaw matches cwe-941.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-941, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-941 - Incorrectly Specified Destination in a Communication Channel

CWE-941: the destination of a communication channel is incorrectly specified, so a request to the wrong destination is accepted.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-941 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the destination of a communication channel is incorrectly specified (a request to the wrong destination is accepted).

## Detection & Test

1. **Find the destination check.** Identify where the app specifies the destination of a channel (a URL, a host, a port).
2. **Send to a wrong destination.** Use a request to an unexpected destination.
3. **Confirm the destination is accepted.** Show the app accepts the wrong destination.
4. **Escalate.** Use the accepted destination to reach the channel.
5. **Document the destination, the wrong value, and proof.

## Example Findings

- A channel that accepts a request to `http://attacker.com` instead of `http://trusted.com`.
- A destination that is not validated before processing.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).