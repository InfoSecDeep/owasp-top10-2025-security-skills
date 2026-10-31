
name: cwe-340-predictable-identifiers
description: Use when testing CWE-340 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Generation of Predictable Numbers or Identifiers

CWE-340: Generation of Predictable Numbers or Identifiers occurs when session tokens, IDs, or nonces have low entropy or follow a predictable pattern, letting an attacker guess or brute-force them.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-340 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a session id, token, or nonce is low-entropy, sequential, or guessable.

## Detection & Test

1. **Sample IDs.** Capture many session ids / tokens / nonces.
2. **Measure entropy.** Check bit length and distribution; note sequential, time-based, or short-integer patterns.
3. **Detect pattern.** If numeric, test for increment/monotonic sequence; if base-encoded, check alphabet.
4. **Predict.** Forecast a plausible next id and confirm the server accepts it.

## Example Findings

- Session id = 6-digit incrementing counter.
- JWT sid = `time()` milliseconds.
- Nonce = random 8 hex chars => 32-bit space.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).