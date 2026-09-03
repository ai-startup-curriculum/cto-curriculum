# Exercise 06 — SLSA and Build-Provenance Baseline

**Module:** `mod-107-founder-scope-security-and-compliance`
**Planned time:** ~2 hours
**Chapter this builds on:** [`07-slsa-and-build-provenance.md`](../07-slsa-and-build-provenance.md),
supported by [`06-owasp-asvs-as-appsec-catalog.md`](../06-owasp-asvs-as-appsec-catalog.md)
for the CI-embedded SCA / secrets / SAST tooling
positions and [`02-soc-2-type-i-readiness.md`](../02-soc-2-type-i-readiness.md)
for the SOC 2 CC8 (change management) evidence
targets the baseline satisfies.

## Problem statement

Ship the **SLSA Build Level 2 baseline** for the
CI/CD pipeline of your primary release artifact
(container image, npm package, Python wheel, Go
binary, mobile bundle — whichever is the artifact
your production environment consumes). Then
publish the founder-scope CI/CD hardening checklist
and the OpenSSF *Secure Software Development
Fundamentals* self-assessment as a `docs/security/`
sub-tree that becomes the SOC 2 CC8 evidence.

The point of the drill is not to *reach SLSA Build
L3* (that is a security-team programme). The point
is to (a) move release builds off developer
laptops onto a hosted CI, (b) attach signed
provenance to every release artifact, (c) pin
dependencies and CI actions, (d) generate an SBOM
on every release, and (e) document the posture as
a checklist a compliance auditor and a first
security hire can inherit.

## Requirements

Ship the artifacts under `docs/security/` and the
corresponding CI configuration under the working
repo's `.github/workflows/` (or the equivalent for
your CI system).

### Artifact 1 — SLSA posture memo (`slsa-posture.md`)

A one-page memo naming:

- The **release artifact(s)** in scope (container
  image, npm package, Python wheel, Go binary,
  mobile bundle) with the registry / distribution
  channel each publishes to.
- The **SLSA specification version** you targeted
  (v1.0 at time of writing — verify at
  [slsa.dev/spec/v1.0](https://slsa.dev/spec/v1.0/)).
- The **level target per artifact** — Build L2 as
  the founder-scope target; note per artifact if
  the reference generator (SLSA GitHub Generator
  or equivalent) actually delivers L3-compliant
  provenance out of the box.
- The **builder** (GitHub Actions / GitLab CI /
  Google Cloud Build / AWS CodeBuild / other) and
  the reason for the choice.
- The **provenance format** (in-toto SLSA
  Provenance v1 predicate; cite
  [slsa.dev/provenance/v1](https://slsa.dev/provenance/v1)).
- The **signing mechanism** (Sigstore cosign
  keyless via CI OIDC; alternative if not
  Sigstore).
- The **verification step** — where in the deploy
  pipeline the provenance signature is checked
  before the artifact is promoted.
- The **L3 gap** — the specific hardening items
  deferred to the first security hire (isolation
  posture, hermetic build hardening, no-manual-
  override discipline).

### Artifact 2 — CI/CD workflow with provenance and SBOM

Extend the release workflow to produce, on every
tagged release:

- The **release artifact** (container image, npm
  package, Python wheel, Go binary, mobile
  bundle).
- A **signed SLSA provenance attestation** using
  the SLSA GitHub Generator
  ([github.com/slsa-framework/slsa-github-generator](https://github.com/slsa-framework/slsa-github-generator))
  or the equivalent for your builder. The
  attestation is published alongside the artifact
  (as an OCI artifact for container images; as a
  release asset for other artifact types).
- A **CycloneDX or SPDX SBOM** using Syft
  ([github.com/anchore/syft](https://github.com/anchore/syft))
  or an equivalent generator. The SBOM is
  published alongside the artifact.
- A **verification step** on the deploy side that
  fails the deploy if signature or provenance
  verification does not pass (cosign
  verify-attestation, or the hosted equivalent).

Commit the workflow file(s) with the exercise
output. If your working repo is a scaffold that
does not yet publish a release artifact, produce
a **template workflow** in `docs/security/ci-
workflow-template.yml` (or equivalent) with the
same shape, ready to drop into a real repo.

### Artifact 3 — Dependency-pinning discipline (`dependency-pinning.md`)

A short memo documenting, per language / ecosystem
the codebase uses:

- **How dependencies are pinned** by version — the
  lockfile committed (`package-lock.json`,
  `yarn.lock`, `pnpm-lock.yaml`, `requirements.txt`
  produced by `pip-tools` / `uv`, `Cargo.lock`,
  `go.sum`, `poetry.lock`).
- **How dependencies are pinned** by content digest
  where the ecosystem supports it (`--generate-
  hashes` for pip; `--require-hashes` on install;
  digest-pinned base images in Dockerfiles).
- **The dependency-update automation** — Dependabot
  ([docs.github.com — Dependabot](https://docs.github.com/en/code-security/dependabot))
  or Renovate
  ([docs.renovatebot.com](https://docs.renovatebot.com/))
  configuration; the update cadence (daily /
  weekly); the auto-merge policy for low-risk
  updates.
- **The CI-action-pinning discipline** — whether
  actions in `.github/workflows/` are pinned by
  SHA (required for L2) or by tag (not
  sufficient for L2). Cite the security-hardening
  guidance at
  [docs.github.com — Security hardening for GitHub Actions](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions).

Where an ecosystem's pinning is not yet in place,
name the gap and the remediation plan.

### Artifact 4 — Founder-scope CI/CD hardening checklist (`ci-hardening-checklist.md`)

Walk the checklist from chapter 07 and mark each
item Pass / Partial / Gap with evidence per row.
The items:

- Release builds run on hosted CI, not developer
  laptops.
- Branch protection on `main` — required reviews
  (≥1), required status checks, required signed
  commits or attested commits.
- Required PR reviews with `CODEOWNERS`.
- CI action versions pinned by SHA, not by tag.
- Dependabot / Renovate enabled for both
  dependency updates and CI action updates.
- Secret scanning enabled (GitHub / GitLab
  built-in or Gitleaks
  ([github.com/gitleaks/gitleaks](https://github.com/gitleaks/gitleaks))
  in CI).
- SAST step blocking PRs on high-severity
  findings (CodeQL / Semgrep — cross-reference
  from exercise 05).
- SCA step blocking PRs on high-severity findings
  (Trivy / osv-scanner / Snyk — cross-reference
  from exercise 05).
- SBOM generation step attaching the SBOM to
  each release.
- SLSA provenance generation step producing
  signed provenance for each release.
- Provenance verified on deploy.
- Base container images pinned by digest.
- CI secrets stored in the CI's native secret
  store (never in source code or version-
  controlled config).
- Any secret ever committed to git has been
  rotated.

For each Gap or Partial row, name the owner and
target close date.

### Artifact 5 — OpenSSF baseline self-assessment (`openssf-baseline.md`)

A one-page document naming:

- The **OpenSSF Best Practices Badge** tier the
  project self-assesses at (Passing / Silver /
  Gold) with a link to the assessment at
  [bestpractices.dev](https://www.bestpractices.dev/).
  Passing is the founder-scope target; Silver
  and Gold are enterprise-ready posture the
  first security hire drives to.
- The **OpenSSF Scorecard** results if the
  primary repo is public (or the internal
  equivalent posture check) — see
  [scorecard.dev](https://scorecard.dev/).
- The **OpenSSF Secure Software Development
  Fundamentals** onboarding requirement — the
  free edX course
  ([openssf.org/education](https://openssf.org/education/))
  as onboarding material for every engineer;
  whether it is in the onboarding checklist or
  a gap on the roadmap.

### Cover memo (`README.md` in `docs/security/`)

If exercise 05 already produced a
`docs/security/README.md`, extend it with the
links to the SLSA posture, CI workflow, pinning
memo, hardening checklist, and OpenSSF
self-assessment. Otherwise, produce a one-page
cover memo linking all five artifacts.

## Starter guidance

- **Do not roll your own provenance generator.**
  The SLSA GitHub Generator (or the equivalent
  for your builder) is the reference implementation.
  A rolled-your-own generator is exactly the kind
  of *"security-team programme"* that founder scope
  should not build — pick the reference tool and
  document the choice in the posture memo.
- **Start with the artifact you actually ship to
  production.** If the SaaS is a hosted service
  running a container image, the container image
  is the artifact — do that one first. Do not
  start with the npm package your SDK team
  publishes on the side; that is a follow-up.
- **Sigstore keyless is the default.** Cosign
  keyless signing using the CI's OIDC identity is
  the industry-standard mechanism. See
  [github.com/sigstore/cosign](https://github.com/sigstore/cosign)
  and the tutorial at
  [docs.sigstore.dev](https://docs.sigstore.dev/).
  Do not maintain long-lived signing keys unless
  you have a specific reason.
- **The verification step is the whole point.**
  Producing provenance and not verifying it on
  deploy is checkbox compliance. The deploy
  pipeline must reject an artifact whose
  provenance signature does not verify. If your
  deploy pipeline is *"push image, kubectl
  apply"* without a verify step, that is the top
  gap.
- **SHA-pin CI actions.** *"uses: actions/
  checkout@v4"* looks safer than it is — the tag
  can be re-pointed by a compromised repo owner.
  Pin to a full SHA. Dependabot can update the
  SHA on version bumps.
- **The dependency-pinning discipline extends
  beyond your app's dependencies.** Base images,
  CI actions, and (for cloud-native workloads)
  Helm charts and Terraform providers all need
  the same treatment. Cover each in the pinning
  memo.
- **The SBOM must actually be inspectable.**
  Publishing an SBOM in a format nobody in your
  supply chain can consume (a custom format,
  hidden in a private registry with no access
  path) is not the same as publishing an SBOM.
  Prefer CycloneDX or SPDX and publish at a URL
  a customer's security team can fetch.
- **Rotate any secret that has ever been
  committed to git.** Even if the commit was
  reverted or the file was deleted. Git history
  makes secrets accessible to anyone with clone
  access; assume they have been extracted.
- **The OpenSSF Best Practices Badge is a
  self-assessment.** Walk it once, publish the
  Passing tier, and re-walk it annually. Silver
  and Gold are for later.
- **Do not commit to L3 externally.** The
  posture memo may note that the SLSA GitHub
  Generator delivers L3-compliant provenance for
  a specific artifact type; the *organisational*
  posture is L2 until the first security hire
  closes the L3 gaps. Say so plainly.

## Acceptance criteria

Your drill output is complete when:

- The SLSA posture memo names the artifacts,
  SLSA version, level target, builder,
  provenance format, signing mechanism,
  verification point, and L3 gaps.
- A CI/CD workflow (or a template workflow)
  produces signed provenance and an SBOM on
  every release, with verification enforced on
  the deploy side.
- The dependency-pinning memo covers every
  language / ecosystem in the codebase, plus
  the CI-action-pinning discipline; every gap
  has an owner and a target close date.
- The CI/CD hardening checklist marks each of
  the 14 items Pass / Partial / Gap with
  evidence; every Gap / Partial row has an
  owner and target close date.
- The OpenSSF baseline self-assessment names
  the Best Practices Badge tier targeted, the
  Scorecard result (if applicable), and the
  onboarding-course requirement status.
- The cover memo links all five artifacts.
- A first security hire could inherit the
  `docs/security/` sub-tree and know within 20
  minutes what the current posture is, what
  the top three gaps are, and what the plan is
  to reach L3.
- Every citation to SLSA, OpenSSF, Sigstore, or
  a specific reference generator points to the
  primary source.

## What this feeds into

- **Exercise 01 (posture memo) — Section 3**
  takes the *"CI/CD targets SLSA Build Level 2
  by [target date] with signed builds,
  dependency pinning, and provenance
  attestations"* clause from this baseline.
- **Exercise 02 (SOC 2 readiness) — CC8**
  (change management) — the CI/CD hardening
  checklist and the provenance workflow are the
  primary evidence artifacts.
- **Exercise 05 (ASVS L1 register)** — the
  SCA / secrets / SAST tooling positions in
  the CI hardening checklist cross-reference
  with several ASVS V10 (malicious code) and
  V14 (configuration) requirements.
- **The module lab** consolidates the SLSA
  baseline with the other exercise outputs into
  a single `docs/compliance/` sub-tree.
- **Capstone
  [`project-102`](../../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package)** —
  the SLSA baseline is one deliverable of the
  project; the SOC 2 CC8 evidence packet is
  another that this drill directly feeds.

The drill's discipline is *adopting the reference
generators and documenting what you have adopted*.
A founder-scope CI/CD pipeline that emits signed
provenance and an SBOM on every release is a
posture the first security hire can extend; one
that emits nothing is a posture they have to
build from scratch.
