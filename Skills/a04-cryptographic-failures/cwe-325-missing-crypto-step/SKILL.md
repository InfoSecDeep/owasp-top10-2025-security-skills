
name: cwe-325-missing-crypto-step
description: Use when testing CWE-325 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Missing Required Cryptographic Step

CWE-325: Missing Required Cryptographic Step occurs when a necessary cryptographic step is skipped - e.g. missing random IV, omitted KDF step, missing salt, or a dropped signature check - weakening an otherwise reasonable algorithm.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-325 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an otherwise-okay algorithm is missing a required step (random IV, salt, KDF, signature verification).

## Detection & Test

1. **Identify the algorithm and its required steps.** AES-CBC needs a random IV; PBKDF2 needs iterations+salt; RSA needs OAEP.
2. **Observe usage.** Check responses/requests for reused/zero IV, missing salt, or no signature.
3. **Exercise the variant.** Feed a known (zero or repeated) IV to CBC and confirm the mode still behaves.
4. **Recover.** Use the missing-step weakness to distinguish or decrypt.
5. **Recommend.** Enforce the required steps (random IV, proper KDF, full verification).

## Example Findings

- AES-CBC with a constant/zero IV => plaintext equivalence observable.
- PBKDF2 with no iterations (effectively raw SHA) => fast crack.
- RSA encryption with no OAEP padding.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).