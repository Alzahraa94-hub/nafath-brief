# nafath-brief
NAFATH brief: cybersecurity-focused overview
git clone https://github.com/Alzahraa94-hub/nafath-brief.git
cd nafath-brief
git config user.name "Alzahraa"
git config user.email "your-github-email@example.com"

# Step 1 — Commit 1: skeleton: NAFATH-V4
cat > brief.md <<'EOF'
# NAFATH Brief

Version: NAFATH-V4
Track: cybersecurity

## Summary

## Software

## AI

## Mobile

## Networking

## Cybersecurity

## Data

## Misconception in my track

## Open questions
EOF

git add brief.md
git commit -m "skeleton: NAFATH-V4"

# Step 2 — Commit 2: overview: connect the six subtopics
cat > brief.md <<'EOF'
# NAFATH Brief

Version: NAFATH-V4
Track: cybersecurity

## Summary

NAFATH is Saudi Arabia's national digital-identity verification platform. Protecting it
touches six technical fields at once. On the Software side, configuration and secrets must
sit outside the codebase so credentials never leak through a published build. On AI,
fraud-scoring and face-match models face adversarial evasion and poisoning. On Mobile, the
citizen-facing app must resist tampering and insecure local storage. On Networking, BGP
route hijacks can silently redirect authentication traffic, so RPKI origin validation is
essential. On Data, a Software Bill of Materials makes every third-party component
auditable. The thread tying these together is supply-chain risk, which is a theme I will
return to across the sections below.

## Software

## AI

## Mobile

## Networking

## Cybersecurity

## Data

## Misconception in my track

## Open questions
EOF

git add brief.md
git commit -m "overview: connect the six subtopics"

# Step 3 — Commit 3: research: software, ai, mobile
cat > brief.md <<'EOF'
# NAFATH Brief

Version: NAFATH-V4
Track: cybersecurity

## Summary

NAFATH is Saudi Arabia's national digital-identity verification platform. Protecting it
touches six technical fields at once. On the Software side, configuration and secrets must
sit outside the codebase so credentials never leak through a published build. On AI,
fraud-scoring and face-match models face adversarial evasion and poisoning. On Mobile, the
citizen-facing app must resist tampering and insecure local storage. On Networking, BGP
route hijacks can silently redirect authentication traffic, so RPKI origin validation is
essential. On Data, a Software Bill of Materials makes every third-party component
auditable. The thread tying these together is supply-chain risk, which is a theme I will
return to across the sections below.

## Software

Store configuration — database URLs, API keys, feature flags — in environment variables or
a secret manager, never in the source tree. The Twelve-Factor App principle III ("Config")
separates config from code so the same build can ship to dev, staging, and production
without edits. For NAFATH, this prevents credentials from leaking through Git history and
lets operators rotate secrets without redeploying.

Resource: The Twelve-Factor App - Config - https://12factor.net/config

## AI

NIST AI 100-2 groups adversarial-ML threats by attacker stage and goal. Evasion attacks
craft inputs at inference time to force misclassification — directly relevant to a
face-match model. Poisoning attacks corrupt the training set to insert a backdoor. Model
extraction steals the trained model through repeated queries, and membership inference
leaks whether a specific record was in the training data. NAFATH's fraud-scoring and
biometric models need defenses tuned to each class.

Resource: NIST AI 100-2 E2023 - Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations - https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-2e2023.pdf

## Mobile

The OWASP Mobile Application Security Verification Standard (MASVS) defines mobile-app
security controls across eight domains — storage, crypto, authentication, network,
platform interaction, code quality, resilience, and privacy. It offers two verification
levels (MASVS-L1 standard, MASVS-L2 defense-in-depth) plus a resilience profile (MASVS-R)
for apps facing reverse engineering. For a national-ID client like NAFATH, MASVS-L2 plus
MASVS-R is the right bar, verified using the companion MASTG test cases.

Resource: OWASP Mobile Application Security Verification Standard (MASVS) - https://mas.owasp.org/MASVS/

## Networking

## Cybersecurity

## Data

## Misconception in my track

## Open questions
EOF

git add brief.md
git commit -m "research: software, ai, mobile"

# Step 4 — Commit 4: research: networking, cybersecurity, data
cat > brief.md <<'EOF'
# NAFATH Brief

Version: NAFATH-V4
Track: cybersecurity

## Summary

NAFATH is Saudi Arabia's national digital-identity verification platform. Protecting it
touches six technical fields at once. On the Software side, configuration and secrets must
sit outside the codebase so credentials never leak through a published build. On AI,
fraud-scoring and face-match models face adversarial evasion and poisoning. On Mobile, the
citizen-facing app must resist tampering and insecure local storage. On Networking, BGP
route hijacks can silently redirect authentication traffic, so RPKI origin validation is
essential. On Data, a Software Bill of Materials makes every third-party component
auditable. The thread tying these together is supply-chain risk, which is a theme I will
return to across the sections below.

## Software

Store configuration — database URLs, API keys, feature flags — in environment variables or
a secret manager, never in the source tree. The Twelve-Factor App principle III ("Config")
separates config from code so the same build can ship to dev, staging, and production
without edits. For NAFATH, this prevents credentials from leaking through Git history and
lets operators rotate secrets without redeploying.

Resource: The Twelve-Factor App - Config - https://12factor.net/config

## AI

NIST AI 100-2 groups adversarial-ML threats by attacker stage and goal. Evasion attacks
craft inputs at inference time to force misclassification — directly relevant to a
face-match model. Poisoning attacks corrupt the training set to insert a backdoor. Model
extraction steals the trained model through repeated queries, and membership inference
leaks whether a specific record was in the training data. NAFATH's fraud-scoring and
biometric models need defenses tuned to each class.

Resource: NIST AI 100-2 E2023 - Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations - https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-2e2023.pdf

## Mobile

The OWASP Mobile Application Security Verification Standard (MASVS) defines mobile-app
security controls across eight domains — storage, crypto, authentication, network,
platform interaction, code quality, resilience, and privacy. It offers two verification
levels (MASVS-L1 standard, MASVS-L2 defense-in-depth) plus a resilience profile (MASVS-R)
for apps facing reverse engineering. For a national-ID client like NAFATH, MASVS-L2 plus
MASVS-R is the right bar, verified using the companion MASTG test cases.

Resource: OWASP Mobile Application Security Verification Standard (MASVS) - https://mas.owasp.org/MASVS/

## Networking

BGP has no built-in origin check, so any ISP can announce someone else's prefix and
redirect traffic. RFC 6480 defines the Resource Public Key Infrastructure (RPKI), where
address holders sign Route Origin Authorizations (ROAs) binding a prefix to an AS number.
Routers running Route Origin Validation drop or deprioritize unsigned or mismatched
announcements. RPKI stops origin hijacks but not path manipulation or route leaks; ASPA
and BGPsec cover the remaining gap.

Resource: RFC 6480 - An Infrastructure to Support Secure Internet Routing - https://www.rfc-editor.org/rfc/rfc6480

## Cybersecurity

CVE-2021-44228 ("Log4Shell") is an unauthenticated remote code execution in Apache Log4j
2.0-beta9 through 2.14.1. If an attacker-controlled string reaches a log statement,
Log4j's JNDI lookup fetches a remote class from an LDAP or RMI endpoint and executes it in
the server JVM. CVSS is 10.0. Mitigation is upgrading to 2.17.1 or later, which disables
JNDI by default and removes the JndiLookup class, or physically deleting that class from
older JARs.

Resource: NVD - CVE-2021-44228 - https://nvd.nist.gov/vuln/detail/CVE-2021-44228

## Data

The NTIA minimum SBOM elements require every software bill of materials to list, for each
component: Supplier Name, Component Name, Version, Unique Identifiers (e.g., CPE, PURL),
Dependency Relationship, Author of the SBOM data, and Timestamp. These seven fields let a
defender answer "do I ship this vulnerable library?" in minutes instead of days — a direct
lesson from Log4Shell triage, and a prerequisite for NAFATH's vendor-risk program.

Resource: NTIA - The Minimum Elements For a Software Bill of Materials (SBOM) - https://www.ntia.gov/sites/default/files/publications/sbom_minimum_elements_report_0.pdf

## Misconception in my track

## Open questions
EOF

git add brief.md
git commit -m "research: networking, cybersecurity, data"

# Step 5 — Commit 5: analysis: misconception and open question
cat > brief.md <<'EOF'
# NAFATH Brief

Version: NAFATH-V4
Track: cybersecurity

## Summary

NAFATH is Saudi Arabia's national digital-identity verification platform. Protecting it
touches six technical fields at once. On the Software side, configuration and secrets must
sit outside the codebase so credentials never leak through a published build. On AI,
fraud-scoring and face-match models face adversarial evasion and poisoning. On Mobile, the
citizen-facing app must resist tampering and insecure local storage. On Networking, BGP
route hijacks can silently redirect authentication traffic, so RPKI origin validation is
essential. On Data, a Software Bill of Materials makes every third-party component
auditable. The thread tying these together is supply-chain risk, which is a theme I will
return to across the sections below.

## Software

Store configuration — database URLs, API keys, feature flags — in environment variables or
a secret manager, never in the source tree. The Twelve-Factor App principle III ("Config")
separates config from code so the same build can ship to dev, staging, and production
without edits. For NAFATH, this prevents credentials from leaking through Git history and
lets operators rotate secrets without redeploying.

Resource: The Twelve-Factor App - Config - https://12factor.net/config

## AI

NIST AI 100-2 groups adversarial-ML threats by attacker stage and goal. Evasion attacks
craft inputs at inference time to force misclassification — directly relevant to a
face-match model. Poisoning attacks corrupt the training set to insert a backdoor. Model
extraction steals the trained model through repeated queries, and membership inference
leaks whether a specific record was in the training data. NAFATH's fraud-scoring and
biometric models need defenses tuned to each class.

Resource: NIST AI 100-2 E2023 - Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations - https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-2e2023.pdf

## Mobile

The OWASP Mobile Application Security Verification Standard (MASVS) defines mobile-app
security controls across eight domains — storage, crypto, authentication, network,
platform interaction, code quality, resilience, and privacy. It offers two verification
levels (MASVS-L1 standard, MASVS-L2 defense-in-depth) plus a resilience profile (MASVS-R)
for apps facing reverse engineering. For a national-ID client like NAFATH, MASVS-L2 plus
MASVS-R is the right bar, verified using the companion MASTG test cases.

Resource: OWASP Mobile Application Security Verification Standard (MASVS) - https://mas.owasp.org/MASVS/

## Networking

BGP has no built-in origin check, so any ISP can announce someone else's prefix and
redirect traffic. RFC 6480 defines the Resource Public Key Infrastructure (RPKI), where
address holders sign Route Origin Authorizations (ROAs) binding a prefix to an AS number.
Routers running Route Origin Validation drop or deprioritize unsigned or mismatched
announcements. RPKI stops origin hijacks but not path manipulation or route leaks; ASPA
and BGPsec cover the remaining gap.

Resource: RFC 6480 - An Infrastructure to Support Secure Internet Routing - https://www.rfc-editor.org/rfc/rfc6480

## Cybersecurity

CVE-2021-44228 ("Log4Shell") is an unauthenticated remote code execution in Apache Log4j
2.0-beta9 through 2.14.1. If an attacker-controlled string reaches a log statement,
Log4j's JNDI lookup fetches a remote class from an LDAP or RMI endpoint and executes it in
the server JVM. CVSS is 10.0. Mitigation is upgrading to 2.17.1 or later, which disables
JNDI by default and removes the JndiLookup class, or physically deleting that class from
older JARs.

Resource: NVD - CVE-2021-44228 - https://nvd.nist.gov/vuln/detail/CVE-2021-44228

## Data

The NTIA minimum SBOM elements require every software bill of materials to list, for each
component: Supplier Name, Component Name, Version, Unique Identifiers (e.g., CPE, PURL),
Dependency Relationship, Author of the SBOM data, and Timestamp. These seven fields let a
defender answer "do I ship this vulnerable library?" in minutes instead of days — a direct
lesson from Log4Shell triage, and a prerequisite for NAFATH's vendor-risk program.

Resource: NTIA - The Minimum Elements For a Software Bill of Materials (SBOM) - https://www.ntia.gov/sites/default/files/publications/sbom_minimum_elements_report_0.pdf

## Misconception in my track

A common belief is that upgrading Log4j to 2.15.0 fully patches Log4Shell
(CVE-2021-44228). It does not. Shortly after 2.15.0 shipped, CVE-2021-45046 was published,
and the Apache Log4j Security Vulnerabilities page states, under the CVE-2021-45046 entry:
"It was found that the fix to address CVE-2021-44228 in Log4j 2.15.0 was incomplete in
certain non-default configurations." A denial-of-service bug (CVE-2021-45105) and a
JDBC-appender RCE (CVE-2021-44832) followed. The real end-state is 2.17.1 or later for
Java 8+, which disables JNDI lookups by default and removes the JndiLookup class entirely.

Source: Apache Log4j Security Vulnerabilities - https://logging.apache.org/log4j/2.x/security.html (section: CVE-2021-45046)

## Open questions

Is Route Origin Validation actually enforced in the ISP path serving NAFATH, or only
published? I want to confirm whether the upstream transit providers drop RPKI-invalid
announcements, because an unenforced ROA still leaves origin hijacks possible even when
the authorization record exists.
EOF

git add brief.md
git commit -m "analysis: misconception and open question"

# Step 6 — Commit 6: revise: overview
python - <<'PY'
from pathlib import Path
p = Path("brief.md")
text = p.read_text()
old = """The thread tying these together is supply-chain risk, which is a theme I will
return to across the sections below."""
new = """The thread tying these together is supply-chain risk, and the clearest worked example is
Log4Shell, which is the question I dig into on the cybersecurity side."""
if old not in text:
    raise SystemExit("old sentence not found")
p.write_text(text.replace(old, new))
PY

git add brief.md
git commit -m "revise: overview"

# Step 7 — Commit 7: changelog: record history
git log --oneline
# output example:
# abcdef1 changelog: record history
# 1234567 revise: overview
# ...
# Copy the first 7 chars from each commit line and create CHANGELOG.md in oldest-to-newest order.

cat > CHANGELOG.md <<'EOF'
# Changelog

- xxxxxxx skeleton: NAFATH-V4
- xxxxxxx overview: connect the six subtopics
- xxxxxxx research: software, ai, mobile
- xxxxxxx research: networking, cybersecurity, data
- xxxxxxx analysis: misconception and open question
- xxxxxxx revise: overview
EOF

# Replace xxxxxxx with the real 7-char commit ids from git log, in oldest-to-newest order.
# Example:
# - 1234567 skeleton: NAFATH-V4
# - 89abcde overview: connect the six subtopics
# ...

git add CHANGELOG.md
git commit -m "changelog: record history"
git push origin main
# Output final info
last_commit_short="$(git log --oneline -n1 | cut -d' ' -f1)"
echo
echo "Done. Repo: $REPO_URL"
echo "Last commit (7-char): ${last_commit_short}"
echo
echo "Literal sentence from cybersecurity source (as included in brief.md):"
echo 'It was found that the fix to address CVE-2021-44228 in Log4j 2.15.0 was incomplete in certain non-default configurations.'
echo
echo "Please verify the CVE-2021-45046 page at:"
echo "https://logging.apache.org/log4j/2.x/security.html"
