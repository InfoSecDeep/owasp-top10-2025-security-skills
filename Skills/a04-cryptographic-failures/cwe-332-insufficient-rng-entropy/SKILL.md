
name: cwe-332-insufficient-rng-entropy
description: Use when testing CWE-332 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Insufficient Entropy in PRNG

CWE-332: Insufficient Entropy in PRNG occurs when the seed or entropy source feeding a pseudo-random generator is too low-entropy, so the output stream is predictable regardless of the algorithm's quality.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-332 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the PRNG seed/entropy source is too low-entropy to produce secure output.

## Detection & Test

1. **Identify the entropy source.** Check what feeds the RNG (time, PID, a fixed constant, low-bit counter).
2. **Measure input entropy.** Sample the seed source and estimate its distinct-value space.
3. **Recover/reproduce.** If the source has small space, enumerate seeds and match an observed token.
4. **Predict.** Forecast the next token after reproducing the seed.
5. **Recommend.** Seed from a CSPRNG entropy pool (os.urandom, /dev/urandom, hardware RNG).

## Example Findings

- RNG seeded from `time()` at millisecond resolution only.
- RNG seeded from a process counter with 1000 values.
- A 'random' value built from a constant seed.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).