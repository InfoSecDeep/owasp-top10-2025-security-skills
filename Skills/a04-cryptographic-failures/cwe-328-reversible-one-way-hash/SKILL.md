
name: cwe-328-reversible-one-way-hash
description: Use when testing CWE-328 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Reversible One-Way Hash

CWE-328: Reversible One-Way Hash occurs when a hash intended to be one-way is effectively reversible or collision-prone (MD5, SHA-1) for the protection level it provides.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-328 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When MD5 or SHA-1 is used where collision resistance matters, or the hash is recoverable.

## Detection & Test

1. **Find the hash.** Locate MD5/SHA-1 usage (auth, token, integrity).
2. **Show a fault.** MD5/SHA-1 have demonstrated collisions; reproduce one or reference known exploits.
3. **Test reversibility.** If used for secrets and unsalted, crack quickly.
4. **Confirm the risk.** Collision allows forging a matching credential/token.
5. **Recommend.** Use SHA-256+ / Argon2 and salted hashing for secrets.

## Example Findings

- MD5 used to sign a token => forge a colliding valid token.
- SHA-1 certificate signature compromised.
- Unsalted MD5 cracked in seconds.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).