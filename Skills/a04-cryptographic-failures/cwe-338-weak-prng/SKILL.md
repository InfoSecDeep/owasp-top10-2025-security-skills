
name: cwe-338-weak-prng
description: Use when testing CWE-338 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Use of a Cryptographically Weak PRNG

CWE-338: Use of a Cryptographically Weak PRNG occurs when an application relies on a generator with weak statistical properties or small internal state (LCGs, `rand()`, `Math.random()`, the Python `random` module), so state can be recovered from observed outputs.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-338 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When randomness is used for security tokens but the implementation relies on a weak PRNG.

## Detection & Test

1. **Identify the PRNG.** Inspect source or behavior to find `rand()`/`srand()` (C/PHP), `Math.random()` (JS), `random.random()` (Python), LCGs, or `rand_r`.
2. **Sample extensively.** Capture 50+ tokens.
3. **Recover state.** Use lattice/time-sequence analysis or the known linear recurrence to predict future outputs.
4. **Predict & verify.** Forecast the next token and match it to a live server value.

## Example Findings

- Java `Random` seeded from time => recoverable from a handful of outputs.
- C `rand()` in auth token code => predictable sequence.
- `Math.random()` used for a login CSRF token.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).