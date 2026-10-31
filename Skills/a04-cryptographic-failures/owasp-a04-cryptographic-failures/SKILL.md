
name: owasp-a04-cryptographic-failures
description: Use when testing A04 Cryptographic Failures on web.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [owasp, top10-2025, a04, crypto, cwe, pentest]
category: pentesting-skills
related_skills:
  - owasp-top10-2025-testing
---

# A04 - Cryptographic Failures

OWASP Top 10 2025 category A04 (down from #2 in 2021). Covers weak algorithms, hard-coded keys, weak hashing, weak PRNGs, and cleartext transmission. The parent skill `owasp-top10-2025-testing` holds scope, reporting, and the full CWE reference.

## When to Use
- TLS/cipher, HSTS, password-hashing, token, randomness, or key-management testing on a web target.

## Mapped CWEs (32)

- CWE-261: Weak encoding for password
- CWE-296: Improper following of certificate chain of trust
- CWE-319: Cleartext transmission of sensitive information
- CWE-320: Key management errors (prohibited)
- CWE-321: Use of hard-coded cryptographic key
- CWE-322: Key exchange without entity authentication
- CWE-323: Reusing a nonce/key pair in encryption
- CWE-324: Use of key past expiration date
- CWE-325: Missing required cryptographic step
- CWE-326: Inadequate encryption strength
- CWE-327: Use of a broken or risky cryptographic algorithm
- CWE-328: Reversible one-way hash
- CWE-329: Not using a random IV with CBC mode
- CWE-330: Use of insufficiently random values
- CWE-331: Insufficient entropy
- CWE-332: Insufficient entropy in PRNG
- CWE-334: Small space of random values
- CWE-335: Incorrect usage of seeds in PRNG
- CWE-336: Same seed in PRNG
- CWE-337: Predictable seed in PRNG
- CWE-338: Use of a cryptographically weak PRNG
- CWE-340: Generation of predictable numbers or identifiers
- CWE-342: Predictable exact value from previous values
- CWE-347: Improper verification of cryptographic signature
- CWE-523: Unprotected transport of credentials
- CWE-757: Selection of less-secure algorithm (downgrade)
- CWE-759: One-way hash without a salt
- CWE-760: One-way hash with a predictable salt
- CWE-780: Use of RSA without OAEP
- CWE-916: Password hash with insufficient computational effort
- CWE-1240: Cryptographic primitive with risky implementation
- CWE-1241: Predictable algorithm in RNG

## Test Procedure

1. **TLS/cipher suites.** Use `openssl s_client` and `nmap --script ssl-enum-ciphers`. Check for 3DES, RC4, anonymous ciphers, and protocol downgrade. If the server accepts a weak cipher, attempt a full weak handshake to prove the downgrade (CWE-757/327/326).
2. **HSTS.** Confirm `Strict-Transport-Security: max-age>=31536000; includeSubDomains; preload`. Absence on HTTPS is a finding.
3. **Cleartext sensitive data.** Capture login, password reset, payment, PII flows. Look for `password`, `token`, `ssn` fields in URL, body, headers. If present in cleartext, flag CWE-319/523.
4. **Password hashing strength.** Trigger a password reset or registration flow. If the response reveals a hash, identify the algorithm by length and format. Flag MD5, SHA-1, unsalted SHA-256, and fast bcrypt (cost < 10) for CWE-759/916/760.
5. **Tokens/JWTs.** Capture every JWT/bearer/auth token. Decode without signature. Check `alg` (none, HS256 with weak key, RS256 with wrong key type). For key recovery or forgery, test `alg=none`, weak HS256 keys, and HS/RS key-type confusion (CWE-321/916/347).
6. **Randomness.** Sample session tokens, OTPs, reset codes, file upload names. Run about 20 samples and look for patterns, low-bit patterns, or predictable timestamps (CWE-330-342/1241).
7. **Hard-coded keys.** Search JS bundles, response bodies, URLs, and logs for credential-shaped values (CWE-321).
8. **Signature verification.** Confirm the server validates JWT signatures and SRI integrity on third-party scripts (CWE-347).

## Validation / Negative Control

- A weak-cipher finding requires a completed weak handshake, not just a banner.
- A hard-coded-key finding requires the key to be a live secret in scope, not an intentionally public client identifier.
- A weak-hash finding requires an offline crack or rainbow-lookup match, not just the hash being visible.

## See Also

- `owasp-top10-2025-testing` - parent skill (scope, reporting, full CWE reference).

## CWE Sub-Skills

Each mapped CWE has a dedicated sub-skill with focused detection steps, example findings, and expected impact. Load the relevant sub-skill via `skill_view(name)` when a finding or test case matches one of these.

| CWE | Sub-skill |
|---|---|
| CWE-261 | `cwe-261-weak-password-encoding` |
| CWE-296 | `cwe-296-improper-cert-chain-trust` |
| CWE-319 | `cwe-319-cleartext-transmission` |
| CWE-320 | `cwe-320-key-management-errors` |
| CWE-321 | `cwe-321-hardcoded-cryptographic-key` |
| CWE-322 | `cwe-322-key-exchange-no-identity` |
| CWE-323 | `cwe-323-reused-nonce-keypair` |
| CWE-324 | `cwe-324-key-past-expiration` |
| CWE-325 | `cwe-325-missing-crypto-step` |
| CWE-326 | `cwe-326-inadequate-encryption-strength` |
| CWE-327 | `cwe-327-broken-risky-algorithm` |
| CWE-328 | `cwe-328-reversible-one-way-hash` |
| CWE-329 | `cwe-329-static-iv-cbc` |
| CWE-330 | `cwe-330-insufficient-randomness` |
| CWE-331 | `cwe-331-insufficient-entropy` |
| CWE-332 | `cwe-332-insufficient-rng-entropy` |
| CWE-334 | `cwe-334-small-random-space` |
| CWE-335 | `cwe-335-incorrect-prng-seed` |
| CWE-336 | `cwe-336-same-prng-seed` |
| CWE-337 | `cwe-337-predictable-prng-seed` |
| CWE-338 | `cwe-338-weak-prng` |
| CWE-340 | `cwe-340-predictable-identifiers` |
| CWE-342 | `cwe-342-predictable-from-previous` |
| CWE-347 | `cwe-347-improper-signature-verification` |
| CWE-523 | `cwe-523-unprotected-credential-transport` |
| CWE-757 | `cwe-757-algorithm-downgrade` |
| CWE-759 | `cwe-759-hash-without-salt` |
| CWE-760 | `cwe-760-hash-predictable-salt` |
| CWE-780 | `cwe-780-rsa-without-oaep` |
| CWE-916 | `cwe-916-weak-password-hash-cost` |
| CWE-1240 | `cwe-1240-risky-crypto-implementation` |
| CWE-1241 | `cwe-1241-predictable-rng-algorithm` |