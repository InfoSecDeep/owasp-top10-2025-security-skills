
name: cwe-776-billion-laughs
description: Use when an XML endpoint expands recursive entities (DoS).
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-776, misconfiguration, pentest, owasp, a02]
category: pentesting-skills
related_skills:
  - owasp-a02-security-misconfiguration
---

# CWE-776 - XML Entity Expansion (Billion Laughs)

CWE-776: XML Entity Expansion - the application parses XML and allows a recursive entity definition to be expanded, consuming resources (Billion Laughs).

## Parent Skill

This is a sub-skill of `owasp-a02-security-misconfiguration` (OWASP A02 Security Misconfiguration, Top 10 2025).
Load the parent for overall A02 scope, validation criteria (negative control), and
the reporting template. This skill covers the CWE-776 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- Use when an XML endpoint can be made to expand a recursive entity definition, causing a DoS.

## Detection & Test

1. Send an XML with a recursive entity definition (`<entity x1 "%1"/>`, etc.).
2. Confirm the server's memory/CPU usage spikes.
3. Check for a 500 or a timeout (the server is expanding the entity).
4. Compare a normal request vs. the entity-expansion request.

## Example Requests

```http
<?xml version="1.0"?><!DOCTYPE root [<!ENTITY x1 "xx"/><!ENTITY x2 "%x1%x1"/><!ENTITY x3 "%x2%x2"/>]><root>&x3;</root>
```

## Bypass Tricks

- Use a recursive entity definition to consume memory.
- Exploit a parser that doesn't limit entity expansion depth.
- Combine with an OOB entity to exfiltrate data.
- Use a `SYSTEM` entity to read a file and expand it.

## Impact

- DoS via uncontrolled XML entity expansion.

## See Also

- `owasp-a02-security-misconfiguration` - parent skill (A02 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).