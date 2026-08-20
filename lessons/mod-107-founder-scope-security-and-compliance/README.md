# mod-107 — Founder-Scope Security, Privacy, and Compliance

> The minimum-viable security, privacy, and compliance
> posture a pre-seed → Series-A CTO owns before there is a
> full-time security hire in the org. The honest reckoning
> underneath the module: enterprise buyers, regulated
> customers, and Series-B acquirers will ask about SOC 2,
> ISO/IEC 27001, GDPR / CCPA, HIPAA, application security,
> and build integrity long before you can afford a
> dedicated security team, and the artifacts you can
> produce in the next 90 days decide which deals close and
> which fall out of the pipeline.

**Planned time:** 18 hours (8 chapters + 7 exercises +
1 lab + 1 quiz)
**Track:** [`cto-curriculum`](../../README.md) —
Co-Founder / CTO, level 25
**Prerequisites:** [`mod-101`](../mod-101-cto-role-and-ownership-map/README.md)
(the CTO ladder — this module's *"which posture at which
rung"* framing sits on the ladder from chapter 01),
[`mod-102`](../mod-102-architecture-under-uncertainty/README.md)
(the ADR discipline the compliance-decision artifacts
reuse; the ISO/IEC 25010 quality-attribute vocabulary the
*Security* characteristic slots into),
[`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md)
(the build-vs-buy discipline the compliance-tool
selection reuses; the vendor scorecard the DPA / BAA
acquisition drill extends),
[`mod-105`](../mod-105-technical-debt-as-business-decision/README.md)
(security debt as a quality-attribute-debt subclass; the
refactor budget the compliance-gap remediation lives
inside),
[`mod-106`](../mod-106-scaling-org-and-stack/README.md)
(the on-call rotation, incident-response playbook, and
blameless post-mortem practice the SOC 2 Availability
and Security criteria measure against).

## Learning objectives

- Scope the **founder-scope security foundation** — the
  minimum-viable posture that (a) does not scare
  enterprise buyers away, (b) does not create
  acquisition-risk debt at Series-B due diligence, and
  (c) can be handed to a first security hire without a
  rewrite. Know what to defer until that hire lands and
  what cannot wait.
- Prepare for a **SOC 2 Type I** audit — the AICPA Trust
  Services Criteria (Security / Availability /
  Processing Integrity / Confidentiality / Privacy),
  scope selection, ISMS shape, and evidence-collection
  cadence at pre-seed / seed scale; know that **Type II
  is a 6–12 month observation window** and plan the
  cadence backward from the customer commitment that
  requires it.
- Position **ISO/IEC 27001:2022** as the international-
  buyer equivalent signal — ISMS scope, Statement of
  Applicability, Annex A controls; know **when** to
  pursue it (typically after Type II, or earlier in
  EU-heavy account bases where SOC 2 alone does not
  clear procurement).
- Ship a **GDPR / CCPA** baseline for the SaaS data
  flow — records of processing activities (Article 30),
  data-subject-request handling, DPA templates for
  downstream vendors, data-residency choices, cookie
  consent, and the customer-facing privacy notice.
- Ship a **HIPAA baseline** where the startup handles
  PHI — the Security Rule technical safeguards, audit
  controls, and BAAs with the foundation-model vendors
  that offer them (Anthropic Claude Enterprise, OpenAI
  API BAA path, AWS Bedrock, Azure OpenAI, GCP Vertex);
  distinguish **PHI-touching** from **PHI-adjacent**
  architectures so the scope stays honest.
- Adopt the **OWASP Application Security Verification
  Standard (ASVS)** as the AppSec scope catalog at
  founder scale — **Level 1** as the founder baseline;
  **Level 2** as the enterprise-ready posture the first
  security hire drives toward.
- Adopt **SLSA build-provenance basics** for the CI/CD
  pipeline — signed builds, tamper-evident provenance,
  and dependency pinning at the level the OpenSSF
  *Secure Software Development Fundamentals* baseline
  recommends.
- Acquire vendor **DPAs and BAAs** from foundation-model
  providers and the wider SaaS stack — which providers
  offer BAA (Anthropic Claude Enterprise, OpenAI API
  BAA path, AWS Bedrock, Azure OpenAI, GCP Vertex),
  which offer zero-retention API modes, and which are
  compatible with EU-only data-residency.
- Cite the boundary to
  [`security-learning` / `ai-infra-security`](../../../ai-infra-security-learning)
  (level 35) on deep security engineering depth and to
  [`senior-ai-governance-architect`](../../../senior-ai-governance-architect-learning)
  (level 50) /
  [`ai-risk-engineer`](../../../ai-risk-engineer-learning)
  (level 25, AI Governance family) on deep AI governance
  and risk-engineering depth.
- Cite the boundary to **legal counsel** — the CTO
  briefs counsel with a defensible package (data-flow
  diagram, sub-processor list, control mapping, incident
  history) but does not deliver legal opinion. Counsel
  turns the package into contract language, regulator
  correspondence, and privileged advice.

## Chapters

1. [The Founder-Scope Security Posture — What to Own, What to Defer](01-founder-scope-security-posture.md) — the minimum-viable posture; the four founder-scope questions (enterprise buyers, acquisition risk, hand-off to first hire, deferrable-until-then); the boundary to `security-learning` / `ai-infra-security` (level 35), `senior-ai-governance-architect` (level 50), `ai-risk-engineer` (level 25), and to legal counsel.
2. [SOC 2 Type I Readiness — Trust Services Criteria, Scope, ISMS, Evidence](02-soc-2-type-i-readiness.md) — the AICPA Trust Services Criteria; the *"which of the five"* scope call; the small-team ISMS shape; the evidence-collection cadence that becomes the Type II observation window; the Type-I-to-Type-II timeline planned backward from the first enterprise commitment.
3. [ISO/IEC 27001:2022 — The International-Buyer Signal](03-iso-27001-international-signal.md) — ISO/IEC 27001:2022 as the international equivalent of SOC 2; ISMS scope, Statement of Applicability, and the Annex A control set (93 controls in four themes); when to pursue it (usually after Type II or in EU-heavy account bases); how it composes with SOC 2 rather than duplicating.
4. [GDPR and CCPA — The SaaS Data-Flow Baseline](04-gdpr-and-ccpa-baseline.md) — the two regimes' scope triggers; controller / processor / sub-processor vocabulary; Article 30 records of processing activities; data-subject-request handling; the DPA template for downstream vendors; data-residency choices; cookie consent; the customer-facing privacy notice; the boundary to counsel for legal-basis and cross-border-transfer opinion.
5. [HIPAA at Founder Scale — Safeguards, Audit Controls, and Which BAAs You Can Actually Get](05-hipaa-baseline-and-phi-scoping.md) — the *PHI-touching vs. PHI-adjacent* scope call; the Security Rule technical safeguards (access control, audit controls, integrity, transmission security); the BAA acquisition list for foundation-model vendors (Anthropic, OpenAI, AWS Bedrock, Azure OpenAI, GCP Vertex) and their conditions; the "don't handle PHI" architecture as a legitimate option.
6. [OWASP ASVS — The AppSec Scope Catalog at Founder Scale](06-owasp-asvs-as-appsec-catalog.md) — ASVS v4.x as the AppSec scope catalog; the three levels (L1 opportunistic, L2 standard for regulated / enterprise SaaS, L3 advanced); L1 as the founder baseline and L2 as the enterprise-ready posture; the gap-register format; the boundary to `ai-infra-security` (level 35) for the deep AppSec depth beyond the founder scope.
7. [SLSA and Build Provenance — The CI/CD Integrity Baseline](07-slsa-and-build-provenance.md) — the SLSA framework (levels 1–4); signed builds, provenance attestations, and hermetic builds; the OpenSSF *Secure Software Development Fundamentals* baseline; dependency pinning and SBOM generation; the pragmatic *"SLSA Build L2 by end of quarter"* target for the founder-scope CI/CD.
8. [Vendor DPAs and BAAs — Acquiring the Downstream Compliance Artifacts](08-vendor-dpa-and-baa-acquisition.md) — the vendor compliance inventory; DPA acquisition process (self-serve vs. sales-assisted vs. custom-redlined); BAA acquisition for foundation-model providers and the compliance-tier gate that unlocks them; zero-retention API modes; EU-only data-residency options; the vendor-artifact library that becomes the SOC 2 sub-processor evidence.

## Exercises

1. [Founder-Scope Security Posture Drill](exercises/exercise-01-founder-scope-security-posture-drill.md) — ~2 hours. Author the one-page posture memo for your startup that answers the four founder-scope questions (enterprise buyers, acquisition risk, hand-off, deferral list) with concrete evidence.
2. [SOC 2 Type I Readiness Checklist](exercises/exercise-02-soc-2-type-i-readiness-checklist.md) — ~3 hours. Author the SOC 2 Type I readiness checklist for your startup — scope selection across the five TSC, small-team ISMS shape, evidence-collection cadence, the timeline planned backward from the first enterprise commitment.
3. [GDPR and CCPA SaaS Baseline Drill](exercises/exercise-03-gdpr-and-ccpa-saas-baseline-drill.md) — ~3 hours. Ship the GDPR / CCPA baseline: RoPA v0, DSR handling process, DPA template, data-residency decision, cookie-consent posture, customer-facing privacy notice.
4. [HIPAA BAA and Technical Safeguards Drill](exercises/exercise-04-hipaa-baa-and-technical-safeguards-drill.md) — ~2 hours. Decide *PHI-touching vs. PHI-adjacent* for your architecture; if PHI-touching, ship the technical-safeguards map and the BAA acquisition list for every downstream vendor that will see PHI.
5. [OWASP ASVS Level 1 Scoping Drill](exercises/exercise-05-owasp-asvs-level-1-scoping-drill.md) — ~2 hours. Score the current app against ASVS L1 requirements; produce a gap register with owner and due date per gap; produce the L2 gap register for the enterprise-ready posture.
6. [SLSA and Build-Provenance Baseline](exercises/exercise-06-slsa-and-build-provenance-baseline.md) — ~2 hours. Ship the SLSA Build Level 2 baseline for the CI/CD pipeline — signed builds, provenance attestations, dependency pinning, SBOM generation, and the OpenSSF *Secure Software Development Fundamentals* checklist as a `docs/security/` sub-tree.
7. [Vendor DPA and BAA Acquisition Drill](exercises/exercise-07-vendor-dpa-and-baa-acquisition-drill.md) — ~2 hours. Author the vendor compliance inventory; run the DPA / BAA acquisition process for the top-10 vendors; produce the sub-processor list that becomes the SOC 2 and GDPR evidence.

## Lab

- `lab-01-publish-a-founder-scope-security-and-compliance-package`
  (~2 hours) — planned. Consolidates the seven
  exercise outputs into a single `docs/compliance/`
  sub-tree in the working repo: the posture memo, the
  SOC 2 readiness checklist, the GDPR / CCPA baseline,
  the HIPAA scope call (with the BAA list where
  applicable), the ASVS gap register, the SLSA
  build-provenance plan, and the vendor DPA / BAA
  inventory. The sub-tree is the single artifact that
  answers *"what's your security posture?"* on a
  design-partner call, and is the direct input to the
  capstone [`project-102`](../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package).

## Quiz

- One quiz (~30 min) covering: the four founder-scope
  posture questions; the five Trust Services Criteria
  and the scope-selection call; the Type I vs. Type II
  timing gap and the observation window; the ISO/IEC
  27001:2022 ISMS + SoA + Annex A structure and the
  *when to pursue* trigger; the Article 30 RoPA
  requirement, the DSR-response clock, and the
  controller / processor / sub-processor role split;
  the PHI-touching vs. PHI-adjacent scope call and the
  BAA acquisition list for the foundation-model
  vendors; the three ASVS levels and the L1 baseline;
  the SLSA Build levels and the OpenSSF baseline; the
  vendor-artifact library and the DPA / BAA
  acquisition process; the boundary to
  [`security-learning` / `ai-infra-security`](../../../ai-infra-security-learning),
  [`senior-ai-governance-architect`](../../../senior-ai-governance-architect-learning),
  [`ai-risk-engineer`](../../../ai-risk-engineer-learning),
  and to legal counsel.

## Resources

See [`resources.md`](resources.md) for the module's
primary references. Full citations for the whole
curriculum are in
[`.aicg/job-requirements.json`](../../.aicg/job-requirements.json)
under `authoritative_references`.

## What comes next

Once you have completed the exercises here,
[`mod-108`](../mod-108-cto-ceo-and-board-communication)
(*The CTO↔CEO Relationship, Board Communication, and
Technical Due Diligence*) is the natural next module —
the compliance package produced here is one of the
load-bearing sections of the technical-due-diligence
data room, and the SOC 2 posture is one of the
recurring board pre-read line items at Series-A and
beyond.

This module feeds directly into the capstone
[`project-102`](../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package)
(*SOC 2 Type I Readiness and Founder-Scope Compliance
Package*), whose deliverables are the polished form of
the seven exercises above.
