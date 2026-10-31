
name: owasp-a08-software-data-integrity
description: Use when testing A08 Integrity Failures on web.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [owasp, top10-2025, a08, integrity, cwe, pentest]
category: pentesting-skills
related_skills:
  - owasp-top10-2025-testing
---

# A08 - Software or Data Integrity Failures

OWASP Top 10 2025 category A08 (same rank as 2021). Low-level trust-boundary enforcement: deserialization, mass assignment, code integrity, and unvalidated cookies/signatures. The parent skill `owasp-top10-2025-testing` holds scope, reporting, and the full CWE reference.

## When to Use
- When an app accepts serialized data, trusts client-modified object attributes, loads unsigned third-party code, or treats cookies/tokens as self-attesting.

## Mapped CWEs (14)

- CWE-345: Insufficient verification of data authenticity
- CWE-353: Missing support for integrity check
- CWE-426: Untrusted search path
- CWE-427: Uncontrolled search path element
- CWE-494: Download of code without integrity check
- CWE-502: Deserialization of untrusted data
- CWE-506: Embedded malicious code
- CWE-509: Replicating malicious code
- CWE-565: Reliance on cookies without validation and integrity checking
- CWE-784: Cookies without validation in a security decision
- CWE-829: Functionality from untrusted control sphere
- CWE-830: Web functionality from an untrusted source
- CWE-915: Improperly controlled modification of dynamically-determined object attributes (mass assignment)
- CWE-926: Improper export of Android application components

## Test Procedure

1. **Mass assignment.** For every create/update endpoint, add privileged fields to the body (`role`, `isAdmin`, `balance`, `ownerId`, `status`); verify persistence by reading the object back (CWE-915).
2. **Deserialization.** Identify endpoints accepting serialized data (Java, .NET, PHP unserialize, Ruby marshal, Python pickle); send stack-appropriate gadget payloads; require a concrete impact (CWE-502).
3. **Code integrity.** Third-party scripts loaded without SRI; replace an asset hash and observe client acceptance (CWE-494/353).
4. **Cookie integrity.** Tamper with signed/encoded auth/CSRF cookies; confirm whether the server re-validates (CWE-565/784). ViewState MAC validation failures are informational only per the checklist convention.
5. **postMessage / origin.** Check `event.origin` validation on message handlers; open handlers to `*` are a finding (CWE-830/346-adjacent).
6. **Download integrity.** Import/download endpoints returning unsigned, unvalidated artifacts (CWE-494).
7. **Search path trust.** Where relevant, check for untrusted PATH or include dirs (CWE-426/427).

## Validation / Negative Control

- Mass assignment proven by persistence plus read-back, not just the request being accepted.
- Deserialization proven by concrete RCE, auth bypass, or data read - never by a deserializer 500 alone.
- Cookie-tamper findings require the tampered value to change a security decision.

## See Also

- `owasp-top10-2025-testing` - parent skill (scope, reporting, full CWE reference).

## CWE Sub-Skills

Each mapped CWE has a dedicated sub-skill with focused detection steps, example findings, and expected impact. Load the relevant sub-skill via `skill_view(name)` when a finding or test case matches one of these.

| CWE | Sub-skill |
|---|---|
| CWE-345 | `cwe-345-insufficient-verification-of-data-authenticity` |
| CWE-353 | `cwe-353-missing-support-for-integrity-check` |
| CWE-426 | `cwe-426-untrusted-search-path` |
| CWE-427 | `cwe-427-uncontrolled-search-path-element` |
| CWE-494 | `cwe-494-download-of-code-without-integrity-check` |
| CWE-502 | `cwe-502-deserialization-of-untrusted-data` |
| CWE-506 | `cwe-506-embedded-malicious-code` |
| CWE-509 | `cwe-509-replicating-malicious-code` |
| CWE-565 | `cwe-565-reliance-on-cookies-without-validation-and-integrity-checking` |
| CWE-784 | `cwe-784-cookies-without-validation-in-a-security-decision` |
| CWE-829 | `cwe-829-functionality-from-untrusted-control-sphere` |
| CWE-830 | `cwe-830-web-functionality-from-an-untrusted-source` |
| CWE-915 | `cwe-915-improperly-controlled-modification-of-dynamically-determined-object-attributes` |
| CWE-926 | `cwe-926-improper-export-of-android-application-components` |