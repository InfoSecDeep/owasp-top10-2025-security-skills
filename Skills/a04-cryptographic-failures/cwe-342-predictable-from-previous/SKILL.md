
name: cwe-342-predictable-from-previous
description: Use when testing CWE-342 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Predictable Exact Value from Previous Values

CWE-342: Predictable Exact Value from Previous Values occurs when a previously unknown value is not random but deterministically recomputable from a few earlier outputs (e.g. LFSR state), so an attacker who sees small samples can reconstruct the whole stream.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-342 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When tokens or nonces look random but reconstruct from earlier samples, or an LFSR is suspected.

## Detection & Test

1. **Sample enough.** Collect values until sequence length >= generator state size.
2. **Find the relation.** Fit a linear recurrence (Berlekamp-Massey) or recover LFSR state.
3. **Reconstruct.** Extend the stream and match a not-yet-issued token.
4. **Verify against live output.** Predict the next server value and confirm.

## Example Findings

- An activation code stream from a 16-bit LFSR solved from ~16 samples.
- A one-time pad reused with a short-period keystream.
- A session token = XOR of an offset keystream.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).