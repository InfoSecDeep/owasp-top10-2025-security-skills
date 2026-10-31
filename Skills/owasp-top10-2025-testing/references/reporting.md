# Finding Report Template

One block per confirmed finding. Copy the template per finding; keep evidence exact (verbatim request/response, unedited HAR or screenshot paths).

```
ID:          <TARGET>-A##-NNN   (category letter + short code + sequence, e.g. WIN-A01-004)
Title:       <short noun phrase: what + where>
Severity:    Critical | High | Medium | Low | Informational
CVSSv3.1:    <score> (vector)
OWASP 2025:  A01-A10 category name
CWE:         CWE-NNN (primary) [+ CWE-NNN secondary if genuinely multi]
Endpoint:    <full URL>

Summary
  <2-4 sentences: what is broken, why it matters, what the attacker gets.>

Evidence
  Request:  <verbatim request line + key headers>
  Response: <status + body excerpt; full capture at <path>>
  Media:    <screenshot/HAR paths from capture-vulnerability-evidence>

Reproduction
  1. <numbered step>
  2. <step - copy-pasteable curl or browser action>
  3. <expected attacker-side result>

Demonstrated Impact
  <concrete: data read/written/executed. Name the data or action shown, not a hypothetical.>

Remediation
  <specific fix: code-level where possible, reference OWASP ASVS 5.0 control if relevant>

Verification
  <negative control or re-test after fix: what was checked, what was observed>
```

## Severity Rubric
- Critical: RCE; full-breach data compromise; auth bypass to admin; deserialization RCE; SSRF to cloud metadata/credentials.
- High: stored XSS in privileged context; SQLi with data access; IDOR to PII; mass-assignment to privilege; session fixation with live sessions; credential theft via exposed logs.
- Medium: reflected XSS; CSRF on sensitive action; SSRF to non-sensitive internal; open redirect chained to phishing; weak TLS carrying sensitive data; real data in error messages.
- Low: missing hardening header; verbose error without real data; default error page; redundant weak control.
- Informational: ViewState MAC validation failure on probe; unconfirmed XSS/SQLi probe (no exploit evidence); best-practice gaps with no demonstrated impact.

## Rules
- One finding = one CWE = one 2025 category. Multi-issue flows get multiple blocks.
- SSRF is filed under A01 in the 2025 edition (absorbed from 2021 A10).
- Severity follows demonstrated impact - not the scanner label, not the CWE's typical rating.
- Every Critical/High must have a reproduction that another tester can replay without guessing.
