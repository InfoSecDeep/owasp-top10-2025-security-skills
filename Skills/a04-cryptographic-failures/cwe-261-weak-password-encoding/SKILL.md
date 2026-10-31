
name: cwe-261-weak-password-encoding
description: Use when testing CWE-261 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Weak Encoding for Password

CWE-261: Weak Encoding for Password occurs when passwords are encoded with a weak or one-way method (reversible encoding, no salting) that does not resist offline guessing.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-261 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When credentials are 'hashed' via a reversible encoding or unsalted fast hash.

## Detection & Test

1. **Locate credential handling.** Find how passwords are transformed (MD5, SHA-1, reversible XOR/base64, unsalted SHA-256).
2. **Classify the transform.** Reversible encoding vs. fast one-way vs. iterative KDF.
3. **Prove weakness.** Crack the stored value offline, or reverse a reversible encoding.
4. **Confirm impact.** Recover a plaintext password for an in-scope user.
5. **Recommend.** Use a salted, iterated KDF (bcrypt/scrypt/Argon2) with a strong cost.

## Example Findings

- `base64(password)` stored in /export => reversible.
- Unsalted MD5/SHA-1 in a legacy store.
- XOR encoding labeled as 'encryption' of a password.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).