
name: cwe-334-small-random-space
description: Use when testing CWE-334 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Small Space of Random Values

CWE-334: Small Space of Random Values occurs when a pseudo-random generator's state space or output space is small, so the number of distinct outputs is limited and brute-force/guess attacks become feasible.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-334 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a PRNG's state/output space is too small for the security use.

## Detection & Test

1. **Estimate space.** Check bit length of internal state and outputs.
2. **Enumerate.** If space is small (< 64 bits), brute force the whole space offline.
3. **Match.** Correlate brute-forced outputs with observed tokens.
4. **Confirm.** Predict a live token once the space is covered.
5. **Recommend.** Use a PRNG with >= 128-bit state.

## Example Findings

- 32-bit LCG seed => 4 billion states, brute-forceable.
- 8-bit output token => trivially guessed.
- Generator period < token volume.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).