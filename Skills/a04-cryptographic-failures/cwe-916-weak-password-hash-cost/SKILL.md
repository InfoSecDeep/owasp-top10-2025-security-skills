
name: cwe-916-weak-password-hash-cost
description: Use when testing CWE-916 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Password Hash With Insufficient Computational Effort

CWE-916: Password Hash With Insufficient Computational Effort occurs when a password hash uses too few iterations / too weak parameters, letting brute-force run fast even for a strong algorithm.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-916 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a password hash uses too few iterations or weak parameters (e.g. bcrypt cost < 10, PBKDF2 < 100k).

## Detection & Test

1. **Locate hashing.** Find the password-hashing function and parameters.
2. **Read the cost.** bcrypt cost factor, PBKDF2 iteration count, Argon2 time/memory params.
3. **Benchmark.** Compare against OWASP/low recommendations (bcrypt >= 12; PBKDF2-HMAC-SHA256 >= 100k+ iterations).
4. **Estimate rate.** Approximate hashes/sec and time-to-crack the weakest passwords.
5. **Recommend.** Raise the cost to the recommended floor and re-hash.

## Example Findings

- bcrypt with cost factor 4 => ~1M hashes/sec.
- PBKDF2-HMAC-SHA1 with 1000 iterations => fast brute force.
- Argon2 with tiny memory/time params.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).