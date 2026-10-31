
name: cwe-330-insufficient-randomness
description: Use when testing CWE-330 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Use of Insufficiently Random Values

CWE-330: Use of Insufficiently Random Values occurs when a security token or value is not sufficiently random - its distribution, period, or state can be weak, letting outputs be predicted.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-330 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a security token's randomness is statistically weak or predictable.

## Detection & Test

1. **Capture many samples.** Pull 50+ security tokens.
2. **Statistical checks.** Chi-square, bit-distribution, autocorrelation tests.
3. **Pattern search.** Repetitions, short periods, partial sequences, or correlation with inputs.
4. **Predict.** Forecast the next value and confirm against a live token.
5. **Determine PRNG.** Identify the generator so state can be recovered.

## Example Findings

- Token byte distribution highly skewed.
- Token repeats every N samples (short period).
- Token correlates with the request timestamp.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).