
name: owasp-a06-insecure-design
description: Use when testing A06 Insecure Design on a web app.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [owasp, top10-2025, a06, design, cwe, pentest]
category: pentesting-skills
related_skills:
  - owasp-top10-2025-testing
---

# A06 - Insecure Design

OWASP Top 10 2025 category A06 (down from #4 in 2021). Design-level weaknesses: trust boundaries, business logic, race conditions, upload handling, and excessive attack surface. The parent skill `owasp-top10-2025-testing` holds scope, reporting, and the full CWE reference.

## When to Use
- Validating business-logic flows, pricing, state machines, or upload handling.
- Suspecting trust-boundary abuse (client-supplied state fields) or HTTP layer interpretation conflicts.

## Mapped CWEs (39)

- CWE-73: External control of file name or path
- CWE-183: Permissive list of allowed inputs
- CWE-256: Unprotected storage of credentials
- CWE-266: Incorrect privilege assignment
- CWE-269: Improper privilege management
- CWE-286: Incorrect user management
- CWE-311: Missing encryption of sensitive data
- CWE-312 / CWE-313 / CWE-316: Cleartext storage in memory/file/disk
- CWE-362: Race condition / TOCTOU
- CWE-382: J2EE use of System.exit()
- CWE-419: Unprotected primary channel
- CWE-434: Unrestricted upload of dangerous file type
- CWE-436: Interpretation conflict
- CWE-444: HTTP request smuggling
- CWE-451: User interface issues
- CWE-454: External initialization of trusted variables
- CWE-472: External control of assumed-immutable web parameter
- CWE-501: Trust boundary violation
- CWE-522: Insufficiently protected credentials
- CWE-525 / CWE-539: Sensitive data in browser cache / persistent cookies
- CWE-598: Sensitive data in GET query strings
- CWE-602: Client-side enforcement of server-side security
- CWE-628: Function call with incorrect arguments
- CWE-642: External control of critical state data
- CWE-646: Reliance on file name/extension of externally-supplied file
- CWE-653: Insufficient compartmentalization
- CWE-656: Reliance on security through obscurity
- CWE-657: Violation of secure design principles
- CWE-676: Use of potentially dangerous function
- CWE-693: Protection mechanism failure
- CWE-799: Improper control of interaction frequency
- CWE-807: Untrusted input in a security decision
- CWE-841: Improper enforcement of behavioral workflow
- CWE-1021: Improper restriction of rendered UI layers/frames
- CWE-1022: Web link to untrusted target with window.opener access
- CWE-1125: Excessive attack surface

## Test Procedure

1. **Race conditions.** Parallel requests with conflicting amounts against checkout, redemption, upload, transfer; total differing from a sequential baseline proves the defect (CWE-362).
2. **Trust boundaries.** Map every boundary (client-API, API-DB, API-cloud, API-3rd-party); confirm identity/origin/signature is verified server-side; flag client-set fields the server should own - prices, roles, balances (CWE-501/642).
3. **Business logic.** Negative/zero/huge amounts, scientific notation, unicode; skipped or rewound workflow steps; duplicate submissions.
4. **Uploads.** Dangerous types (.php/.phtml/.html/.svg), double extensions, MIME mismatch; verify where files land and how they are served (CWE-434/646/73).
5. **HTTP smuggling.** CL.TE / TE.CL mismatch against the frontend proxy; confirm with a state marker (CWE-444/436).
6. **Rate limiting.** Sustained requests against auth, OTP, and API endpoints; absence of 429/lockout is a design failure (CWE-799).
7. **Excessive surface.** Enumerate debug endpoints, admin tools, legacy APIs; require justification for each to be in production (CWE-1125).
8. **UI layers.** Clickjacking via X-Frame-Options/frame-ancestors; window.opener leaks to external targets (CWE-1021/1022).
9. **Client-side enforcement.** Disable JS and replay privileged actions; anything working without server-side checks is a finding (CWE-602).

## Validation / Negative Control

- Race is proven by measurable delta, not timing noise.
- Smuggling is proven by a state merge between requests.
- An upload is only a finding when it is served or executable at an attacker-reachable path.

## See Also

- `owasp-top10-2025-testing` - parent skill (scope, reporting, full CWE reference).

## CWE Sub-Skills

Each mapped CWE has a dedicated sub-skill with focused detection steps, example findings, and expected impact. Load the relevant sub-skill via `skill_view(name)` when a finding or test case matches one of these.

| CWE | Sub-skill |
|---|---|
| CWE-73 | `cwe-73-external-control-of-file-name` |
| CWE-183 | `cwe-183-permissive-list-of-allowed-inputs` |
| CWE-256 | `cwe-256-unprotected-storage-of-credentials` |
| CWE-266 | `cwe-266-incorrect-privilege-assignment` |
| CWE-269 | `cwe-269-improper-privilege-management` |
| CWE-286 | `cwe-286-incorrect-user-management` |
| CWE-311 | `cwe-311-missing-encryption-of-sensitive-data` |
| CWE-312 | `cwe-312-cleartext-storage-in-memory` |
| CWE-313 | `cwe-313-cleartext-storage-in-file-disk` |
| CWE-316 | `cwe-316-cleartext-storage-in-browser-cache` |
| CWE-362 | `cwe-362-race-condition-toctou` |
| CWE-382 | `cwe-382-j2ee-use-of-system-exit` |
| CWE-419 | `cwe-419-unprotected-primary-channel` |
| CWE-434 | `cwe-434-unrestricted-upload-of-dangerous-file` |
| CWE-436 | `cwe-436-interpretation-conflict` |
| CWE-444 | `cwe-444-http-request-smuggling` |
| CWE-451 | `cwe-451-user-interface-issues` |
| CWE-454 | `cwe-454-external-initialization-of-trusted-variable` |
| CWE-472 | `cwe-472-external-control-of-assumed-immutable-web-parameter` |
| CWE-501 | `cwe-501-trust-boundary-violation` |
| CWE-522 | `cwe-522-insufficiently-protected-credentials` |
| CWE-525 | `cwe-525-sensitive-data-in-browser-cache` |
| CWE-539 | `cwe-539-sensitive-data-in-persistent-cookies` |
| CWE-598 | `cwe-598-sensitive-data-in-get-query-string` |
| CWE-602 | `cwe-602-client-side-enforcement-of-server-side-security` |
| CWE-628 | `cwe-628-function-call-with-incorrect-arguments` |
| CWE-642 | `cwe-642-external-control-of-critical-state-data` |
| CWE-646 | `cwe-646-reliance-on-file-name-extension-of-external-file` |
| CWE-653 | `cwe-653-insufficient-compartmentalization` |
| CWE-656 | `cwe-656-reliance-on-obscurity` |
| CWE-657 | `cwe-657-violation-of-secure-design-principles` |
| CWE-676 | `cwe-676-use-of-dangerous-function` |
| CWE-693 | `cwe-693-protection-mechanism-failure` |
| CWE-799 | `cwe-799-improper-control-of-interaction-frequency` |
| CWE-807 | `cwe-807-untrusted-input-in-security-decision` |
| CWE-841 | `cwe-841-improper-enforcement-of-behavioral-workflow` |
| CWE-1021 | `cwe-1021-improper-restriction-of-rendered-ui-layers` |
| CWE-1022 | `cwe-1022-web-link-to-untrusted-target-with-window-opener` |
| CWE-1125 | `cwe-1125-excessive-attack-surface` |