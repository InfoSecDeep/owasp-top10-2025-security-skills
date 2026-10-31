
name: owasp-a07-authentication-failures
description: Use when testing A07 Authentication Failures on web.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [owasp, top10-2025, a07, authentication, cwe, pentest]
category: pentesting-skills
related_skills:
  - owasp-top10-2025-testing
---

# A07 - Authentication Failures

OWASP Top 10 2025 category A07 (same rank as 2021, renamed from Identification and Authentication Failures). Covers brute force, session defects, weak/default credentials, and certificate-channel validation. The parent skill `owasp-top10-2025-testing` holds scope, reporting, and the full CWE reference.

## When to Use
- Testing login, signup, password-reset, or session behavior; or when auth-related tokens, cookies, or channels are in scope.

## Mapped CWEs (36)

- CWE-258: Empty password in configuration file
- CWE-259: Use of hard-coded password
- CWE-287: Improper authentication
- CWE-288: Authentication bypass via alternate path or channel
- CWE-289: Authentication bypass by alternate name (case)
- CWE-290: Authentication bypass by spoofing
- CWE-291: Reliance on IP address for authentication
- CWE-293: Using Referer field for authentication
- CWE-294: Authentication bypass by capture-replay
- CWE-295: Improper certificate validation
- CWE-297 / CWE-298 / CWE-299: Improper certificate validation with host mismatch
- CWE-300: Channel accessible by non-endpoint
- CWE-302: Authentication bypass by assumed-immutable data
- CWE-303: Incorrect implementation of authentication algorithm
- CWE-304: Missing critical step in authentication
- CWE-305: Authentication bypass by primary weakness
- CWE-306: Missing authentication for critical function
- CWE-307: Improper restriction of excessive authentication attempts
- CWE-308 / CWE-309: Single-factor / password-system as primary authentication
- CWE-346: Origin validation error
- CWE-350: Reliance on reverse DNS for security-critical action
- CWE-384: Session fixation
- CWE-521: Weak password requirements
- CWE-613: Insufficient session expiration
- CWE-620: Unverified password change
- CWE-640: Weak password recovery mechanism
- CWE-798: Use of hard-coded credentials
- CWE-940: Improper verification of source of a communication channel
- CWE-941: Incorrectly specified destination in a channel
- CWE-1390: Weak authentication
- CWE-1391: Use of weak credentials
- CWE-1392: Use of default credentials
- CWE-1393: Use of default password

## Test Procedure

1. **Brute force / rate limits.** Bounded burst of failed logins (within scope and rules of engagement); expect 429, lockout, CAPTCHA, or step-up. Absence = CWE-307. WordPress: use the XML-RPC multicall endpoint to amplify a bounded login spray; confirm brute-force resistance (CWE-307).
2. **Username enumeration.** Measure response time and message differences for valid vs invalid usernames/emails; flag when distinguishable and actionable.
3. **Alternate name / case.** admin vs Admin vs ADMIN; email whitespace and case variants (CWE-289).
4. **Session fixation.** Capture the pre-login session ID; log in; replay the same ID after login (CWE-384).
5. **Session expiry.** Idle past the stated timeout, replay the session; expiry must actually invalidate (CWE-613).
6. **Password recovery.** Reset-link IDOR (token +1/-1), guessable or short codes, account disclosure in the flow (CWE-640).
7. **Unverified password change.** Change password with a stolen/interim token; confirm the old account locks out or not (CWE-620).
8. **Default / hard-coded credentials.** Common pairs against login and any admin panel; mine code paths and JS bundles (CWE-1392/1393/259/798).
9. **Replay / capture-replay.** Replay auth headers after logout (CWE-294).
10. **JWT authentication defects.** Decode every token: alg confusion, missing exp, weak secrets (feeds A04/A07 findings).
11. **Channel validation.** HTTP login, missing cert pinning on API clients, Referer- or IP-based auth (CWE-293/291/940/941).

## Validation / Negative Control

- Enumeration must be measurable and distinguishable from generic behavior.
- Fixation requires the same session ID working after login.
- Brute-force absence measured with a bounded burst, not assumed.

## See Also

- `owasp-top10-2025-testing` - parent skill (scope, reporting, full CWE reference).

## CWE Sub-Skills

Each mapped CWE has a dedicated sub-skill with focused detection steps, example findings, and expected impact. Load the relevant sub-skill via `skill_view(name)` when a finding or test case matches one of these.

| CWE | Sub-skill |
|---|---|
| CWE-258 | `cwe-258-empty-password-in-config` |
| CWE-259 | `cwe-259-hard-coded-password` |
| CWE-287 | `cwe-287-improper-authentication` |
| CWE-288 | `cwe-288-auth-bypass-alternate-path` |
| CWE-289 | `cwe-289-auth-bypass-alternate-name` |
| CWE-290 | `cwe-290-auth-bypass-by-spoofing` |
| CWE-291 | `cwe-291-auth-bypass-ip-address` |
| CWE-293 | `cwe-293-auth-bypass-referer-field` |
| CWE-294 | `cwe-294-auth-bypass-capture-replay` |
| CWE-295 / CWE-297 / CWE-298 / CWE-299 | `cwe-295-improper-certificate-validation`, `cwe-297-improper-certificate-host-mismatch`, `cwe-298-improper-verification-of-certificate-with-host-mismatch`, `cwe-299-improper-validation-of-certificate-with-host-mismatch` |
| CWE-300 | `cwe-300-channel-accessible-by-non-endpoint` |
| CWE-302 | `cwe-302-auth-bypass-assumed-immutable-data` |
| CWE-303 | `cwe-303-incorrect-implementation-of-auth-algorithm` |
| CWE-304 | `cwe-304-missing-critical-step-in-authentication` |
| CWE-305 | `cwe-305-auth-bypass-by-primary-weakness` |
| CWE-306 | `cwe-306-missing-auth-for-critical-function` |
| CWE-307 | `cwe-307-improper-restriction-of-excessive-attempts` |
| CWE-308 / CWE-309 | `cwe-308-single-factor-as-primary`, `cwe-309-use-of-password-system-for-primary-authentication` |
| CWE-346 | `cwe-346-origin-validation-error` |
| CWE-350 | `cwe-350-reliance-on-reverse-dns` |
| CWE-384 | `cwe-384-session-fixation` |
| CWE-521 | `cwe-521-weak-password-requirements` |
| CWE-613 | `cwe-613-insufficient-session-expiration` |
| CWE-620 | `cwe-620-unverified-password-change` |
| CWE-640 | `cwe-640-weak-password-recovery-mechanism` |
| CWE-798 | `cwe-798-hard-coded-credentials` |
| CWE-940 | `cwe-940-improper-verification-of-source-channel` |
| CWE-941 | `cwe-941-incorrectly-specified-destination-in-channel` |
| CWE-1390 | `cwe-1390-weak-authentication` |
| CWE-1391 | `cwe-1391-weak-credentials` |
| CWE-1392 | `cwe-1392-default-credentials` |
| CWE-1393 | `cwe-1393-default-password` |