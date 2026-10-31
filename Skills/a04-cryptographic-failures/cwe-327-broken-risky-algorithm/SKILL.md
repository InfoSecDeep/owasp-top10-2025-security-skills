
name: cwe-327-broken-risky-algorithm
description: Use when testing CWE-327 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Use of a Broken or Risky Cryptographic Algorithm

CWE-327: Use of a Broken or Risky Cryptographic Algorithm occurs when an algorithm with known weaknesses (RC4, DES/3DES weak, MD5, SHA-1, IDEA, RC2) is used for protection.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-327 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a cipher/hash with known weaknesses (RC4, DES, MD5, SHA-1) is in active use.

## Detection & Test

1. **Enumerate.** `openssl s_client`, `nmap --script ssl-enum-ciphers` to list active ciphers/hashes.
2. **Match to a known list.** RC4, DES/3DES-64, MD5, SHA-1, Blowfish, IDEA.
3. **Prove usability.** Complete a handshake on the weak cipher; decrypt a captured sample if feasible.
4. **Estimate attack.** Quote realistic cost (RC4 biases, Sweet32 on 3DES, MD5 collisions).
5. **Recommend.** Disable the algorithm and pin to a modern suite.

## Example Findings

- RC4 cipher negotiated => keystream bias attack.
- 3DES-64 accepted => Sweet32 birthday attack.
- MD5 used for a signature/hash => collision forgery

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).