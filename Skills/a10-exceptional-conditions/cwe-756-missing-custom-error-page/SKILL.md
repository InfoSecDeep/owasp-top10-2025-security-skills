
name: cwe-756-missing-custom-error-page
description: Use when testing cwe-756 exceptional conditions on target.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-756, exceptions, a10, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a10-exceptional-conditions
---

# CWE-756 - Missing Custom Error Page

CWE-756: the application does not provide a custom error page, so the framework or server default error page is shown, leaking internals.

## Parent Skill

This is a sub-skill of `owasp-a10-exceptional-conditions` (OWASP A10 Mishandling of Exceptional Conditions, Top 10 2025).
Load the parent for overall A10 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-756 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When the application does not provide a custom error page, so the framework default (Apache, Tomcat, Express) is shown.

## Detection & Test

1. **Trigger the error.** Send a request that causes a 404, 500, or 403.
2. **Observe the error page.** Note whether the framework default (Apache, Tomcat, Express) is served.
3. **Check for internals.** Look for paths, versions, or stack traces on the default page.
4. **Confirm the disclosure.** Verify the internals are present.
5. **Document the status, the default page, and the internal data.

## Example Findings

- A 404 that serves the Apache default page with the server version.
- A 500 that serves the Tomcat default page with the Tomcat version and the request path.

## Impact

- Information disclosure of internals (paths, versions, stack traces) that attackers target (CWE-209/215/550).
- Bypass of a security control via missing or extra parameters, or via fall-through (CWE-234/235/478/484).
- Crash or state change from an unhandled condition (CWE-248/369/476/460).
- Failing open (CWE-636) when a control errors, so the security decision is bypassed.

## See Also

- `owasp-a10-exceptional-conditions` - parent skill (A10 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).
- `dogfood` - owning skills (when loaded).