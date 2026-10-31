
name: cwe-336-same-prng-seed
description: Use when testing CWE-336 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Same Seed in PRNG

CWE-336: Same Seed in PRNG occurs when a pseudo-random generator is initialized with an identical seed on every run, so the entire output sequence repeats and tokens become fully deterministic.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-336 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When tokens repeat in a short window, or a PRNG reseeds identically per session/worker.

## Detection & Test

1. **Capture a burst.** Collect many tokens within seconds.
2. **Detect repetition.** Look for exact repeats or identical sequence start points.
3. **Confirm the seed.** Find a code path, config, or startup value that reuses a constant seed (e.g. `random.seed(42)` at app init).
4. **Replay.** Re-seed identically and reproduce a captured token.

## Example Findings

- `random.seed(42)` at module import => every request's token sequence is identical.
- A worker that re-inits the RNG from a constant on each connection.
- JWT jti = hash of a fixed nonce.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).