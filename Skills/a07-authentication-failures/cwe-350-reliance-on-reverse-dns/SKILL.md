
name: cwe-350-reliance-on-reverse-dns
description: Use when a web auth flaw matches cwe-350.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-350, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-350 - Reliance on Reverse DNS for a Security-Critical Action

CWE-350: a security-critical action relies on a reverse DNS lookup, which the attacker can spoof or control.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-350 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a security-critical action (authn, authz) relies on a reverse DNS lookup.

## Detection & Test

1. **Find the reverse DNS check.** Identify where the app uses reverse DNS for a security decision.
2. **Spoof the DNS.** Set up a DNS record that resolves to the expected value.
3. **Confirm the spoof.** Show the reverse DNS check accepts the spoofed value.
4. **Escalate.** Use the spoofed DNS to reach the resource.
5. **Document the DNS value, the spoof, and proof.

## Example Findings

- A check that resolves the client's IP to a hostname and grants access based on the hostname.
- A security-critical action that relies on a reverse DNS lookup.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).