
name: cwe-11-aspnet-debug-binary
description: Use when an ASP.NET app has Debug=true and a debug endpoint.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-11, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-11 - ASP.NET Misconfiguration - Creating Debug Binary

CWE-11: ASP.NET Misconfiguration - Creating Debug Binary - the app ships with a debug assembly enabled, exposing stack traces and sometimes remote debug endpoints.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-11 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an ASP.NET app is built with `Debug=true` and exposes a debug endpoint.

## Detection & Test

1. Check `X-AspNet-Version` and `Server` headers for debug hints.
2. Request a path that returns a verbose .NET stack trace.
3. Look for a `/_dev` or `/aspnet_client` debug handler.
4. Confirm `Debug=true` in `web.config`.

## Example Requests

```http
GET /error-page (500 with .NET stack trace)
```
```http
GET /aspnet_client/facts/
```

## Bypass Tricks

- Trigger a 500 to leak the stack trace.
- Use a `.aspx` handler that exposes the debug view.
- Request `/_DevTools` on newer .NET Framework.
- Exploit `X-Powered-By: ASP.NET` to fingerprint the exact version.

## Impact

- Information disclosure via verbose stack traces and debug handlers.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).