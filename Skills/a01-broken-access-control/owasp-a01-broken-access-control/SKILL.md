
name: owasp-a01-broken-access-control
description: Use when testing A01 Broken Access Control on web.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [owasp, top10-2025, a01, access-control, cwe, pentest]
category: pentesting-skills
related_skills:
  - owasp-top10-2025-testing
---

# A01 - Broken Access Control

OWASP Top 10 2025 category A01. The most serious web app risk (100% of tested apps). SSRF is now absorbed here from the 2021 list (CWE-918). This skill is the per-category focus entry point; the parent skill `owasp-top10-2025-testing` holds scope, reporting, and the full CWE reference.

## When to Use
- Testing authorization: IDOR/BOLA, forced browsing, CSRF, SSRF, open redirect, or access-control bypass on a web target.

## Mapped CWEs (40)

- CWE-22 / CWE-23 / CWE-36: Path traversal (absolute, relative, general)
- CWE-59: Improper link resolution before file access (link following)
- CWE-61: UNIX symbolic link
- CWE-65: Windows hard link
- CWE-200: Exposure of sensitive information to unauthorized actor
- CWE-201: Exposure of sensitive information through sent data
- CWE-219: Sensitive file stored under web root
- CWE-276: Incorrect default permissions
- CWE-281 / CWE-282 / CWE-283: Improper preservation of permissions / ownership / unverified ownership
- CWE-284: Improper access control
- CWE-285: Improper authorization
- CWE-352: Cross-Site Request Forgery (CSRF)
- CWE-359: Exposure of private personal information
- CWE-377 / CWE-379: Insecure temporary file / created with insecure permissions
- CWE-402: Resource leak to new sphere
- CWE-424: Improper protection of alternate path
- CWE-425: Direct request (forced browsing)
- CWE-441: Confused deputy
- CWE-497: Sensitive system information exposure
- CWE-538 / CWE-540: Sensitive info in externally-accessible file / in source
- CWE-548: Exposure through directory listing
- CWE-552: Files/dirs accessible to external parties
- CWE-566: Authorization bypass via user-controlled SQL key (IDOR)
- CWE-601: Open redirect
- CWE-615: Sensitive info in code comments
- CWE-639: Authorization bypass via user-controlled key (BOLA / IDOR)
- CWE-668: Resource in wrong sphere
- CWE-732: Incorrect permission assignment
- CWE-749: Exposed dangerous method/function
- CWE-862: Missing authorization
- CWE-863: Incorrect authorization
- CWE-918: Server-Side Request Forgery (SSRF)
- CWE-922: Insecure storage of sensitive information
- CWE-1275: Sensitive cookie with improper SameSite

## Test Procedure

1. **Identity/role swap (BOLA).** For each in-scope resource or API call, replay with a second identity of lower role and compare data returned. Confirm the server authorizes, not the UI.
2. **ID stepping (IDOR).** Step through IDs (user, order, invoice, doc IDs) using another identity's values.
3. **Verb swap.** For every endpoint try GET, PUT, PATCH, DELETE, OPTIONS, TRACE; flag `Allow` headers listing destructive verbs.
4. **Forced browsing.** Enumerate admin routes: /admin, /console, /api/admin, /debug, /swagger-ui, /actuator. Compare with a random 404 path to rule out a catch-all routing handler.
5. **Path traversal** on every file parameter: ../, %2e%2e%2f, /....//, ..%2f, and ..\ variants.
6. **CSRF.** Find state-changing POST/PUT/DELETE without CSRF token, SameSite, or Origin/Referer check; replay from a foreign origin.
7. **SSRF.** On every URL/fetch/import parameter, test http://169.254.169.254/, file:///etc/passwd, gopher://, dict://, and use a controlled external callback for blind cases.
8. **Open redirect.** Redirect parameters pointing to attacker hosts; observe where the final page lands.
9. **Directory / file exposure.** Check /../ patterns and known debug paths; flag 200s returning files not in the authorized listing.

## Validation / Negative Control

- A random nonexistent path returns 404 or the same shape as a non-authorized resource (rules out catch-all).
- The second identity genuinely lacks the privilege (not just a different status code).
- SSRF is proven by the OOB callback, not by a status code.

## See Also

- `owasp-top10-2025-testing` - parent skill (scope, priority order, reporting template, full 249-CWE reference).

## CWE Sub-Skills

Each mapped CWE has a dedicated sub-skill with focused detection steps, example payloads, and expected impact. Load the relevant sub-skill via `skill_view(name)` when a finding or test case matches one of these.

| CWE | Sub-skill |
|---|---|
| CWE-22 / CWE-23 / CWE-36 | `cwe-22-path-traversal`, `cwe-23-relative-path-traversal`, `cwe-36-absolute-path-traversal` |
| CWE-59 | `cwe-59-improper-link-resolution` |
| CWE-61 | `cwe-61-unix-symbolic-link` |
| CWE-65 | `cwe-65-windows-hard-link` |
| CWE-200 | `cwe-200-sensitive-info-exposure` |
| CWE-201 | `cwe-201-sensitive-info-sent-data` |
| CWE-219 | `cwe-219-sensitive-file-webroot` |
| CWE-276 | `cwe-276-incorrect-default-permissions` |
| CWE-281 / CWE-282 / CWE-283 | `cwe-281-improper-permission-preservation`, `cwe-282-improper-ownership-management`, `cwe-283-unverified-ownership` |
| CWE-284 | `cwe-284-improper-access-control` |
| CWE-285 | `cwe-285-improper-authorization` |
| CWE-352 | `cwe-352-csrf` |
| CWE-359 | `cwe-359-exposure-of-ppi` |
| CWE-377 / CWE-379 | `cwe-377-insecure-temp-file`, `cwe-379-insecure-temp-file-creation` |
| CWE-402 | `cwe-402-resource-wrong-sphere` |
| CWE-424 | `cwe-424-improper-alt-path` |
| CWE-425 | `cwe-425-direct-request` |
| CWE-441 | `cwe-441-confused-deputy` |
| CWE-497 | `cwe-497-system-info-exposure` |
| CWE-538 / CWE-540 | `cwe-538-sensitive-info-external-file`, `cwe-540-sensitive-info-in-source` |
| CWE-548 | `cwe-548-directory-listing` |
| CWE-552 | `cwe-552-files-external-accessible` |
| CWE-566 | `cwe-566-idor-sql-key` |
| CWE-601 | `cwe-601-open-redirect` |
| CWE-615 | `cwe-615-sensitive-info-code-comments` |
| CWE-639 | `cwe-639-bola-idor` |
| CWE-668 | `cwe-668-resource-wrong-sphere` |
| CWE-732 | `cwe-732-incorrect-permission-assignment` |
| CWE-749 | `cwe-749-dangerous-method-exposure` |
| CWE-862 | `cwe-862-missing-authorization` |
| CWE-863 | `cwe-863-incorrect-authorization` |
| CWE-918 | `cwe-918-ssrf` |
| CWE-922 | `cwe-922-insecure-storage` |
| CWE-1275 | `cwe-1275-samesite-cookie` |