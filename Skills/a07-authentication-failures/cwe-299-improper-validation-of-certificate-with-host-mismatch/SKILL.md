
name: cwe-299-improper-validation-of-certificate-with-host-mismatch
description: Use when TLS cert host/chain validation is loose or skipped.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-299, owasp, top10-2025, pentest]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-299 - Improper Validation of Certificate with Host Mismatch

CWE-299: the client's validation of a host's certificate is improper - hostname and/or validity checks are absent or bypassed - so any attacker-controlled certificate on the target host authenticates.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (A07 Authentication Failures, OWASP Top 10 2025). Load the parent for overall category scope, the shared test procedure, and validation criteria (negative control). This skill covers the CWE-299 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- Any code path that dials the target over TLS (API, SAML IdP, upstream service) with a permissive certificate validator.

## Detection & Test

1. Supply a mismatched-host certificate and observe acceptance; compare with a mismatched-host certificate that IS rejected.
2. Toggle hostname verification off and confirm the attack surface widens (self-signed and wrong-host certs both accepted).
3. Replay a captured session over a rogue endpoint using a fabricated certificate and confirm the client proceeds.

## Example Findings

- A configured endpoint where verifyCertificate=false lets any cert/hostname pass.
- An IdP/API client accepting a fabricated certificate and issuing a token.

## Impact

- Forged-certificate man-in-the-middle; forged token/credential issuance.
- Completes an auth-bypass chain: the identity the client trusts is no longer the real host.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, test procedure, validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full CWE table, priority order).