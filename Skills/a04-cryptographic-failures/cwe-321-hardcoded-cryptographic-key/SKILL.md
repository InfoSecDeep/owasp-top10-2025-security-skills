
name: cwe-321-hardcoded-cryptographic-key
description: Use when testing CWE-321 crypto weakness on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, owasp, a04, crypto, pentest]
category: pentesting-skills
related_skills:
  - owasp-a04-cryptographic-failures
---

# Use of Hard-Coded Cryptographic Key

CWE-321: Use of Hard-Coded Cryptographic Key occurs when a key, IV, MAC key, or signing secret is embedded directly in source, config, JS bundles, or responses instead of being managed through a KMS, environment, or vault. Anyone who can read the artifact can use the key offline.

## Parent Skill

This is a sub-skill of `owasp-a04-cryptographic-failures` (OWASP A04 Cryptographic Failures, Top 10 2025). Load the parent for overall A04 scope, the test procedure, and validation criteria (negative control). This skill covers the CWE-321 detail: what to look for, how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a key, IV, MAC key, or signing secret is embedded in code, config, JS bundles, or API responses instead of a KMS or environment variable.

## Detection & Test

1. **Client-side search.** Grep JS bundles, HTML, and inline scripts for key-shaped constants: `apiKey`, `api_key`, `secret`, `token`, `iv`, `aes`, `des`, `rsa`, `EC_KEY`, `X-Api-Key`, base64 blobs >= 16 bytes, and hex strings of length 16/32/64.
2. **Server responses.** Search response bodies, headers, error messages, and debug pages for the same patterns. A key returned in an error body is a hard leak.
3. **Config and .env.** Fetch `/config.js`, `/env.js`, `/config.json`, `.env`, `.env.backup`, `.env.prod`, `.env.local`, `phpinfo.php`, and `server-status` to look for embedded secrets.
4. **Prove liveness.** Confirm the key is live: use it against an in-scope API, decrypt a captured encrypted response, or forge a signed cookie with it. A key in the bundle but unused server-side is not yet a finding.
5. **Version control.** If source is reachable (via a source-map, debug endpoint, or leaked .git), search commit history for key changes and revocation.

## Example Findings

- `const API_KEY = 'sk_live_51H7...'` in a public JS bundle.
- `Authorization: Bearer eyJ...` header with a hardcoded `secret` field in a response.
- `/config.json` returns `{ "db_password": "...", "jwt_secret": "..." }`.
- An error page shows `Expected key: 9f86d081884c7d65...`

## Impact

- Offline or network capture of secrets the algorithm is meant to protect.
- Forgery or decryption without the private key/secret.
- Persistence until the algorithm or keys are rotated.
- Lateral movement when the same weakness repeats across services.

## See Also

- `owasp-a04-cryptographic-failures` - parent skill (A04 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).