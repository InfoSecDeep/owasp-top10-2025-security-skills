
name: owasp-a02-security-misconfiguration
description: Use when testing A02 Security Misconfiguration on web.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [owasp, top10-2025, a02, misconfiguration, cwe, pentest]
category: pentesting-skills
related_skills:
  - owasp-top10-2025-testing
---

# A02 - Security Misconfiguration

OWASP Top 10 2025 category A02 (up from #5 in 2021). Covers defaults, debug surfaces, exposed config, XXE, and permissive policies. The parent skill `owasp-top10-2025-testing` holds scope, reporting, and the full CWE reference.

## When to Use
- Checking security headers and cookies, default/debug endpoints, XXE, or cross-domain policies on a web target.

## Mapped CWEs (16)

- CWE-5: J2EE misconfiguration - data transmission without encryption
- CWE-11: ASP.NET misconfiguration - creating debug binary
- CWE-13: ASP.NET misconfiguration - password in config file
- CWE-15: External control of system or configuration setting
- CWE-16: Configuration
- CWE-260: Password in configuration file
- CWE-315: Cleartext storage of sensitive information in a cookie
- CWE-489: Active debug code
- CWE-526: Exposure of sensitive information through environmental variables
- CWE-547: Hard-coded security-relevant constants
- CWE-611: Improper restriction of XML External Entity Reference (XXE)
- CWE-614: Sensitive cookie without 'Secure' attribute
- CWE-776: XML Entity Expansion (Billion Laughs)
- CWE-942: Permissive cross-domain policy with untrusted domains
- CWE-1004: Sensitive cookie without 'HttpOnly' flag
- CWE-1174: ASP.NET misconfiguration - improper model validation

## Test Procedure

1. **Defaults and debug surfaces.** Probe /phpinfo.php, /server-status, /server-info, /actuator, /actuator/env, /env, /.env, /.git/config, /debug, /tracing, /metrics, /swagger.json, /api-docs.
2. **Verbose errors.** Send malformed parameters, oversized bodies, wrong Content-Type; read the response for stack traces, file paths, DB names, class names.
3. **Security headers.** Inspect Server, X-Powered-By, X-AspNet-Version, X-Debug-Toolkit, X-Frame-Options, X-Content-Type-Options, Referrer-Policy, Content-Security-Policy, and Strict-Transport-Security.
4. **Cookies.** Read all Set-Cookie attributes; flag missing HttpOnly, Secure, and SameSite (CWE-1004/614/315/1275).
5. **XXE.** On every XML/SOAP/upload endpoint, send an external entity (file:///etc/passwd, file:///etc/hostname) and an out-of-band exfiltration callback. For CWE-776, try a recursive DTD (Billion Laughs) to check DoS potential.
6. **Cross-domain policy.** Retrieve crossdomain.xml and clientaccesspolicy.xml; flag `<allow-access-from domain="*"/>` for CWE-942.
7. **Environment leakage.** Check responses and debug endpoints for env-var dumps (CWE-526).
8. **Hard-coded config.** Search JS bundles and exposed files for security-relevant constants and credentials (CWE-547/CWE-260).

## Validation / Negative Control

- A random unknown URL returns the same default body as the exposed path - this is a catch-all 404 route, not an exposure. Confirm the endpoint is real before filing.
- XXE is confirmed only by an actual file read, OOB callback, or timing - a 500 on malformed XML is not evidence.

## See Also

- `owasp-top10-2025-testing` - parent skill (scope, reporting, full CWE reference).
- `web-security-checklist-workflow` - owning skills for sub-techniques (when loaded).

## CWE Sub-Skills

Each mapped CWE above has a dedicated sub-skill with focused detection steps, example payloads, bypass tricks, and expected impact. Load the relevant sub-skill via `skill_view(name)` when a finding or test case matches one of these.

| CWE | Sub-skill |
|---|---|
| CWE-5 | `cwe-5-j2ee-misconfig-plaintext` |
| CWE-11 | `cwe-11-aspnet-debug-binary` |
| CWE-13 | `cwe-13-aspnet-password-in-config` |
| CWE-15 | `cwe-15-external-control-of-system-config` |
| CWE-16 | `cwe-16-configuration` |
| CWE-260 | `cwe-260-password-in-configuration-file` |
| CWE-315 | `cwe-315-cleartext-cookie` |
| CWE-489 | `cwe-489-active-debug-code` |
| CWE-526 | `cwe-526-env-var-leak` |
| CWE-547 | `cwe-547-hardcoded-security-constant` |
| CWE-611 | `cwe-611-xxe` |
| CWE-614 | `cwe-614-cookie-without-secure` |
| CWE-776 | `cwe-776-billion-laughs` |
| CWE-942 | `cwe-942-permissive-cross-domain-policy` |
| CWE-1004 | `cwe-1004-cookie-without-httponly` |
| CWE-1174 | `cwe-1174-aspnet-improper-model-validation` |