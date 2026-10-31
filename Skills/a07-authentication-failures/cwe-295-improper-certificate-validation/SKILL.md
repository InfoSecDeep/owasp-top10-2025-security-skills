
name: cwe-295-improper-certificate-validation
description: Use when a web auth flaw matches cwe-295.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-295, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-295 - Improper Certificate Validation

CWE-295: a certificate is not validated properly (missing chain of trust, wrong hostname, self-signed, or expired), so a malicious certificate is accepted.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-295 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a TLS certificate is not validated: missing chain, wrong hostname, self-signed, or expired.

## Detection & Test

1. **Check the certificate.** Examine the cert's issuer, hostname, and validity dates.
2. **Test a mismatch.** Use a cert with a different hostname than the requested one.
3. **Confirm acceptance.** Show the client or server accepts the mismatched cert.
4. **Escalate.** Use the accepted cert to perform a MITM.
5. **Document the cert, the mismatch, and proof.

## Example Findings

- A cert issued for `a.com` is accepted for `b.com`.
- A self-signed cert that the client trusts without pinning.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).