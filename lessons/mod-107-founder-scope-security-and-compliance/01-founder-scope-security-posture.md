# The Founder-Scope Security Posture — What to Own, What to Defer

> "The role of the CTO before there is a security team is
> to build a posture the first security hire *inherits*,
> not one they have to *rewrite*." — the framing this
> module is organised around.

## Motivation

Every founder-CTO in the seed → Series-A window ends up
in some version of this meeting:

- **The enterprise design partner:** *"Send over your
  SOC 2 report, your DPA, your sub-processor list, your
  penetration-test summary, and your data-flow diagram
  before we can move to a paid contract."*
- **The seed-stage CTO:** *"...we don't have those yet."*
- **The design partner:** *"When will you?"*
- **The seed-stage CTO:** *"..."*

The mistake in that meeting is not the missing SOC 2
report. The mistake is that the CTO has no **defensible
posture** to describe in the interim — no articulation of
which controls are in place, which are on a roadmap, and
which are deliberately deferred. Enterprise procurement
teams have seen the *"we are working on it"* answer a
hundred times; the answer that actually keeps the deal
alive is the one-page posture memo that names what you
own, what you defer, and when the deferral ends.

This chapter is the scoping layer for the rest of the
module. Chapters 02–08 give you the artifacts (SOC 2 Type
I readiness, ISO/IEC 27001 posture, GDPR / CCPA
baseline, HIPAA scope call, OWASP ASVS, SLSA build
provenance, vendor DPA / BAA library). This chapter tells
you which of those artifacts belong in the founder-scope
package **now** and which are deliberately deferred until
the first full-time security hire lands.

## The four founder-scope questions

Any decision about *"should we invest in this security
control now?"* at pre-seed / seed / Series-A should be
answered against four questions in order. The order
matters: the enterprise-buyer question comes first because
it is the one that most directly threatens revenue; the
first-security-hire question comes last because it is the
one that is easiest to defer without immediate cost.

### Question 1 — Does the absence of this control lose us enterprise deals?

Enterprise procurement, mid-market IT, and any regulated
buyer (healthcare, finance, government, education) has a
standard vendor-security questionnaire — often derived
from the Cloud Security Alliance CAIQ
([cloudsecurityalliance.org — CAIQ](https://cloudsecurityalliance.org/artifacts/consensus-assessments-initiative-questionnaire-caiq-v4/))
or the SIG (Shared Assessments)
([sharedassessments.org — SIG](https://sharedassessments.org/sig/)) —
that they will send you before signing. The controls
they screen on are surprisingly consistent:

- SOC 2 Type I or Type II attestation (or a credible
  path to one within a stated window).
- A signed DPA / MSA with the customer.
- A published sub-processor list and change-notice
  process.
- MFA / SSO for administrative access.
- Encryption in transit and at rest.
- A named incident-response process with a customer-
  notification clock.
- A published data-retention and data-deletion policy.
- Access-control review and off-boarding evidence.

If your posture is silent on any of the items in this
list, the deal enters *"procurement will get back to
you"* purgatory. The founder-scope posture must have a
credible answer to each — either *"in place, here is
evidence"* or *"on the roadmap, target date, here is the
compensating control"*.

### Question 2 — Does the absence of this control create acquisition-risk debt?

Series-B and later diligence — see the a16z technical-
due-diligence checklist
([a16z.com/tech-diligence-checklist](https://a16z.com/tech-diligence-checklist/))
for the public-facing version — treats security debt as a
first-order valuation issue. A missing artifact discovered
in DD is not fatal; a *pattern* of missing artifacts is a
price cut. The pattern that most reliably shows up in
diligence:

- No SOC 2 report and no ISMS documentation → *"the
  acquirer will have to build the entire compliance
  substrate from scratch"*.
- No dependency inventory / SBOM → *"we cannot bound
  the supply-chain risk"*.
- No incident-history log → *"we cannot bound the
  incident-frequency baseline"*.
- No signed BAAs with any vendor that touched PHI →
  *"the target may have HIPAA exposure we can't scope"*.
- No published sub-processor list → *"we cannot bound
  the cross-border data-transfer risk"*.

The rule at founder scope: **you do not need every
artifact by Series-A, but you do need every artifact you
have committed to in a customer contract, in a privacy
notice, or in a public-facing statement**. The gap
between the commitment and the evidence is the debt.

### Question 3 — Can the current posture be handed to a first security hire without a rewrite?

The first security hire — usually a Head of Security or a
Security Engineer 2–3 quarters after Series-A funding —
will inherit whatever you have built. Two patterns are
common; only one is useful:

- **Useful pattern.** The founder-scope posture is a
  short set of *documented* decisions: policies live in
  `docs/security/`, controls live in a control-mapping
  spreadsheet, evidence lives in a shared drive with a
  monthly collection cadence. The first hire reads the
  package in a day, disagrees with two decisions, keeps
  the rest, and extends.
- **Un-useful pattern.** The founder-scope posture
  lives entirely in the CTO's head. Vendors were
  onboarded ad-hoc; DPAs were signed but never
  centrally filed; incident retros were held on Slack
  and never written up; MFA was deployed to some tools
  but not others. The first hire spends their first
  quarter reconstructing the posture rather than
  extending it.

The founder-scope discipline is not depth — it is
**write-down**. Every decision you make now becomes an
artifact the first security hire can either extend or
consciously replace. Undocumented decisions become
rework.

### Question 4 — What can be deferred until the first security hire lands?

The list of legitimately deferrable items is longer than
most founders realise. A rough founder-scope deferral
list — items that a first-year security hire will build
correctly if you have not built them incorrectly first:

- **Formal threat modelling** (STRIDE workshops,
  attack-tree analysis, per-feature security review).
  Defer; ASVS L1 self-assessment (chapter 06) is a
  sufficient founder-scope substitute.
- **Bug-bounty programme.** Defer; a private-disclosure
  policy at `SECURITY.md` in the root of the repo
  (see [securitytxt.org](https://securitytxt.org/) and
  the [GitHub security policy docs](https://docs.github.com/en/code-security/getting-started/adding-a-security-policy-to-your-repository))
  is a sufficient founder-scope substitute.
- **Formal penetration test** beyond the SOC 2 Type II
  observation-window requirement. Defer; a lightweight
  third-party pen test annually is fine at founder
  scope.
- **SIEM / SOC / 24×7 security operations centre.**
  Defer; cloud-native audit logs (CloudTrail, Cloud
  Audit Logs, Azure Monitor) piped to a queryable
  store are sufficient at founder scope.
- **Formal risk register** beyond the Statement of
  Applicability's control mapping. Defer; the SoA
  itself (chapter 03) is the founder-scope risk
  register.
- **Dedicated data-protection officer role.** Defer
  unless GDPR Article 37 explicitly triggers (large-
  scale monitoring, special-category processing) — see
  [ICO — DPO](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/accountability-and-governance/data-protection-officers/)
  and [EDPB Guidelines 1/2017 on DPOs](https://www.edpb.europa.eu/our-work-tools/our-documents/guidelines/guidelines-12017-data-protection-officers-dpos_en).
- **Formal secure-SDLC programme, secure-coding
  training, quarterly awareness training beyond the
  onboarding checkbox.** Defer; the ASVS L1 checklist
  plus an onboarding security module is sufficient.

The load-bearing sentence: **the founder-scope posture
must not contradict what the first security hire will
build**. If your MFA rollout uses a vendor the first hire
will replace, that is fine; if your MFA rollout skips
your production database, the first hire has to redo the
work and defend the delay to the board.

## The founder-scope posture, in one paragraph

The one-paragraph articulation the CTO should be able to
give from memory on a design-partner call:

> *"We run our SaaS on [cloud], with tenant isolation
> at [layer], encryption in transit via TLS 1.2+ and at
> rest via cloud-managed keys, SSO / MFA on all admin
> access via [vendor], centralised audit logging via
> [tool], a documented incident-response runbook with a
> [N-hour] customer-notification clock, DPAs and where
> applicable BAAs signed with every sub-processor
> including [foundation-model vendor], a published
> sub-processor list at [URL], a SOC 2 Type I report
> [issued / in progress with a target date of], and a
> Type II observation window [starting / underway /
> completed]. Our GDPR / CCPA baseline covers Article 30
> RoPA, DSR handling within the statutory clock, and
> the DPA-with-sub-processors chain. We use OWASP ASVS
> as our AppSec catalog at Level 1 with a gap register
> for the [N] items we have not yet closed. Our CI/CD
> targets SLSA Build Level 2 by [target date] with
> signed builds, dependency pinning, and provenance
> attestations."*

Every clause of this paragraph is a chapter in this
module. If any clause has to be replaced with *"we
haven't figured that out yet"*, the corresponding chapter
tells you the founder-scope way to close the gap.

## The boundary to `security-learning` / `ai-infra-security`

Founder-scope security is deliberately **shallow and
broad**: the CTO owns the *scoping* of every posture
line, and the *evidence-collection cadence* that keeps
each one honest. Everything past that scope belongs to a
dedicated security engineer.

The specific hand-off list — what the first security
hire (typically at
[`ai-infra-security-learning`](../../../ai-infra-security-learning)
level 35) will own from day one:

- Deep application-security work — threat modelling
  workshops, secure-code review at scale, DAST / SAST
  tuning, WAF policy design, dependency vulnerability
  triage as a full workflow rather than as monthly
  Dependabot bulk-merge.
- Cloud security engineering — IAM policy hardening
  beyond the SOC 2 baseline, workload identity, network
  segmentation, encryption-key lifecycle management,
  cloud-security-posture-management tuning.
- Detection and response engineering — SIEM design and
  tuning, detection-as-code, incident-response tooling,
  forensic-readiness posture, table-top exercises.
- Vulnerability management as a lifecycle — SLA-driven
  vulnerability triage, exception-tracking, patch
  cadence, EOL-inventory management.
- SOC 2 Type II *sustainment* beyond the first
  observation window — quarterly control testing,
  evidence-collection automation, auditor liaison as an
  ongoing craft rather than a one-time exercise.
- ISO/IEC 27001 *maintenance* beyond initial
  certification — annual surveillance audits, internal-
  audit programme, corrective-action management, ISMS
  performance metrics.

The founder-scope discipline is to build the *shell* of
each of these so the first hire has somewhere to stand.
Building the shell wrong is worse than building nothing
at all — chapter 03 on ISO/IEC 27001 will walk the *"do
not build a real ISMS you cannot maintain"* pathology in
more detail.

## The boundary to `senior-ai-governance-architect` and `ai-risk-engineer`

AI governance is a related but distinct discipline.
Where security asks *"can an attacker read, modify, or
deny our data?"*, AI governance asks *"is our AI system
behaving in a way our stakeholders can defend?"*. The
overlap at founder scope is real but small; the depth
belongs to a dedicated role.

The founder-scope AI-governance posture is:

- Vendor selection with the AI-safety artifacts already
  in scope — see the model-card, system-card, and
  responsible-scaling-policy publications from the
  frontier providers (Anthropic, OpenAI, Google
  DeepMind).
- BAA / DPA acquisition (chapter 08) for the
  foundation-model providers that offer them.
- Zero-retention API modes selected where PII, PHI, or
  regulated data enters the prompt (chapter 08).
- Documented human-in-the-loop for high-risk
  inferences (medical, legal, financial, hiring, credit,
  housing — the categories the EU AI Act designates
  high-risk and the FTC has enforcement history on).
- An audit-log of AI system outputs for the same
  categories.

Everything beyond that — a formal AI risk register, red-
teaming programme, model-eval regression suites,
policy-as-code for prompt / output filtering, an AI
incident-response function distinct from security IR —
belongs to
[`ai-risk-engineer`](../../../ai-risk-engineer-learning)
(level 25, AI Governance family) and
[`senior-ai-governance-architect`](../../../senior-ai-governance-architect-learning)
(level 50). The founder-scope CTO cites those roles as
the owners of the follow-ups they cannot close alone.

## The boundary to legal counsel

The single most-abused sentence in early-stage compliance
work is *"the CTO said we're compliant"*. The CTO does
not deliver legal opinion. Counsel does.

The founder-scope discipline is that the CTO produces a
**defensible package** — data-flow diagram, sub-processor
inventory, control mapping, incident-history log, DPA and
BAA copies, privacy notice draft, evidence collection
manifest — that counsel can turn into:

- Contract language (customer DPAs, vendor MSAs, BAA
  redlines).
- Regulator correspondence (breach notifications under
  GDPR Article 33, HHS OCR breach reports, state
  attorney general notices under state breach laws).
- Board memoranda under privilege.
- Advice on cross-border data transfer, legal-basis
  analysis under GDPR Article 6 / 9, and sub-processor
  onward-transfer risk.

The tell that the boundary has been crossed the wrong
way: any sentence in a customer contract, a public
statement, or a regulator response that the CTO drafted
without counsel review. The reverse tell — counsel is
drafting substantive technical controls without CTO
input — is equally problematic. Counsel and CTO ship
together; neither ships without the other.

## Summary

- Four founder-scope questions decide whether a
  control belongs in the *now* posture: enterprise-
  deal risk (Q1), acquisition-DD risk (Q2), hand-off
  to the first security hire without rewrite (Q3),
  and *what is legitimately deferrable* (Q4).
- The founder-scope posture is **shallow and broad**:
  the CTO owns scope and evidence cadence, not the
  depth of any single control family.
- The load-bearing artifact is a **one-paragraph
  posture articulation** the CTO can give from memory
  on a design-partner call, whose every clause is a
  documented decision with evidence behind it.
- The deferral list to the first security hire is
  longer than most founders realise — formal threat
  modelling, SIEM / SOC, bug-bounty programme,
  dedicated DPO — but the discipline is that the
  founder-scope posture must not **contradict** what
  the first hire will build.
- Legal opinion is delivered by counsel, not by the
  CTO. The CTO's role is to build the defensible
  package counsel turns into contract language and
  regulator correspondence.

The exercise for this chapter —
`exercise-01-founder-scope-security-posture-drill.md` —
walks the four questions for your own current
situation and produces the one-page posture memo.
