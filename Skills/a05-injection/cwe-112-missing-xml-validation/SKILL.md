
name: cwe-112-missing-xml-validation
description: Use when a web injection sink accepts CWE input.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [cwe, cwe-112, injection, a05, pentest, owasp]
category: pentesting-skills
related_skills:
  - owasp-a05-injection
---

# CWE-112 - Missing XML Validation

CWE-112: an XML document is parsed without proper validation, allowing the attacker to inject unexpected elements, attributes, or DTDs that change the parser's behavior.

## Parent Skill

This is a sub-skill of `owasp-a05-injection` (OWASP A05 Injection, Top 10 2025).
Load the parent for overall A05 scope, the test procedure, and validation criteria
(negative control). This skill covers the CWE-112 detail: what to look for,
how to trigger it, and what a confirmed finding looks like.

## When to Use

- When an XML input (SOAP body, XML config, uploaded XML) is parsed without a schema or validation step.

## Detection & Test

1. **Find the XML sink.** Identify which endpoint parses XML (SOAP, REST with XML body, uploaded XML file).
2. **Inject unexpected elements.** Add an element or attribute that the schema doesn't define.
3. **Confirm the parser accepts it.** Verify the parser processes the unexpected element (different response, error, or data change).
4. **Test DTD injection.** If the parser supports DTDs, test for XXE via `<!DOCTYPE` and entity definitions.
5. **Document the sink, payload, and proof.

## Example Findings

- A SOAP body with an extra `<admin>true</admin>` element that the parser processes.
- An uploaded XML file with a DOCTYPE that defines an external entity.

## Impact

- Data disclosure, logic manipulation, or code execution through the injection point.
- Privilege escalation or session hijack if the injection reaches auth/session logic.
- Persistence until the sink is parameterized or the input is validated.
- Lateral movement when the same unsanitized sink repeats across endpoints.

## See Also

- `owasp-a05-injection` - parent skill (A05 scope, Test Procedure, Validation, reporting).
- `owasp-top10-2025-testing` - top-level OWASP Top 10 2025 reference (full 249-CWE table, priority order).