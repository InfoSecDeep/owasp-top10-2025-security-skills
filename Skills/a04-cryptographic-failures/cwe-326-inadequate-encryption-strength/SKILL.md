
name: cwe-326-inadequate-encryption-strength
description: Use when testing CWE-326 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Inadequate Encryption Strength

CWE-326: Inadequate Encryption Strength occurs when an encryption scheme lacks sufficient strength to resist attack - short key length, a deprecated cipher, or parameters too small to be safe.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-326 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an encryption scheme uses a short key, a deprecated cipher, or too-small parameters.

## Detection & Test

1. **Identify the scheme.** AES/RSA key size, cipher mode, stream-cipher length.
2. **Compare to a modern floor.** AES-128 minimum, RSA-2048 minimum, no RC4/DES.
3. **Probe the parameter.** Confirm key length from response sizes or metadata; decrypt a sample if a short key is found.
4. **Estimate effort.** Quote the cost to brute force the key.
5. **Recommend.** Use AES-256/RSA-2048+ and modern key lengths.

## Example Findings

- AES-128 with ECB mode and a reused IV.
- RSA-1024 key negotiated => factorable.
- 56-bit DES in an older endpoint.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).