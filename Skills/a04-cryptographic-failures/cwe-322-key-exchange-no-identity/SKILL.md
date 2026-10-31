
name: cwe-322-key-exchange-no-identity
description: Use when testing CWE-322 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Key Exchange Without Entity Authentication

CWE-322: Key Exchange Without Entity Authentication occurs when a symmetric key or secret is established but the other party's identity is not authenticated, allowing a man-in-the-middle to impersonate either side.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-322 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a shared secret/key is negotiated without verifying the identity of the endpoint (anonymous key exchange).

## Detection & Test

1. **Identify key negotiation.** Find TLS sessions, pre-shared-key setups, or custom secret exchanges.
2. **Check authentication.** Confirm the peer identity is bound to the key (client certs, PSK identity validation, mutual auth).
3. **Probe anonymous exchange.** Attempt anonymous ciphers (ADH) or observe if the server authenticates the client before the handshake completes.
4. **MITM simulate.** If no mutual auth, impersonate a peer and complete the exchange.
5. **Confirm.** Recover a value protected only by the negotiated key.

## Example Findings

- ADH anonymous cipher accepted => MITM decrypts the session.
- Pre-shared-key established without validating the PSK identity.
- Custom key exchange where the server accepts an unauthenticated peer.

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).