
name: cwe-335-incorrect-prng-seed
description: Use when testing CWE-335 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Incorrect Usage of Seeds in PRNG

CWE-335: Incorrect Usage of Seeds in PRNG occurs when a pseudo-random number generator is seeded with predictable or low-entropy values (PID, timestamp, process address), making outputs guessable even if the algorithm is sound.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-335 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When session tokens, OTPs, or CSRF tokens appear time/sequence-dependent and a PRNG seed looks predictable.

## Detection & Test

1. **Capture many samples.** Pull 20+ tokens (OTP, session, CSRF, reset codes) at close intervals.
2. **Correlate with clock.** Time-stamp each sample and check if output increments, decays, or maps to millisecond deltas.
3. **Probe known seeds.** Compare against outputs of `seed(time)` / `seed(PID)` / `seed(rand_seed)` in common languages (srand in C/PHP, random.seed in Python/JS).
4. **Confirm predictability.** Regenerate the next value from the seed and show it matches a real server token.
5. **Differentiate from CWE-337.** Wrong seed source vs. a seed the attacker actually sees — CWE-337 is the higher-privilege variant.

## Example Findings

- A reset code derived from `srand(getpid())` repeats after process restart.
- An OTP equals `int(time.time() / 60) % 1000000` on the server.
- Session id = `random.seed(hash(url))` replayable for any URL.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).