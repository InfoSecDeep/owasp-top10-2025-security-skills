
name: cwe-759-hash-without-salt
description: Use when testing CWE-759 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Use of a One-Way Hash without a Salt

CWE-759: Use of a One-Way Hash without a Salt occurs when a cryptographic hash used for password storage or token binding has no random per-value salt, enabling precomputed rainbow-table attacks across the whole dataset.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-759 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a revealed hash has no salt column, uses a constant salt, or matches a rainbow-table lookup.

## Detection & Test

1. **Capture hashes.** From password reset, registration, /users export, or error output.
2. **Inspect format.** Salted hashes embed salt (bcrypt `$2b$`, PBKDF2, Argon2 `$argon2id$`); a bare hex is unsalted.
3. **Determine salt strategy.** Is the salt empty, constant, or derived from a non-secret (email)? Constant = effectively unsalted.
4. **Crack offline.** Run hashcat against a rainbow table or wordlist; unsalted SHA-256/MD5 crack fast.
5. **Benchmark effort.** Unsalted + fast algorithm = critical; report expected seconds-to-crack.

## Example Findings

- Plaintext-ish MD5 hash in `/export` => crackable in minutes.
- PBKDF2 with `salt=constant` across all users.
- SHA-1 token stored with no per-user salt.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).