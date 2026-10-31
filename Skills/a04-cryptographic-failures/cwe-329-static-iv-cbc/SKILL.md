
name: cwe-329-static-iv-cbc
description: Use when testing CWE-329 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Not Using a Random IV with CBC Mode

CWE-329: Not Using a Random IV with CBC Mode occurs when CBC encryption uses a fixed, zero, or reused initialization vector, so identical plaintexts produce identical ciphertexts and leak plaintext equivalence.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-329 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When CBC-mode encryption uses a fixed, zero, or repeated IV.

## Detection & Test

1. **Identify CBC.** Find AES-CBC / 3DES-CBC usage in code or endpoints.
2. **Observe the IV.** Check for a constant, all-zero, or sequential IV in requests/responses.
3. **Exercise it.** Encrypt two known identical plaintexts with the IV and confirm identical ciphertext.
4. **Recover.** Plaintext equivalence allows pattern leakage or selective decryption with the key.
5. **Recommend.** Use a fresh random IV per operation (or switch to GCM).

## Example Findings

- AES-CBC with IV = 00000000 => identical blocks leak.
- A per-connection fixed IV reused across users.
- 3DES-CBC IV derived from a constant.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).