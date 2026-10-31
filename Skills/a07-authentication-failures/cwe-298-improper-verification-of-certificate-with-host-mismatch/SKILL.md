
name: cwe-298-improper-verification-of-certificate-with-host-mismatch
description: Use when TLS cert host/chain validation is loose or skipped.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-298, owasp, top10-2025, pentest]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-298 - Improper Verification of Certificate with Host Mismatch

CWE-298: certificate verification is lax - hostname is not checked, self-signed certificates are accepted, or validation is skipped - so a forged certificate for the target host authenticates without detection.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (A07 Authentication Failures, OWASP Top 10 2025). Load the parent for overall category scope, the shared test procedure, and validation criteria (negative control). This skill covers the CWE-298 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- A client (API caller, CLI, scanner) validates a TLS certificate against a target but tolerates self-signed certs or host mismatches.

## Detection & Test

1. Connect with a self-signed certificate for the host; a successful connection is CWE-298.
2. Hand back a certificate with the wrong subjectName/SAN; observe whether it is rejected.
3. Force a certificate with a valid chain but expired or wrong host and confirm the handshake still completes.

## Example Findings

- A client configured to not verify hostname accepts any self-signed certificate on the port.
- An API/IdP client accepting a fabricated certificate and issuing a token.

## Impact

- Man-in-the-middle of the client-to-server auth channel; credential/token theft over a spoofed endpoint.
- Undermines CWE-295 - the certificate no longer authenticates the intended party.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, test procedure, validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full CWE table, priority order).