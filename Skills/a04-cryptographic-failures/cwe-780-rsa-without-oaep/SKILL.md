
name: cwe-780-rsa-without-oaep
description: Use when testing CWE-780 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Use of RSA without OAEP

CWE-780: Use of RSA without OAEP occurs when RSA is used for encryption with textbook or weak padding (PKCS#1 v1.5 or none), exposing the scheme to Bleichenbacher padding-oracle attacks, Rabin-Kanz, and multiplicative attacks.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-780 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When RSA key usage is encryption/signing and the padding is textbook or PKCS#1 v1.5, or OAEP is absent.

## Detection & Test

1. **Identify RSA usage.** Find RSA encryption endpoints, JWS/JWE, or signed cookies using RSA.
2. **Check padding.** Confirm OAEP vs PKCS#1 v1.5 vs none; v1.5 is the attack surface.
3. **Padding oracle test.** Feed modified ciphertexts and observe oracle differential responses (Bleichenbacher).
4. **Broadcast attack.** If OAEP missing, encrypt the same small plaintext to 3+ keys with the same e and solve (Rabin-Kanz).
5. **Confirm decryption.** Recover a real plaintext/ciphertext pair from target keys.

## Example Findings

- RSA with PKCS#1 v1.5 padding => Bleichenbacher oracle.
- Same RSA key reused for encryption and signing.
- Textbook RSA (no padding) on a token endpoint.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).