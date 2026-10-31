
name: cwe-323-reused-nonce-keypair
description: Use when testing CWE-323 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Reusing a Nonce or Key Encryption Pair

CWE-323: Reusing a Nonce or Key Encryption Pair occurs when the same nonce or key/nonce pair is used for more than one encryption, breaking the security of stream ciphers, GCM, or CTR and enabling plaintext recovery.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-323 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a nonce, IV, or keypair is reused across encryptions (stream/GCM/CTR).

## Detection & Test

1. **Identify encryptor.** Look for stream ciphers, AES-GCM, AES-CTR usage.
2. **Observe nonce reuse.** Check for a fixed/zero nonce, a sequential nonce, or a nonce derived from a constant.
3. **Exercise.** Encrypt two known plaintexts with the reused nonce and compare ciphertexts.
4. **Recover.** XOR difference of ciphertexts reveals XOR difference of plaintexts; GCM forgery possible with reuse.
5. **Recommend.** Use a random nonce per key; never reuse a key+nonce pair.

## Example Findings

- AES-GCM with a fixed nonce => two ciphertexts XOR to plaintext difference.
- A session cookie encrypted with a key+nonce reused across users.
- CTR mode with a constant nonce across requests.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).