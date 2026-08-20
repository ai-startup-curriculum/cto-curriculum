# SLSA and Build Provenance — The CI/CD Integrity Baseline

> "The question is no longer *did the code you wrote get
> into production*. The question is *can you prove no one
> else's code got into production alongside it*." — the
> supply-chain-security discipline this chapter is written
> around.

## Motivation

The supply-chain security incidents of the last five
years — SolarWinds
([cisa.gov — SolarWinds](https://www.cisa.gov/news-events/news/emergency-directive-21-01-mitigate-solarwinds-orion-code-compromise)),
Codecov ([about.codecov.io — Security update](https://about.codecov.io/security-update/)),
Log4Shell ([cve.mitre.org — CVE-2021-44228](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44228)),
the ongoing stream of malicious npm and PyPI package
takeovers, and the XZ Utils backdoor
([nvd.nist.gov — CVE-2024-3094](https://nvd.nist.gov/vuln/detail/CVE-2024-3094)) —
have moved *build-pipeline integrity* from a niche
concern to a first-order enterprise procurement
question. The CIO office that used to ask *"do you
scan your dependencies?"* now asks *"do you sign your
builds, produce provenance attestations, and pin your
dependencies?"*.

The answer at founder scope is *"we target SLSA Build
Level 2, and here is the provenance file from our last
release"*. SLSA (Supply-chain Levels for Software
Artifacts) is the free, open framework that lets you
say that answer without inventing it. This chapter
walks the framework, the founder-scope target level,
and the composition with the OpenSSF *Secure Software
Development Fundamentals* baseline that many procurement
questionnaires now cite directly.

## What SLSA actually is

SLSA — pronounced *salsa* — is a supply-chain security
framework maintained by the Open Source Security
Foundation (OpenSSF) under the Linux Foundation. See
the specification at [slsa.dev](https://slsa.dev/) and
the current release at
[slsa.dev/spec/v1.0](https://slsa.dev/spec/v1.0/).
Key properties for founder scope:

- **It is a framework, not a tool.** SLSA defines
  what *properties* a build system must have. Which
  specific tools you use to achieve those properties
  is your choice.
- **It has a versioned specification.** The current
  stable is v1.0 (released 2023). Older references
  to "SLSA levels 1–4 across four tracks" describe
  the pre-1.0 draft; the v1.0 specification narrows
  scope to the **Build track** with four levels
  (Build L0, L1, L2, L3), with Source and
  Distribution tracks planned for future revisions.
- **Levels are cumulative.** Every Build L2
  requirement is also a Build L3 requirement.
- **The framework is threat-model-driven.** Each
  level protects against a specific class of
  supply-chain attack (unauthorised build, tampered
  provenance, malicious builder, insider threat).

### The Build track levels (v1.0)

- **Build L0.** No requirements. A default state; do
  not describe your posture as L0 externally.
- **Build L1.** Provenance exists. The build produces
  a provenance attestation that describes what was
  built, how, and by whom. Consumers can inspect the
  provenance but cannot yet verify its integrity.
- **Build L2.** Hosted, tamper-resistant build. The
  build runs on a hosted service that produces
  signed provenance. Consumers can verify the
  provenance signature against the build service's
  identity.
- **Build L3.** Hardened, isolated build. The build
  service isolates each build such that a malicious
  actor cannot influence the build from an adjacent
  workload; the build is fully hermetic (all
  dependencies pinned by digest, no external
  network); the provenance is unforgeable even by a
  malicious builder operator.

Founder-scope target: **Build Level 2 by end of
first customer-deployment quarter**. Build L3 is a
security-team programme.

## Reaching Build L1 — provenance that exists

Build L1 requires *provenance*. A provenance
attestation is a machine-readable document that
describes:

- What artifact was built (name, hash).
- The build process (which source revision, which
  build command, which environment).
- The builder (which identity ran the build).

The industry-standard format is the
[in-toto](https://in-toto.io/) SLSA provenance
predicate — see the schema at
[slsa.dev/provenance/v1](https://slsa.dev/provenance/v1).
It is a JSON document you attach to each release
artifact.

Founder-scope path to L1:

- On every release, produce a JSON provenance file
  alongside the artifact.
- The provenance records the git commit SHA, the CI
  workflow file and commit, the build environment
  (runner OS and version), the timestamp, and the
  produced artifact digest.
- Publish the provenance alongside the release.

At founder scope, this is 10–20 lines of GitHub
Actions or GitLab CI YAML plus a small script. The
value is that *it exists* — the provenance is now
inspectable.

## Reaching Build L2 — signed provenance from a hosted builder

Build L2 requires that the build runs on a **hosted
service** — GitHub Actions, GitLab CI, Google Cloud
Build, AWS CodeBuild, or an equivalent — and that
the provenance is **signed** by an identity tied to
the build service.

Founder-scope path to L2:

- Use a hosted CI (GitHub Actions is the most common
  founder-scope choice). Do not build on developer
  laptops for release artifacts.
- Sign the provenance with a keyless signing
  mechanism. The dominant modern option is
  [Sigstore](https://www.sigstore.dev/) — see the
  cosign tool at
  [github.com/sigstore/cosign](https://github.com/sigstore/cosign) —
  which uses the CI's OIDC identity to obtain a
  short-lived signing certificate from Fulcio and
  records the signature in the Rekor transparency
  log.
- Use one of the reference generators for the CI
  system in question — for GitHub Actions, the
  [SLSA GitHub Generator](https://github.com/slsa-framework/slsa-github-generator)
  produces SLSA L3-compliant provenance out of the
  box for many artifact types; for GitLab, see
  [docs.gitlab.com — Provenance and SLSA](https://docs.gitlab.com/administration/settings/import_and_export_settings/#supply-chain-security)
  and successor documentation.
- Verify the signature and provenance on
  consumption — either explicitly with `cosign
  verify-attestation` in your deployment pipeline, or
  via GitHub's built-in attestation verification for
  container images and archives.

At founder scope, adopting the SLSA GitHub Generator
takes 1–2 hours per repository and hits L3 for
release artifacts produced through it — the framework
level is L3, though the *organisational* posture
around it is usually L2 until the hardening in the
next section is in place.

## Reaching Build L3 — hardened, isolated, hermetic

Build L3 requires:

- **Isolation between builds.** A malicious build
  cannot observe or influence adjacent builds on the
  same builder.
- **Hermetic build.** All dependencies are declared
  ahead of time and available in the build
  environment without runtime network fetch;
  dependency versions are pinned by content digest.
- **Provenance unforgeable by builder operators.** The
  build service enforces that the provenance
  accurately reflects the build; even the operator
  cannot fake it.

Founder-scope guidance: **do not commit to L3
externally**. Reference generators (SLSA GitHub
Generator with hermetic builder configurations,
Google Cloud Build hermetic mode, Bazel with
`--nobuild_python_zip` and equivalent hardening) can
get you there for specific artifact types, but the
*organisational* discipline (no manual override of
CI, no ad-hoc builds signed with the release
identity, no bypass of the isolation) is a security-
team programme. Get to L2, document the L3 gaps in
the gap register, and let the first security hire
close them.

## Dependency pinning and SBOM generation

Two founder-scope disciplines that live adjacent to
SLSA but are separately called out by every
enterprise procurement questionnaire:

### Dependency pinning

Pin every direct and transitive dependency by
version *and*, where the ecosystem supports it, by
content digest. Ecosystem-specific:

- **npm / yarn / pnpm** — commit `package-lock.json`
  / `yarn.lock` / `pnpm-lock.yaml`; enable
  `npm ci` in CI.
- **pip** — use `pip-tools` or `uv` to compile a
  fully-pinned `requirements.txt` with hashes
  (`--generate-hashes`); enable `pip install
  --require-hashes` in CI.
- **Go** — `go.sum` is required by the tooling.
- **Docker / OCI images** — pin base images by
  digest (`FROM alpine@sha256:...`), not by tag.

The founder-scope reason: without digest pinning, an
attacker who compromises the package registry can
substitute the package for a malicious version and
your CI will pull the malicious version on the next
build without any diff in your source tree.

### SBOM generation

A Software Bill of Materials (SBOM) is a machine-
readable inventory of every component in a software
artifact. The two common formats:

- **SPDX** — [spdx.dev](https://spdx.dev/) — ISO/IEC
  5962:2021 standard.
- **CycloneDX** — [cyclonedx.org](https://cyclonedx.org/) —
  OWASP-maintained.

Founder-scope tools that generate SBOMs from a
codebase or container: Syft
([github.com/anchore/syft](https://github.com/anchore/syft)),
Trivy
([github.com/aquasecurity/trivy](https://github.com/aquasecurity/trivy)),
cdxgen
([github.com/CycloneDX/cdxgen](https://github.com/CycloneDX/cdxgen)),
osv-scanner
([github.com/google/osv-scanner](https://github.com/google/osv-scanner)).

At founder scope: produce a CycloneDX or SPDX SBOM
on every release, publish alongside the release, and
retain the historical SBOMs for the artifact-
retention period. Some enterprise buyers (federal
contracts, healthcare enterprise) will ask for the
SBOM on the security questionnaire; the founder-
scope answer is *"here is the URL to the latest
SBOM"*, not *"we can generate one for you on
request"*.

## The OpenSSF Secure Software Development Fundamentals baseline

The [OpenSSF Secure Software Development
Fundamentals](https://openssf.org/education/) course
series (available free on edX) is the canonical
baseline curriculum for secure software development
practice at founder scope. The associated
[OpenSSF Best Practices Badge Program](https://www.bestpractices.dev/)
(formerly the CII Best Practices Badge) provides a
self-assessed checklist you can walk through and
publish a badge for.

The founder-scope adopters:

- Complete the *Secure Software Development
  Fundamentals* course as onboarding material for
  every engineer.
- Walk the OpenSSF Best Practices Badge criteria
  (Passing tier) as a self-assessment; publish the
  badge (or a link to the assessment) as part of
  the security posture.
- Follow the
  [OpenSSF Scorecard](https://scorecard.dev/) score
  for your own open-source repositories; use the
  scorecard as a founder-scope health check across
  the security-relevant hygiene items (branch
  protection, dependency pinning, code review,
  signed releases, etc.).

The Best Practices Badge Passing criteria correlate
strongly with SLSA Build L1–L2 posture; adopting one
tends to move you toward the other.

## The founder-scope CI/CD hardening checklist

A concrete checklist a founder-scope team can walk in
2–3 focused engineering days:

- Move all production release builds from developer
  laptops to hosted CI (GitHub Actions / GitLab CI /
  Cloud Build).
- Enable branch protection on `main` — required
  reviews (≥1), required status checks, required
  signed commits or attested commits.
- Enable required PR reviews with `CODEOWNERS`.
- Pin CI action versions by SHA, not by tag (
  `uses: actions/checkout@a5ac7e51b41094c92402da3b24376905380afc29`,
  not `@v4`).
- Enable Dependabot / Renovate for dependency updates
  and CI action updates.
- Enable secret scanning (GitHub / GitLab built-in,
  or Gitleaks pre-commit + CI).
- Add a SAST step (CodeQL / Semgrep) that blocks PRs
  on high-severity findings.
- Add an SCA step (Trivy / osv-scanner / Snyk) that
  blocks PRs on high-severity findings.
- Add an SBOM generation step (Syft / cdxgen) that
  attaches the SBOM to the release.
- Add a provenance-generation step (SLSA GitHub
  Generator or equivalent) that produces signed
  provenance.
- Verify provenance on deploy (cosign verify or the
  hosted equivalent).
- Pin base container images by digest.
- Store secrets in the CI's native secret store
  (GitHub Encrypted Secrets, GitLab CI variables,
  Cloud Secret Manager); do not store secrets in
  code or in environment files under version
  control.
- Rotate any secret that has ever been committed to
  git, regardless of whether it appears to have
  been exploited.

Each of these items is a *documented decision* in
the ISMS (chapter 02) — most naturally in the
Secure Software Development Lifecycle Policy and the
Change Management Policy — and evidence-collection
target in the SOC 2 audit.

## The boundary to `ai-infra-security` (level 35)

Founder-scope SLSA L2 posture is what the CTO owns.
Beyond that:

- **SLSA Build L3 posture** — hardened isolated
  hermetic builds at scale, provenance-verification-
  as-code across a multi-repo estate — is
  [`ai-infra-security-learning`](../../../ai-infra-security-learning)
  (level 35) scope.
- **Source track and Distribution track** (planned
  additions to the SLSA specification) will define
  requirements on the source-control side (branch
  protection, signed commits, review integrity) and
  the artifact-distribution side (registry
  hardening). Founder-scope posture: adopt the
  publicly-recommended defaults; do not build
  bespoke tooling.
- **Deep supply-chain attack detection** —
  behavioural analysis on dependency updates,
  malicious-package detection, insider-threat
  monitoring on the CI system — is level 35 scope.
- **Post-quantum signing algorithm migration** as
  NIST finalises the transition — a level 35
  concern; founder-scope posture is *"we use the
  Sigstore-recommended defaults and inherit any
  algorithm migration from the ecosystem"*.

The founder-scope discipline: adopt the reference
generators, do not roll your own, and document what
you have adopted. A first security hire can extend
this to L3 and to the wider supply-chain-security
posture; a first security hire cannot easily undo a
bespoke half-implemented build system.

## Summary

- SLSA (Supply-chain Levels for Software Artifacts) is
  the framework the industry has coalesced on for
  build-provenance. The v1.0 specification defines
  the Build track with levels L0–L3.
- **Build L1** — provenance exists (a signed or
  unsigned attestation of what was built and how).
- **Build L2** — signed provenance from a hosted
  builder; the current founder-scope target.
- **Build L3** — hardened, isolated, hermetic build;
  a security-team programme. Do not commit to L3
  externally at founder scope.
- Reference generators — the SLSA GitHub Generator
  in particular — reach L3 for many artifact types
  out of the box; the *organisational* posture
  around them stays at L2 until security-team
  hardening is in place.
- Dependency pinning by version and content digest,
  and SBOM generation on every release, are
  founder-scope disciplines that live adjacent to
  SLSA and are separately called out by every
  enterprise procurement questionnaire.
- The OpenSSF *Secure Software Development
  Fundamentals* baseline, the OpenSSF Best Practices
  Badge, and the OpenSSF Scorecard are the free,
  publicly-recognised checklists to walk against.
- The CI/CD hardening checklist (hosted CI, branch
  protection, SHA-pinned actions, dependency
  updates, secret scanning, SAST, SCA, SBOM,
  provenance, digest-pinned images, secrets-in-
  vault) is 2–3 focused engineering days at founder
  scope.
- L2 is what the CTO owns; L3, the deep supply-
  chain-detection depth, and the source/distribution
  track additions belong to
  [`ai-infra-security`](../../../ai-infra-security-learning)
  (level 35).

The exercise for this chapter —
`exercise-06-slsa-and-build-provenance-baseline.md` —
ships the SLSA Build L2 baseline for your CI/CD
pipeline plus the CI hardening checklist and the
OpenSSF baseline self-assessment.
