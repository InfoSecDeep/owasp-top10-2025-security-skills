
name: cwe-1241-predictable-rng-algorithm
description: Use when testing CWE-1241 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Predictable Algorithm in RNG

CWE-1241: Predictable Algorithm in RNG occurs when the RNG algorithm itself is known/reverse-engineered and its outputs are recomputable (not merely weak seeds), so an attacker reproduces the exact stream.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-1241 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an RNG's algorithm is discoverable (decompiled, documented) and its outputs match a known generator.

## Detection & Test

1. **Enumerate outputs.** Capture many tokens.
2. **Identify the algorithm.** Compare against known generators via structural analysis (periodicity, modulus, output width).
3. **Recover/confirm the algorithm.** Match observed outputs to a specific PRNG algorithm (LCG mod, LFSR polynomial).
4. **Recompute.** Feed the recovered seed and algorithm parameters to reproduce a live token.
5. **Verify on server.** Predict the next server value and confirm.

## Example Findings

- Auth token matches Java `Random` stream after decompiling the jar.
- OTP stream matches a documented LFSR generator.
- HMAC-based token reproduced from a published nonce pattern.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).