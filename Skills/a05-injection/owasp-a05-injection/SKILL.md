
name: owasp-a05-injection
description: Use when testing A05 Injection in web app parameters.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [owasp, top10-2025, a05, injection, cwe, pentest]
category: pentesting-skills
related_skills:
  - owasp-top10-2025-testing
---

# A05 - Injection

OWASP Top 10 2025 category A05 (down from #3 in 2021). The highest-CVE-count category. Covers SQLi, XSS, command injection, LDAP, XPath, template, and code injection. The parent skill `owasp-top10-2025-testing` holds scope, reporting, and the full CWE reference.

## When to Use
- Testing any string parameter, header, or body field for SQLi, command, code, XSS, LDAP, XPath, or template injection.

## Mapped CWEs (37)

- CWE-20: Improper input validation
- CWE-74: Improper neutralization of special elements (injection, general)
- CWE-76: Improper neutralization of equivalent special elements
- CWE-77: Command injection
- CWE-78: OS command injection
- CWE-79: Cross-site scripting (XSS)
- CWE-80: Basic XSS (HTML tags)
- CWE-83: XSS in attributes
- CWE-86: Invalid characters in identifiers
- CWE-88: Argument injection
- CWE-89: SQL injection
- CWE-90: LDAP injection
- CWE-91: XML / XPath injection
- CWE-93: CRLF injection
- CWE-94: Code injection
- CWE-95: Eval injection
- CWE-96: Static code injection
- CWE-97: Server-side include (SSI) injection
- CWE-98: PHP remote file inclusion
- CWE-99: Resource injection
- CWE-103 / CWE-104: Struts validation deficiencies
- CWE-112: Missing XML validation
- CWE-113: CRLF injection / HTTP response splitting
- CWE-114: Process control
- CWE-115: Misinterpretation of output
- CWE-116: Improper encoding or escaping of output
- CWE-129: Improper validation of array index
- CWE-159: Improper handling of invalid special elements
- CWE-470: Unsafe reflection
- CWE-493 / CWE-500: Public variable without final
- CWE-564: SQL Injection: Hibernate
- CWE-610: JNDI-style / resource injection
- CWE-643: XPath injection
- CWE-644: HTTP header scripting syntax injection
- CWE-917: Expression language injection

## Test Procedure

1. **SQL injection.** For every parameter: `'`, `"`, `; --`, `,`, `AND 1=1` vs `AND 1=2`, `ORDER BY 1`, `UNION SELECT NULL`. Use time-based and blind checks. Confirm blind with an out-of-band callback (CWE-89/564/610).
2. **Command / argument injection.** `; sleep 5`, `$(sleep 5)`, `\`sleep 5\``, `| sleep 5`, `\n sleep 5`. Confirm by time delay or file write (CWE-77/78/88).
3. **Template / SSTI.** `{{7*7}}`, `${7*7}}`, `{{config}}`, `{{''.__class__}}` for Jinja2-style. Confirm by evaluating a known expression (CWE-94/95).
4. **XSS.** Reflected (param echo), stored (profile/comments/upload), DOM (location.hash/search, message handlers). Note context: HTML body, attribute, JavaScript, or template (CWE-79/80/83).
5. **LDAP.** `*` in a search field; `))` and `(&` in filter fields (CWE-90).
6. **XPath.** `//` and `::attribute::` in query fields (CWE-91/643).
7. **CRLF / response splitting.** `\r\nSet-Cookie: pwned=1` and `\r\nX-Injection: 1` into headers and redirect Location (CWE-93/113).
8. **SSTI / EL injection.** Expression language: `#{7*7}`, `${7*7}` (CWE-917).
9. **Log injection.** `\n2025-01-01 00:00:00 INFO /login` in a field; if it appears in a log or later response, log-injection is present (adjacent to A09).
10. **JNDI / resource injection.** LDAP/RMI URLs in logged or error-echoed params where the stack resolves them (CWE-610).

## Validation / Negative Control

- A blind or true-injection finding requires a marker (OOB callback, data echo, file read) - not a 500 alone.
- A negative control: send a value that must be treated as a string; confirm no error and no side effect.
- Do not file a 500 as a finding without showing the actual defect (stack trace, data leak, or controlled output).

## See Also

- `owasp-top10-2025-testing` - parent skill (scope, reporting, full CWE reference).

## CWE Sub-Skills

Each mapped CWE has a dedicated sub-skill with focused detection steps, example findings, and expected impact. Load the relevant sub-skill via `skill_view(name)` when a finding or test case matches one of these.

| CWE | Sub-skill |
|---|---|
| CWE-20 | `cwe-20-improper-input-validation` |
| CWE-74 | `cwe-74-injection-general` |
| CWE-76 | `cwe-76-improper-equivalent-neutralization` |
| CWE-77 | `cwe-77-command-injection` |
| CWE-78 | `cwe-78-os-command-injection` |
| CWE-79 | `cwe-79-cross-site-scripting` |
| CWE-80 | `cwe-80-basic-xss-html-tags` |
| CWE-83 | `cwe-83-xss-in-attributes` |
| CWE-86 | `cwe-86-invalid-chars-in-identifiers` |
| CWE-88 | `cwe-88-argument-injection` |
| CWE-89 | `cwe-89-sql-injection` |
| CWE-90 | `cwe-90-ldap-injection` |
| CWE-91 | `cwe-91-xml-xpath-injection` |
| CWE-93 | `cwe-93-crlf-injection` |
| CWE-94 | `cwe-94-code-injection` |
| CWE-95 | `cwe-95-eval-injection` |
| CWE-96 | `cwe-96-static-code-injection` |
| CWE-97 | `cwe-97-ssi-injection` |
| CWE-98 | `cwe-98-php-rfi` |
| CWE-99 | `cwe-99-resource-injection` |
| CWE-103 | `cwe-103-struts-1-validation` |
| CWE-104 | `cwe-104-struts-2-validation` |
| CWE-112 | `cwe-112-missing-xml-validation` |
| CWE-113 | `cwe-113-crlf-response-splitting` |
| CWE-114 | `cwe-114-process-control` |
| CWE-115 | `cwe-115-misinterpretation-of-output` |
| CWE-116 | `cwe-116-improper-encoding-escaping` |
| CWE-129 | `cwe-129-array-index-out-of-bounds` |
| CWE-159 | `cwe-159-improper-invalid-special-element` |
| CWE-470 | `cwe-470-unsafe-reflection` |
| CWE-493 | `cwe-493-public-method-without-final` |
| CWE-500 | `cwe-500-public-static-field-not-marked-final` |
| CWE-564 | `cwe-564-hibernate-sql-injection` |
| CWE-610 | `cwe-610-jndi-injection` |
| CWE-643 | `cwe-643-xpath-injection` |
| CWE-644 | `cwe-644-http-header-scripting-syntax` |
| CWE-917 | `cwe-917-expression-language-injection` |