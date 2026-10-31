
name: cwe-347-improper-signature-verification
description: Use when testing CWE-347 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Improper Verification of Cryptographic Signature

CWE-347: Improper Verification of Cryptographic Signature occurs when a consumer accepts a signature that is missing, tampered, or forged - e.g. accepting `alg:none`, trusting the public key, or validating a tampered signed payload against the old signature.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-347 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a signature-bearing token (JWT, SRI, signed cookie) may not be validated, or the algorithm is bypassable.

## Detection & Test

1. **Token signature (JWT).** Set `alg:none`; flip `iss`/`role`/`sub` and replay; try key confusion (RS256 header with a public key as HMAC secret).
2. **Cookie signature.** Tamper the payload and check whether the server re-signs vs. rejects.
3. **SRI.** Remove/alter an integrity attribute and confirm the resource is still loaded.
4. **Old signature acceptance.** Replace a token with an older captured one and see if the new signature is ignored.
5. **Prove impact.** Recover privileged data, bypass authz, or forge a claim.

## Example Findings

- `alg: none` JWT accepted as valid.
- RS256 token forged with the public key as the HMAC secret.
- SRI integrity attribute stripped, resource still executes.
- Tampered signed cookie re-accepted (server ignores the new signature).

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).