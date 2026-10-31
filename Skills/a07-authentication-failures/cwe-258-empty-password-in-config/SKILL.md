
name: cwe-258-empty-password-in-config
description: Use when a web auth flaw matches cwe-258.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-258, authentication, a07, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a07-authentication-failures
---

# CWE-258 - Empty Password in Configuration File

CWE-258: a configuration file contains a service account with an empty password, allowing login to that account without a password.

## Parent Skill

This is a sub-skill of `owasp-a07-authentication-failures` (OWASP A07 Authentication Failures, Top 10 2025).
Load the parent for overall A07 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-258 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When a service account (DB, app, admin) has an empty password in a config file.

## Detection & Test

1. **Find the config file.** Locate configuration with service credentials (DB, app, admin panels).
2. **Check the password field.** Confirm it is empty or a blank placeholder.
3. **Attempt login.** Use the service account with no password to log in.
4. **Confirm access.** Verify the account grants access to its intended service.
5. **Document the config, account, and proof.

## Example Findings

- A DB config with `user=root` and an empty password.
- An app config with `service_password=` left blank.

## Impact

- Unauthorized access through the authentication bypass.
- Session hijack or account takeover via the auth defect.
- Persistence until the auth flow is corrected (rotation, rate limit, MFA).
- Lateral impact when the same auth flaw repeats across endpoints.

## See Also

- `owasp-a07-authentication-failures` - parent skill (A07 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).