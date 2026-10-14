# NAFATH Brief

Version: NAFATH-V4
Track: cybersecurity

## Summary

NAFATH is Saudi Arabia's national digital-identity verification platform. Protecting it
requires coordinated controls across six technical domains: secure software delivery and
secret management; robustness of AI fraud and biometric models; hardened mobile clients;
resilient Internet routing; incident-aware cybersecurity practices; and provable software
supply chains via SBOMs. Together these address supply-chain risk: compromised code,
models, devices, or transit can all silently undermine identity verification unless the
entire stack is governed, audited, and monitored.

## Software

Store configuration and secrets (database URLs, API keys, feature flags) outside the
source tree — in environment variables or a dedicated secret manager — so the same build
artifact can be promoted across environments without code changes. Keeping secrets out of
VCS prevents accidental leakage via published builds or Git history and allows operators
to rotate credentials without rebuilding.

Resource: The Twelve-Factor App - Config - https://12factor.net/config

## AI

Adversarial-machine-learning attacks fall into distinct classes: evasion (crafting inputs
at inference to cause misclassification), poisoning (injecting poisoned samples during
training to insert backdoors), model extraction (reconstructing a model via queries), and
membership inference (determining if a record was in the training data). Defenses must be
matched to each threat model — robust training for evasion, data vetting for poisoning, rate
limits and authentication for extraction, and differential privacy for membership risks.

Resource: NIST AI 100-2 E2023 - Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations - https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-2e2023.pdf

## Mobile

The OWASP Mobile Application Security Verification Standard (MASVS) defines security
requirements across storage, crypto, authentication, networking, platform interaction,
code quality, resilience, and privacy. MASVS provides two levels (L1 standard, L2
defense-in-depth) plus a resilience profile (R) for apps facing reverse engineering. Mobile
clients are verified against MASVS with the companion MASTG test-cases to produce repeatable
assessment evidence.

Resource: OWASP Mobile Application Security Verification Standard (MASVS) - https://mas.owasp.org/MASVS/

## Networking


## Cybersecurity


## Data


## Misconception in my track


## Open questions

