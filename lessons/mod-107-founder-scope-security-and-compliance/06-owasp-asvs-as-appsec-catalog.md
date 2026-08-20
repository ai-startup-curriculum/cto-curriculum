# OWASP ASVS — The AppSec Scope Catalog at Founder Scale

> "Do not invent your application-security programme.
> ASVS L1 has already invented it for you; your job is to
> mark every requirement Pass / Fail / N/A with evidence,
> and to close the Fails on a defensible schedule." — the
> discipline this chapter is written around.

## Motivation

Application security is the security discipline most
often approached by founder-scope teams as *"we should
probably do more of that"* — with no scope catalog to
work against and no way to know when *"more"* is
enough. Every enterprise security questionnaire asks
some version of *"describe your application-security
programme"*, and the founder-scope answer without a
catalog is a paragraph of hand-waving that lands as a
procurement red flag.

OWASP publishes the exact catalog you need. The
Application Security Verification Standard (ASVS) is a
free, versioned, community-maintained catalog of
application-security requirements grouped into three
levels — Level 1 (opportunistic), Level 2 (standard,
appropriate for regulated / enterprise SaaS), Level 3
(advanced, appropriate for critical infrastructure and
sensitive-data applications). The founder-scope
posture is to adopt L1 as the baseline and to run a
gap-register discipline against L2 as the enterprise-
ready target.

This chapter walks the ASVS structure, the level
selection, the founder-scope gap-register format, and
the boundary to the deep AppSec depth that belongs to
a security engineer.

## What ASVS actually is

The OWASP Application Security Verification Standard
is a free, open, versioned catalog of application-
security verification requirements — see the project
page at
[owasp.org — Application Security Verification Standard](https://owasp.org/www-project-application-security-verification-standard/)
and the current release repository at
[github.com/OWASP/ASVS](https://github.com/OWASP/ASVS).
Key properties for founder scope:

- **It is a scope catalog, not a methodology.** ASVS
  tells you *what* to verify. How you verify each item
  (SAST, DAST, manual review, penetration test) is a
  separate decision.
- **It is versioned.** The current stable release is
  the v4.x line; a v5.0 revision has been under
  active development and may be the current stable
  release depending on when you read this — verify at
  [github.com/OWASP/ASVS/releases](https://github.com/OWASP/ASVS/releases).
- **It is levelled.** L1 / L2 / L3 correspond to
  progressively more rigorous requirements. Every L1
  requirement is also an L2 and L3 requirement.
- **It is grouped into chapters** (v4.0.3 uses 14
  chapters: Architecture, Authentication, Session
  Management, Access Control, Validation Sanitisation
  Encoding, Stored Cryptography, Error Handling and
  Logging, Data Protection, Communications, Malicious
  Code, Business Logic, Files and Resources, API and
  Web Service, Configuration; v5 restructures and
  renames — verify against the release notes).
- **Each requirement has a unique ID** (`V2.1.1` for
  example) suitable for direct citation in a gap
  register.

<!-- needs-research: confirm the current ASVS release version (v4.0.3 stable vs. v5.x release status) as of the reader's date; the chapter references v4.x, which is the stable line at the time of writing but is being superseded. -->

## The three levels

### Level 1 — Opportunistic

Requirements that can be verified by an outside
observer without access to source code or design
documentation. Intended as a *minimum defence against
opportunistic attackers*. Roughly 130 requirements in
v4.0.3.

Founder-scope target: **every applicable L1
requirement is Pass at time of first customer
deployment**. Any Fail at L1 is a blocker; any N/A
requires an explicit *"why it does not apply to this
product"* line.

### Level 2 — Standard

The Level 1 requirements plus additional design-
verification and code-verification requirements
suitable for applications that handle **sensitive
data** or operate in **regulated industries**.
Roughly 270 requirements total in v4.0.3.

Founder-scope target: **L2 as the enterprise-ready
posture**. The gap register between L1-Pass and
L2-Pass is the AppSec-hardening roadmap the first
security hire will drive to closure. Some L2
requirements are legitimately Not Applicable for a
given product (SAML if you do not offer SAML; secure
file upload if you do not accept uploads); each N/A
gets a one-line justification.

### Level 3 — Advanced

The L1 + L2 requirements plus additional
requirements suitable for **critical applications** —
applications that perform high-value transactions,
contain sensitive medical data, or operate in
national-security contexts. Roughly 290 requirements
total in v4.0.3.

Founder-scope target: **out of scope**. L3 is a
security-team programme. If a specific customer
demands L3 posture, the demand is a hiring signal
for a dedicated AppSec engineer, not a founder-scope
work item.

## The founder-scope gap-register format

The load-bearing artifact this chapter produces is a
**gap register**: a spreadsheet (or a table in
`docs/security/asvs-gap-register.md`) with one row per
ASVS requirement in scope. Columns:

- **ID** — the ASVS requirement identifier (e.g.,
  `V2.1.1`).
- **Level** — 1 or 2 (or 3 if in scope).
- **Requirement** — the requirement text (verbatim
  from ASVS).
- **Chapter** — the ASVS chapter name.
- **Status** — Pass / Fail / N/A / In Progress.
- **Evidence or justification** — for Pass, a
  citation (log query, code file / line, control
  reference). For Fail, a description of the gap.
  For N/A, the one-line justification. For In
  Progress, the current state and the plan.
- **Owner** — the engineer (or the CTO) accountable
  for closing the gap.
- **Target close date** — for Fail / In Progress.
- **Verification method** — how the Pass was
  determined (self-attestation, code review, SAST,
  DAST, unit test, integration test, penetration
  test, manual walkthrough).

A founder-scope gap register at L1 typically starts
with 60–80% Pass, 10–20% Fail, 10–20% N/A. The
Fails become sprint work; the register is re-
reviewed monthly.

## L1 requirement categories — the founder-scope walkthrough

A brief tour of the chapters that most often produce
Fails at founder scope:

- **V1 Architecture / V14 Configuration.**
  Architecture-level requirements — high-level
  design, security roles, secure-configuration
  defaults. Frequent Fails: no documented threat
  model (L2), no documented trust boundaries, no
  documented security-relevant configuration
  defaults.
- **V2 Authentication.** Password policy, MFA,
  credential recovery, brute-force protection, secret
  storage. Frequent Fails: password policy without
  breach-list check, no rate limit on login,
  credentials logged in application logs.
- **V3 Session Management.** Session creation,
  binding, timeout, logout. Frequent Fails: session
  cookie without HttpOnly / Secure / SameSite, session
  timeout not enforced server-side.
- **V4 Access Control.** Authorisation, deny-by-
  default, sensitive-data access controls. Frequent
  Fails: authorisation checked in some routes and
  not others; missing horizontal-authorisation
  checks (IDOR class).
- **V5 Validation / Sanitisation / Encoding.**
  Input validation, output encoding, injection
  prevention. Frequent Fails: SQL-injection risk in
  raw-query paths, XSS risk in template contexts
  that do not autoescape by default.
- **V6 Stored Cryptography.** Cryptographic
  requirements, key management. Frequent Fails: use
  of deprecated algorithms (MD5, SHA-1 for anything
  security-relevant), non-random tokens (use of
  `Math.random` for security-sensitive IDs),
  hardcoded encryption keys.
- **V7 Error Handling and Logging.** Log content,
  log protection, log retention. Frequent Fails:
  stack traces returned to the user, PII / secrets
  logged, no security-event logging at all, log
  files world-readable.
- **V8 Data Protection.** Client / server data
  protection, sensitive private data. Frequent Fails:
  sensitive data cached without controls, sensitive
  data returned in URLs.
- **V9 Communications.** TLS configuration, HTTP
  security headers. Frequent Fails: TLS 1.0 / 1.1
  still enabled, missing HSTS header, missing
  Content-Security-Policy header, mixed content.
- **V10 Malicious Code.** Subresource integrity,
  dependency checks. Frequent Fails: no SCA
  (software-composition analysis) in CI, third-
  party scripts loaded without SRI.
- **V11 Business Logic.** Rate limiting, sequential-
  step enforcement, abuse prevention. Frequent
  Fails: no rate limit on expensive endpoints, no
  abuse-monitoring, no CAPTCHA on public forms.
- **V12 Files and Resources.** File upload,
  file-integrity, file execution. Frequent Fails
  (only relevant if the product accepts uploads):
  MIME-type check by extension only, uploaded
  files served with the client-supplied MIME
  type, uploaded files stored in a web-reachable
  path.
- **V13 API and Web Service.** REST / GraphQL
  security. Frequent Fails: mass-assignment risk,
  no schema validation on inputs, no rate limit on
  authenticated endpoints.

The founder-scope discipline: walk the L1 chapter
list once as a code-review exercise, mark every
requirement Pass / Fail / N/A, and produce the gap
register. This takes 2–3 focused days for a
founder-scope codebase and can be repeated whenever
the architecture shifts substantially.

## The relationship to the OWASP Top 10

The OWASP Top 10 (current 2021, next revision under
active development — see
[owasp.org/Top10](https://owasp.org/Top10/)) is a
top-of-mind *"most critical risks"* awareness list.
The ASVS is a *verification catalog*. The two are
complementary, not substitutes:

- The Top 10 is the *"if we only fix ten things"*
  list, useful for training and for onboarding
  material.
- The ASVS is the *"here are the 130 things to
  verify"* list, useful for the gap register and the
  procurement questionnaire.

A team that has walked ASVS L1 has by construction
covered the Top 10. A team that has covered the Top
10 has not necessarily walked ASVS L1.

## Verification methods and the founder-scope tooling stack

ASVS is silent on how you verify each requirement.
The founder-scope tooling for verification:

- **SAST (Static Application Security Testing).**
  GitHub CodeQL
  ([github.com/github/codeql](https://github.com/github/codeql)),
  Semgrep
  ([semgrep.dev](https://semgrep.dev/)), or
  language-specific linters. Cover code-quality
  requirements and injection classes. Founder-scope:
  one SAST tool in CI, blocking PRs on high-severity
  findings.
- **DAST (Dynamic Application Security Testing).**
  OWASP ZAP
  ([zaproxy.org](https://www.zaproxy.org/))
  scheduled against staging, or a paid DAST vendor.
  Cover the exploited-in-the-wild classes SAST
  misses. Founder-scope: one DAST run per release
  or nightly.
- **Software Composition Analysis (SCA).**
  Dependabot
  ([docs.github.com — Dependabot](https://docs.github.com/en/code-security/dependabot)),
  Snyk, Trivy
  ([github.com/aquasecurity/trivy](https://github.com/aquasecurity/trivy)),
  osv-scanner
  ([github.com/google/osv-scanner](https://github.com/google/osv-scanner)),
  Sonatype IQ. Cover vulnerable-dependency risk.
  Founder-scope: one SCA tool in CI, weekly or
  daily dependency-update PRs (see chapter 07).
- **Secrets scanning.** Gitleaks
  ([github.com/gitleaks/gitleaks](https://github.com/gitleaks/gitleaks)),
  TruffleHog, or the GitHub / GitLab built-in
  scanners. Cover the *"credentials in git"* risk
  class. Founder-scope: pre-receive hook + CI
  block.
- **Container scanning.** Trivy, Grype, or the
  cloud registry's built-in scanning. Cover CVEs in
  base images and installed packages.
- **Manual penetration test.** Annual third-party
  engagement. Cover the classes automated tooling
  misses (business-logic flaws, chained
  vulnerabilities, authorisation model issues).

The founder-scope stack is roughly: one SAST, one
SCA, one secrets scanner, one container scanner, one
scheduled DAST or a compensating manual review, and
one annual penetration test. Every ASVS L1
requirement has a verification method it maps to;
the gap register records which method attested each
Pass.

## The `SECURITY.md` and coordinated-disclosure surface

One founder-scope AppSec artifact worth naming
separately: a published security-contact and
coordinated-disclosure policy. This lets external
researchers report vulnerabilities responsibly
before they weaponise them. Two conventions:

- **`SECURITY.md`** at the root of the source
  repository (or in `.github/`). GitHub renders this
  as a security policy tab. See
  [docs.github.com — Adding a security policy](https://docs.github.com/en/code-security/getting-started/adding-a-security-policy-to-your-repository).
- **`/.well-known/security.txt`** at the root of the
  production website. See
  [securitytxt.org](https://securitytxt.org/) — the
  file format is defined in RFC 9116.

Both should carry: contact email
(`security@yourcompany.com`), preferred language,
expected response window (usually 3 business days
for acknowledgement), acknowledgement / attribution
policy, and out-of-scope items. This is the
founder-scope substitute for a bug-bounty programme.

## The boundary to `ai-infra-security` (level 35)

ASVS L1 is the founder-scope baseline the CTO owns.
ASVS L2 is the enterprise-ready target the first
security hire drives to closure. Beyond that:

- **Deep threat modelling** — STRIDE workshops,
  attack-tree analysis, formal per-feature threat
  review — is
  [`ai-infra-security-learning`](../../../ai-infra-security-learning)
  (level 35) scope.
- **Detection engineering, WAF policy design, SIEM
  tuning, incident-response tooling** — level 35.
- **AppSec depth on specific technology stacks**
  (Kubernetes hardening, service-mesh mTLS,
  container-runtime security, cloud IAM depth) —
  level 35 or the specific platform-security tracks.
- **Adversarial ML testing, model-eval regression
  suites, red-team programmes for AI outputs** —
  [`ai-risk-engineer`](../../../ai-risk-engineer-learning)
  (level 25, AI Governance family) and
  [`senior-ai-governance-architect`](../../../senior-ai-governance-architect-learning)
  (level 50).

The founder-scope discipline: build the shell so the
first hire has somewhere to stand. A gap register
that is 70% Pass at L1, with a defensible plan for
each Fail, is what a first security hire wants to
inherit. A codebase that has never been scanned and
has no gap register is what a first security hire
has to reconstruct.

## Summary

- OWASP ASVS is the AppSec scope catalog at founder
  scale — free, versioned, levelled, structured for
  direct citation.
- Three levels: **L1 opportunistic** (founder-scope
  baseline), **L2 standard** (enterprise-ready
  target), **L3 advanced** (out of founder scope).
- The load-bearing artifact is the **gap register** —
  one row per requirement in scope, Pass / Fail /
  N/A with evidence, owner, and target close date.
  L1 gap register at first-customer deployment; L2
  gap register as the enterprise-ready roadmap.
- The chapter list (v4.x — Authentication, Session,
  Access Control, Validation, Cryptography, Logging,
  Data Protection, Communications, Malicious Code,
  Business Logic, Files, API, Configuration) walks
  the AppSec surface founder-scope teams most often
  under-verify.
- Founder-scope verification stack: one SAST, one
  SCA, one secrets scanner, one container scanner,
  one scheduled DAST or manual review, one annual
  penetration test. Each ASVS requirement maps to a
  verification method.
- Publish a `SECURITY.md` and a `security.txt` for
  coordinated disclosure. This is the founder-scope
  substitute for a bug-bounty programme.
- L1 is what the CTO owns. L2 is what the first
  security hire drives. L3 and the deep AppSec /
  detection / red-team / AI-safety depth belong to
  [`ai-infra-security`](../../../ai-infra-security-learning)
  (level 35),
  [`ai-risk-engineer`](../../../ai-risk-engineer-learning)
  (level 25), and
  [`senior-ai-governance-architect`](../../../senior-ai-governance-architect-learning)
  (level 50).

The exercise for this chapter —
`exercise-05-owasp-asvs-level-1-scoping-drill.md` —
scores your current application against ASVS L1,
produces the L1 gap register, and drafts the L2 gap
register for the enterprise-ready posture.
