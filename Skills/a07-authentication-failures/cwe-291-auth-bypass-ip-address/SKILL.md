
name: cwe-291-auth-bypass-ip-address
description: Use when a web auth flaw matches cwe-291.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-291, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-291 - Authentication Bypass by Spoofing of Source IP Address

CWE-291: authentication relies on the source IP address being in an allowlist, so an attacker who reaches or spoofs that IP can bypass authentication.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-291 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When access is controlled by an IP allowlist and the source IP can be spoofed or the IP is reachable.

## Detection & Test

1. **Find the IP allowlist.** Identify which IPs are trusted for access.
2. **Spoof or reach the IP.** Use a spoofed IP or route through a trusted IP.
3. **Confirm the bypass.** Show the IP allowlist accepts the spoofed source.
4. **Escalate.** Use the trusted IP to reach the resource.
5. **Document the allowlist, the spoof, and proof.

## Example Findings

- A login page only accepts `10.0.0.0/8`; a spoofed `X-Forwarded-For` bypasses it.
- An IP allowlist that the attacker reaches by routing through a trusted host.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).