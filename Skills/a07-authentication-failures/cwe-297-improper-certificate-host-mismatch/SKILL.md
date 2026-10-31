
name: cwe-297-improper-certificate-host-mismatch
description: Use when a web auth flaw matches cwe-297.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-297, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-297 - Improper Handling of Device-specific Certificate (Host Mismatch)

CWE-297/298/299: a certificate is validated but the hostname check is missing or flawed, so a cert for one host is accepted for another.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-297 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the certificate hostname doesn't match the requested host but is still accepted.

## Detection & Test

1. **Identify the hostname check.** Find where the cert's hostname is compared to the requested host.
2. **Send a mismatched hostname.** Use a cert for `a.com` on `b.com`.
3. **Confirm the mismatch is accepted.** Show the cert is accepted despite the hostname difference.
4. **Escalate.** Use the mismatched cert for a MITM.
5. **Document the hostname, the cert, and proof.

## Example Findings

- A wildcard cert for `*.trusted.com` accepted for `api.trusted.com.evil.com`.
- A cert for `internal.com` accepted for `internal.com.evil.com`.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).