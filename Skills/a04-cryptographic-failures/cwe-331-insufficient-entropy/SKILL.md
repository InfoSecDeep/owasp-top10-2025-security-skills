
name: cwe-331-insufficient-entropy
description: Use when testing CWE-331 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Insufficient Entropy

CWE-331: Insufficient Entropy occurs when a value used as a secret, token, or nonce has too little entropy to resist guessing, brute-forcing, or prediction.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-331 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a secret/nonce/token has too little entropy to resist guessing or brute force.

## Detection & Test

1. **Measure the output.** Count distinct values and their bit length.
2. **Sample heavily.** Collect many values and estimate entropy per symbol.
3. **Brute-force test.** Estimate guesses needed; if small space, try the range.
4. **Confirm.** Match a brute-forced value to a live accepted token.
5. **Recommend.** Use >= 128 bits of cryptographic entropy for secrets.

## Example Findings

- A 'random' token of only 8 bits => 256 guesses.
- OTP uses 3 digits => 1000 possibilities.
- CSRF token drawn from a 16-value list.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).