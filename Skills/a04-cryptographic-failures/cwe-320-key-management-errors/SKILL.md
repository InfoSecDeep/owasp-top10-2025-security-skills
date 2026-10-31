
name: cwe-320-key-management-errors
description: Use when testing CWE-320 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Key Management Errors

CWE-320: Key Management Errors occurs when a cryptographic key lifecycle is mismanaged - rotation missing, expiration ignored, revocation not enforced, or keys persisted in plaintext - so compromised or expired keys keep working.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-320 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When key rotation, expiry, or revocation is missing or ignored, or keys are stored unencrypted.

## Detection & Test

1. **Locate key storage.** Find where keys are kept (config, DB, vault, hardcoded) and how they are protected at rest.
2. **Check rotation.** Is there a documented/actual rotation schedule? Old keys still accepted?
3. **Check expiry/revocation.** Can expired or revoked keys still authenticate or decrypt?
4. **Check distribution.** Are keys shared across environments or services without isolation?
5. **Simulate.** Use an expired key or a rotated-out key against an in-scope endpoint.

## Example Findings

- An expired TLS certificate/key still accepted (replay).
- DB-stored API key in plaintext.
- Same key used in prod and staging.
- No rotation after a suspected breach.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).