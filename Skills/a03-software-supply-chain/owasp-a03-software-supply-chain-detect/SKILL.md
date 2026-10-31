
name: owasp-a03-software-supply-chain-detect
description: Use when testing A03 Supply Chain Failures on web.
version: 1.0.0
license: MIT
platforms: [linux, windows]
tags: [owasp, top10-2025, a03, supply-chain, cwe, pentest]
category: pentesting-skills
related_skills:
  - owasp-top10-2025-testing
---

# A03 - Software Supply Chain Failures

OWASP Top 10 2025 category A03 (new, expands 2021's A06 Vulnerable and Outdated Components). Covers untracked or outdated dependencies, untrusted components, and distribution infrastructure compromise. The parent skill `owasp-top10-2025-testing` holds scope, reporting, and the full CWE reference.

## When to Use
- Fingerprinting stack/library versions, hunting out-of-date or unmaintained components, or auditing third-party supply chain exposure.

## Mapped CWEs (6)

- CWE-447: Use of obsolete function
- CWE-1035: Using components with known vulnerabilities (2017 A9)
- CWE-1104: Use of unmaintained third-party components
- CWE-1329: Reliance on component that is not updateable
- CWE-1357: Reliance on insufficiently trustworthy component
- CWE-1395: Dependency on vulnerable third-party component

## Test Procedure

1. **Fingerprint with at least 2 signals.** Response headers, JS bundle names/versions, asset paths, and favicon hash. Do not rely on a single banner.
2. **WordPress.** For WordPress sites, enumerate plugins and themes with their versions. For each plugin CVE, confirm the exact version and configuration.
3. **Version-to-CVE check.** Cross-check observed version against NVD or GitHub Advisory DB. Confirm the CVE's prerequisites (version range + configuration + feature in use) before filing a finding.
4. **Exposed manifests.** Check /package.json, /package-lock.json, /composer.json, /pom.xml, /requirements.txt, /go.mod, /vendor/, and /sbom for version pinning and unmaintained deps.
5. **Third-party widgets.** Identify chat, analytics, payment, and ad scripts. Check their origin domains. Confirm SRI integrity attributes are present on external scripts; absence is a supply-chain risk.
6. **Stale CDN assets.** Compare asset hashes across cache layers; if an out-of-date library with a known CVE is still being served, flag it.
7. **Unmaintained components.** Note any component with no active maintainers or an abandoned upstream (CWE-1104).

## Validation / Negative Control

- Version confirmed by at least two independent signals (header + JS + asset path).
- CVE prerequisites independently verified - the exact version is present and the vulnerable feature is used.
- Do not file a finding for a component that is present but not loaded/executed in the flow.

## See Also

- `owasp-top10-2025-testing` - parent skill (scope, reporting, full CWE reference).

## CWE Sub-Skills

Each mapped CWE above has a dedicated sub-skill with focused detection steps, example payloads, bypass tricks, and expected impact. Load the relevant sub-skill via `skill_view(name)` when a finding or test case matches one of these.

| CWE | Sub-skill |
|---|---|
| CWE-447 | `cwe-447-use-of-obsolete-function` |
| CWE-1035 | `cwe-1035-component-with-known-vulnerability` |
| CWE-1104 | `cwe-1104-unmaintained-third-party-component` |
| CWE-1329 | `cwe-1329-reliance-on-component-not-updatable` |
| CWE-1357 | `cwe-1357-reliance-on-insufficiently-trustworthy-component` |
| CWE-1395 | `cwe-1395-dependency-on-vulnerable-third-party-component` |