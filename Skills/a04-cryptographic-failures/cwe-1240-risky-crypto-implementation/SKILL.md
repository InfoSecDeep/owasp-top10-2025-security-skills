
name: cwe-1240-risky-crypto-implementation
description: Use when testing CWE-1240 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Use of Cryptographic Primitive with Risky Implementation

CWE-1240: Use of Cryptographic Primitive with Risky Implementation occurs when an app implements or wires a primitive (hash, HMAC, AES) in a way that is subtly insecure - non-constant-time comparison, bad chaining, hand-rolled encryption, or misuse of a valid primitive.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-1240 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When encryption/hashing is app-rolled or a primitive is applied incorrectly despite being known-good.

## Detection & Test

1. **Find custom crypto.** Look for `xor`, hand-rolled encrypt functions, or `==` on hash output.
2. **Check timing.** Constant-time comparison required for secret equality; `==` is not.
3. **Verify modes/params.** ECB misuse, missing padding validation, reused nonces, weak KDF iteration counts.
4. **Test the risky property.** For `==` on secrets, submit near-miss values and time responses; for ECB, feed two equal plaintext blocks and see equal ciphertext.
5. **Produce a differential.** Show a valid plaintext decrypts or a secret compares unequal only at a boundary.

## Example Findings

- `if (input_hash == stored_hash)` non-constant-time in auth middleware.
- `AES-ECB` used for token encryption.
- Custom `xor`-based token encoding labeled 'encrypted'.
- HMAC over `(msg, key)` concatenated instead of nested.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).