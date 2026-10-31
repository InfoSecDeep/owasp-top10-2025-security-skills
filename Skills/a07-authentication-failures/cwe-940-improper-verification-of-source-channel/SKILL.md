
name: cwe-940-improper-verification-of-source-channel
description: Use when a web auth flaw matches cwe-940.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-940, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-940 - Improper Verification of Source of a Communication Channel

CWE-940: the source of a communication channel is not properly verified, so a request from a wrong source is accepted.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-940 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the source of a communication channel is not properly verified (a request from a wrong source is accepted).

## Detection & Test

1. **Find the source check.** Identify where the app verifies the source of a channel (a header, an IP, a certificate).
2. **Send a wrong source.** Use a request from an untrusted source.
3. **Confirm the source is accepted.** Show the app accepts the wrong source.
4. **Escalate.** Use the accepted source to reach the channel.
5. **Document the source, the wrong value, and proof.

## Example Findings

- A request from `http://attacker.com` that is accepted by a check that expects `http://trusted.com`.
- A channel that accepts a request with a spoofed source header.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).