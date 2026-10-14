# NAFATH Brief

Version: NAFATH-V4
Track: cybersecurity

## Summary

NAFATH is Saudi Arabia's national digital-identity verification platform. Protecting it requires coordinated work across six technical areas: secure software delivery and secret management; hardening AI fraud and face‑match models; building tamper‑resistant mobile clients; ensuring resilient Internet routing; applying strong cybersecurity practices; and tracking third‑party components with SBOMs. A weakness in any layer — code, models, devices, transit, or data — can quietly break identity checks. The shared theme is supply‑chain risk: defenders must audit, monitor, and patch every component and its configuration so that an attacker cannot exploit a small flaw to gain large access.

## Software

Store configuration and secrets (database URLs, API keys, feature flags) outside the source tree — in environment variables or a dedicated secret manager. This follows the Twelve‑Factor App principle III (“Config”). Keeping secrets out of VCS prevents accidental leakage through published builds or Git history and lets operators rotate credentials without rebuilding artifacts.

Resource: The Twelve-Factor App - Config - https://12factor.net/config

## AI

Adversarial machine‑learning attacks include evasion (crafting inputs at inference to fool models), poisoning (adding malicious examples to training data), model extraction (reconstructing a model via queries), and membership inference (learning whether a record was in training). Defenses differ by class: robust training and input checks for evasion, data validation and provenance for poisoning, rate limits and access controls for extraction, and privacy measures for membership risks.

Resource: NIST AI 100-2 E2023 - Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations - https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-2e2023.pdf

## Mobile

The OWASP Mobile Application Security Verification Standard (MASVS) catalogs security requirements for mobile apps across storage, crypto, auth, networking, platform interaction, code quality, resilience, and privacy. MASVS offers levels L1 (standard) and L2 (defense‑in‑depth) plus a resilience profile (R). Assessments use the MASTG test cases to produce repeatable evidence that a client resists tampering and insecure local storage.

Resource: OWASP Mobile Application Security Verification Standard (MASVS) - https://mas.owasp.org/MASVS/

## Networking

BGP has no built‑in origin authentication, so a misbehaving or malicious ISP can announce another party's IP prefix and divert traffic (prefix hijack). RPKI lets address holders publish cryptographic Route Origin Authorizations (ROAs) that bind prefixes to origin ASNs; routers that do Route Origin Validation can drop or deprioritize invalid announcements. RPKI stops origin hijacks but does not protect against path manipulation or route leaks.

Resource: RFC 6480 - An Infrastructure to Support Secure Internet Routing - https://www.rfc-editor.org/rfc/rfc6480

## Cybersecurity

Log4Shell (CVE-2021-44228) is a critical remote code execution in Apache Log4j where attacker input could trigger JNDI lookups that load and run remote code on servers. It scored 10.0 because it allowed easy, unauthenticated exploitation across many Java applications. The practical fix was upgrading to patched releases (final baseline: 2.17.1+ for Java 8+) and removing or disabling the JndiLookup component where needed.

Resource: NVD - CVE-2021-44228 - https://nvd.nist.gov/vuln/detail/CVE-2021-44228

## Data

A Software Bill of Materials (SBOM) is a machine‑readable list of components and their relationships used to triage vulnerabilities quickly. The NTIA minimum SBOM elements require, for each component: Supplier Name, Component Name, Version, Unique Identifiers (e.g., CPE, PURL), Dependency Relationship, Author of the SBOM entry, and Timestamp. These fields let teams answer "do we ship this vulnerable library?" fast.

Resource: NTIA - The Minimum Elements For a Software Bill Of Materials (SBOM) - https://www.ntia.gov/sites/default/files/publications/sbom_minimum_elements_report_0.pdf

## Misconception in my track

A common misconception is that upgrading Log4j to 2.15.0 fully fixed Log4Shell. In reality, the 2.15.0 fix was incomplete for some non‑default configurations and additional CVEs followed. The correct safe state for most Java 8+ deployments is Log4j 2.17.1 or later, which disables JNDI lookups by default and removes the vulnerable JndiLookup class. The Apache Log4j security page documents this: "It was found that the fix to address CVE-2021-44228 in Log4j 2.15.0 was incomplete in certain non-default configurations."

Source: Apache Log4j Security Vulnerabilities - https://logging.apache.org/log4j/2.x/security.html (section: CVE-2021-45046)

## Open questions

Is Route Origin Validation actually enforced on the ISP path that serves NAFATH (not merely published ROAs)? I will verify whether upstream transit providers drop RPKI-invalid announcements or only publish ROAs without enforcement.
