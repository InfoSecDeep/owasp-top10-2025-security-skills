
name: owasp-a10-exceptional-conditions
description: Use when web-testing A10 Exceptional Conditions.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [owasp, top10-2025, a10, exceptions, cwe, pentest]
category: pentesting-skills
related_skills:
  - owasp-top10-2025-testing
---

# A10 - Mishandling of Exceptional Conditions

OWASP Top 10 2025 category A10 (new in the 2025 edition). Improper error handling, failing open, and behavior on abnormal conditions: missing/extra parameters, edge values, and unhandled states. The parent skill `owasp-top10-2025-testing` holds scope, reporting, and the full CWE reference.

## When to Use
- Boundary and error-path testing on any endpoint; verifying that security controls fail closed, not open.

## Mapped CWEs (24)

- CWE-209: Error message containing sensitive information
- CWE-215: Sensitive information in debugging code
- CWE-234: Failure to handle missing parameter
- CWE-235: Improper handling of extra parameters
- CWE-248: Uncaught exception
- CWE-252: Unchecked return value
- CWE-274: Improper handling of insufficient privileges
- CWE-280: Improper handling of insufficient permissions
- CWE-369: Divide by zero
- CWE-390: Detection of error condition without action
- CWE-391: Unchecked error condition
- CWE-394: Unexpected status code or return value
- CWE-396: Catch for generic exception
- CWE-397: Throws for generic exception
- CWE-460: Improper cleanup on thrown exception
- CWE-476: NULL pointer dereference
- CWE-478: Missing default case in multi-branch expression
- CWE-484: Omitted break in switch
- CWE-550: Server-generated error message containing sensitive information
- CWE-636: Not failing securely (failing open)
- CWE-703: Improper check or handling of exceptional conditions
- CWE-754: Improper check for unusual or exceptional conditions
- CWE-755: Improper handling of exceptional conditions
- CWE-756: Missing custom error page

## Test Procedure

1. **Boundary sweep** on every parameter: missing, extra unknown, wrong type, empty, max-length, max+1, unicode, negative, zero, null (CWE-234/235/129).
2. **Error disclosure.** Read error responses for stack traces, file paths, class names, DB names, and version numbers (CWE-209/550).
3. **Failing open.** For each security control (authorization check, rate limit, signature check, file validation), force the underlying failure with an in-scope bad input; if the default action is to allow the request, flag CWE-636.
4. **Cleanup on exception.** Trigger errors mid-flow (upload, transfer, write); observe inconsistent state - partial file, orphaned record, queued-but-unprocessed job (CWE-460).
5. **Undefined states.** Send enum/state parameters with values outside the documented set; undefined-but-predictable behavior flags CWE-478/484-class weaknesses.
6. **Default error pages.** Framework default 404/500 pages (Apache, Tomcat, Express) = CWE-756 plus information disclosure.
7. **Crash conditions.** Divide-by-zero, null dereference, and uncaught exception responses (CWE-369/476/248); only findings when they leak internals or break a control.

## Validation / Negative Control

- Error disclosure requires real internal data, not the mere fact that a 500 was returned.
- Failing open requires both the failure condition and the allow-by-default behavior to be demonstrated.
- A 500 without visible internals is an observation, not a finding.

## See Also

- `owasp-top10-2025-testing` - parent skill (scope, reporting, full CWE reference).
- `dogfood` (exploratory triggering), (error captures), (when loaded).

## CWE Sub-Skills

Each mapped CWE has a dedicated sub-skill with focused detection steps, example findings, and expected impact. Load the relevant sub-skill via `skill_view(name)` when a finding or test case matches one of these.

| CWE | Sub-skill |
|---|---|
| CWE-209 | `cwe-209-error-message-containing-sensitive-information` |
| CWE-215 | `cwe-215-sensitive-information-in-debugging-code` |
| CWE-234 | `cwe-234-failure-to-handle-missing-parameter` |
| CWE-235 | `cwe-235-improper-handling-of-extra-parameters` |
| CWE-248 | `cwe-248-uncaught-exception` |
| CWE-252 | `cwe-252-unchecked-return-value` |
| CWE-274 | `cwe-274-improper-handling-of-insufficient-privileges` |
| CWE-280 | `cwe-280-improper-handling-of-insufficient-permissions` |
| CWE-369 | `cwe-369-divide-by-zero` |
| CWE-390 | `cwe-390-detection-of-error-condition-without-action` |
| CWE-391 | `cwe-391-unchecked-error-condition` |
| CWE-394 | `cwe-394-unexpected-status-code-or-return-value` |
| CWE-396 | `cwe-396-catch-for-generic-exception` |
| CWE-397 | `cwe-397-throws-for-generic-exception` |
| CWE-460 | `cwe-460-improper-cleanup-on-thrown-exception` |
| CWE-476 | `cwe-476-null-pointer-dereference` |
| CWE-478 | `cwe-478-missing-default-case-in-multi-branch-expression` |
| CWE-484 | `cwe-484-omitted-break-in-switch` |
| CWE-550 | `cwe-550-server-generated-error-message-containing-sensitive-information` |
| CWE-636 | `cwe-636-not-failing-securely` |
| CWE-703 | `cwe-703-improper-check-or-handling-of-exceptional-conditions` |
| CWE-754 | `cwe-754-improper-check-for-unusual-or-exceptional-conditions` |
| CWE-755 | `cwe-755-improper-handling-of-exceptional-conditions` |
| CWE-756 | `cwe-756-missing-custom-error-page` |