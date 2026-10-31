
name: cwe-290-auth-bypass-by-spoofing
description: Use when a web auth flaw matches cwe-290.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-290, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-290 - Authentication Bypass by Spoofing

CWE-290: authentication is bypassed by spoofing the source of a request (IP, hostname, or header), so the attacker presents as a trusted source without real credentials.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-290 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the authentication check trusts a source attribute (IP, hostname, header) that the attacker can spoof.

## Detection & Test

1. **Find the source-based check.** Identify where the app checks the source (IP, Referer, X-Forwarded-For, host).
2. **Spoof the source.** Send the request with the spoofed source value.
3. **Confirm the bypass.** Show the app trusts the spoofed source and grants access.
4. **Escalate.** Use the spoofed source to reach a protected resource.
5. **Document the source, the spoof, and proof.

## Example Findings

- A `X-Forwarded-For: 10.0.0.1` header that grants internal access.
- A Referer-based check that accepts `http://trusted.com`.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).