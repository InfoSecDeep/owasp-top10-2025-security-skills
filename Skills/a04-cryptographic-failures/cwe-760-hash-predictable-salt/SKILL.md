
name: cwe-760-hash-predictable-salt
description: Use when testing CWE-760 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Use of a One-Way Hash with a Predictable Salt

CWE-760: Use of a One-Way Hash with a Predictable Salt occurs when a hash is salted but the salt is low-entropy or secret-derivable (constant, the username/email, or a timestamp), so precomputed tables can still be built and the salt offers little protection.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-760 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a hash appears salted but the salt is constant, derived from user data, or time-based.

## Detection & Test

1. **Capture hashes and their salt columns.**
2. **Classify the salt.** Is it the same for all rows (constant), equal to a user field (email/username), or `time()`-based?
3. **Reconstruct offline.** If salt is enumerable (known/derivable), build a rainbow table keyed by the predictable salt.
4. **Show degradation.** Compare brute-force cost with the predictable salt vs. a true random salt - usually negligible improvement.
5. **Recommend fix.** Store a per-user random salt and a proper iteration count.

## Example Findings

- Salt = user email lowercase => per-user table, but predictable.
- Salt = `int(time()/1000)` => enumerable within a second.
- Salt = `config.SALT` constant in source => global table works.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).