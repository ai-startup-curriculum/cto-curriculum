# HIPAA at Founder Scale — Safeguards, Audit Controls, and Which BAAs You Can Actually Get

> "The cheapest HIPAA compliance strategy is *don't
> handle PHI*. Say so out loud, in an architecture
> decision record, before you decide otherwise." — the
> scoping discipline this chapter is written around.

## Motivation

HIPAA — the US Health Insurance Portability and
Accountability Act of 1996 — regulates the handling of
Protected Health Information (PHI) by covered entities
(healthcare providers, health plans, healthcare
clearinghouses) and by their **business associates**
(vendors that handle PHI on the covered entity's
behalf). If your SaaS touches PHI on behalf of a
healthcare customer, you are a business associate; a
Business Associate Agreement (BAA) is a legal
prerequisite to that engagement; and the Security
Rule's technical, administrative, and physical
safeguards apply.

The founder-scope trap is *volunteering* into the
business-associate role. Many SaaS products can serve
healthcare customers without ever touching PHI — the
customer keeps PHI in a separate system, and the SaaS
sees only non-PHI metadata. Some SaaS products cannot
avoid PHI. The distinction between *PHI-touching* and
*PHI-adjacent* architectures is a load-bearing
architecture decision (chapter 02 of
[`mod-102`](../mod-102-architecture-under-uncertainty/README.md)
covers the ADR discipline this decision is written up
in) with multi-quarter compliance consequences.

This chapter walks the PHI scoping call, the Security
Rule technical safeguards, the audit-control requirement
that always surprises first-time HIPAA teams, and the
current state of BAA availability from the
foundation-model providers a modern AI-native SaaS
depends on.

## What HIPAA actually is

HIPAA is a US federal law with two operative rules for
a SaaS founder:

- **The Privacy Rule** —
  [hhs.gov — Privacy Rule Summary](https://www.hhs.gov/hipaa/for-professionals/privacy/laws-regulations/index.html) —
  governs *use and disclosure* of PHI. Applies to
  covered entities; extends to business associates via
  BAA.
- **The Security Rule** —
  [hhs.gov — Security Rule](https://www.hhs.gov/hipaa/for-professionals/security/index.html) —
  governs the *administrative, physical, and technical
  safeguards* around electronic PHI (ePHI). Applies
  to covered entities and business associates directly.

The Breach Notification Rule
([hhs.gov — Breach Notification](https://www.hhs.gov/hipaa/for-professionals/breach-notification/index.html))
adds a mandatory breach-reporting mechanism (60-day
clock for notifying HHS OCR and affected individuals
for breaches affecting 500+ individuals; annual
aggregate report for smaller breaches).

HHS has proposed a Security Rule modernisation
(Notice of Proposed Rulemaking published December 2024
— see
[hhs.gov — HHS Announces NPRM on the HIPAA Security Rule to Strengthen Cybersecurity for Electronic Protected Health Information](https://www.hhs.gov/about/news/2024/12/27/hhs-announces-nprm-hipaa-security-rule-strengthen-cybersecurity-electronic-protected-health-information.html))
that would tighten several currently-addressable
safeguards into required ones. Watch that rulemaking as
part of the annual policy review.

The load-bearing consequence: the Security Rule
requires that every business associate implement the
technical safeguards, regardless of size. There is no
"small business associate" exemption.

## The scoping call — PHI-touching vs. PHI-adjacent

The single most valuable HIPAA decision at founder
scope is the *scope-of-PHI* decision. Three
architectures:

### Architecture A — PHI-touching

The SaaS stores, processes, transmits, or displays PHI
on behalf of a covered entity. Examples: an EHR-
adjacent workflow tool that displays patient records;
a patient-messaging platform where message bodies
contain clinical detail; a clinical-notes AI assistant
that summarises visit transcripts; a medical-imaging
review tool.

- BAA is required with the covered-entity customer.
- BAA is required with every downstream sub-processor
  that touches PHI (cloud provider, foundation-model
  vendor, observability vendor if logs contain PHI,
  email vendor if emails contain PHI).
- The Security Rule technical safeguards apply
  directly.
- The Breach Notification Rule applies directly.

### Architecture B — PHI-adjacent

The SaaS serves healthcare customers but is
architected so PHI never enters the SaaS. Examples:
practice-management billing systems where the
customer keeps PHI in a separate EHR and the SaaS
only handles CPT codes / claim IDs / non-PHI billing
metadata; scheduling tools where appointments carry
only the patient's initials or a customer-generated
opaque identifier; workforce-management tools for
clinician scheduling.

- BAA is *not required* if the architecture holds up.
- The Security Rule technical safeguards do not
  apply as a HIPAA obligation (they may still apply
  as an ISMS obligation).
- Careful: any *inadvertent* PHI intake (a customer
  pastes a patient chart into a support ticket, a
  free-text field starts collecting clinical detail)
  moves the SaaS to Architecture A. The founder-scope
  discipline is to build *input controls* — form
  validation, DLP on inbound support, customer-facing
  reminders — that prevent inadvertent intake.

### Architecture C — PHI-limited enclave

The main SaaS is PHI-adjacent; a specific enclave
(a specific feature, a specific tenant tier, a
specific data path) is PHI-touching. The BAA and the
technical safeguards apply only to the enclave.

- BAA is required only for the enclave.
- Sub-processor BAAs are required only for
  sub-processors that touch the enclave.
- The Security Rule technical safeguards apply to the
  enclave; the main SaaS retains the lighter
  posture.
- The architectural discipline: the enclave must be
  *demonstrably separable* — a distinct VPC, a
  distinct account, a distinct data store, distinct
  access controls. If a reviewer cannot draw the
  boundary in a data-flow diagram, the enclave
  strategy is not defensible and the whole SaaS is
  in scope.

The founder-scope discipline: pick the architecture
*deliberately*, write it up as an ADR, and revisit the
choice on every new feature. The default under
uncertainty is Architecture B or C — Architecture A
without a specific product-market-fit reason is
paying a large compliance cost for no marginal
customer value.

## The Security Rule technical safeguards

The Security Rule at 45 CFR § 164.312 defines four
technical safeguards. Founder-scope translation:

- **§ 164.312(a) — Access control.** Unique user
  identification (required); emergency access
  procedure (required); automatic logoff
  (addressable); encryption and decryption
  (addressable). At founder scope: SSO with unique
  identities, MFA for administrative access, break-
  glass procedure documented, session-timeout on
  workforce access.
- **§ 164.312(b) — Audit controls.** Hardware,
  software, and procedural mechanisms that record and
  examine activity in information systems that
  contain or use ePHI (required). This is the
  requirement that always surprises first-time HIPAA
  teams. It requires that you be able to reconstruct
  *who accessed what PHI when* — not sampled, not
  logged for a week, but *durably* for the period
  the customer contract requires (usually 6 years by
  HIPAA standard). Application-layer access logs,
  cloud audit logs (CloudTrail / Cloud Audit Logs /
  Azure Monitor), and database-layer audit logs must
  cover the PHI-touching paths.
- **§ 164.312(c) — Integrity.** Mechanisms to
  authenticate ePHI (addressable). At founder scope:
  cryptographic hashes on stored records where
  integrity is critical; checksums on data-in-transit;
  transaction-log-based audit trails.
- **§ 164.312(d) — Person or entity authentication.**
  Verify that the person or entity seeking access is
  who they claim to be (required). Overlaps with
  access control.
- **§ 164.312(e) — Transmission security.** Guard
  against unauthorised access to ePHI transmitted
  over a network (required); integrity controls
  (addressable); encryption (addressable). At
  founder scope: TLS 1.2+ (1.3 preferred) on every
  network path carrying PHI; encryption of PHI in
  backups and in message queues.

"Addressable" in the Security Rule vocabulary does
*not* mean "optional". It means the entity must
either implement the safeguard or document why it is
not reasonable and appropriate and implement an
equivalent alternative. The founder-scope discipline:
implement all addressable safeguards unless there is
a documented equivalent alternative — the
"documented equivalent" path invites scrutiny that
the "just implement it" path avoids.

Administrative safeguards (§ 164.308) and physical
safeguards (§ 164.310) apply in parallel; most of
their content is already in the SOC 2 / ISO/IEC 27001
ISMS (policies, risk analysis, workforce security,
contingency planning, physical inheritance from the
cloud provider). The founder-scope ISMS from chapter
02 covers the majority of these when extended with
HIPAA-specific language.

## The audit-control requirement in more detail

The audit-control requirement is worth its own
subsection because it drives architectural decisions
in a way the other safeguards do not:

- Every PHI access — read, write, print, export, API
  fetch — must produce an audit-log entry.
- Entries must include: user identity, action,
  timestamp, PHI resource identifier, source system.
- Entries must be *tamper-evident* (append-only, or
  cryptographically hashed / signed).
- Entries must be *retained* for the contract-
  specified period (usually 6 years).
- Entries must be *queryable* — an auditor or a
  breach-investigation team must be able to answer
  *"who accessed this patient's record between date
  X and date Y?"*.

The founder-scope architectural implication: the
PHI-touching data plane must have an audit-logging
sidecar (or an application-layer decorator) that
produces one log line per PHI access. The
observability path for these logs must terminate in a
storage tier with tamper-evidence and long retention
(WORM S3, Cloud Storage with retention policy,
Azure Immutable Blob Storage). "We use CloudTrail"
is not sufficient because CloudTrail logs *control-
plane* activity, not application-layer PHI access.

## BAAs with foundation-model providers

The single most-asked-about HIPAA question in AI-
native SaaS: *"which foundation-model vendors will
sign a BAA with us?"*. The current state, verified as
of 2026-08-20 against each vendor's public compliance
pages:

### Anthropic

- **Anthropic Claude Enterprise / Team / Enterprise
  API** offers HIPAA support with a BAA — see
  [anthropic.com — Privacy and legal — HIPAA](https://www.anthropic.com/legal)
  and the Trust Center at
  [trust.anthropic.com](https://trust.anthropic.com/).
  BAA availability is via the sales-assisted path;
  self-serve Claude API and consumer Claude.ai do
  not carry BAA.
- Zero-retention is available on request via
  Anthropic Enterprise API; Claude Enterprise
  deployments generally have zero-day retention
  configurable in the admin console.

<!-- needs-research: confirm the current wording of Anthropic's BAA availability, self-serve vs. sales-assisted gating, and the zero-retention default as of the reader's audit date. -->

### OpenAI

- **OpenAI API BAA path** is available for eligible
  customers via a sales-assisted process — see
  [openai.com/enterprise-privacy](https://openai.com/enterprise-privacy)
  and the Trust Portal at
  [trust.openai.com](https://trust.openai.com/).
  ChatGPT Enterprise and API access under the BAA
  path support HIPAA-compliant use.
- Zero-retention is available on approved API endpoints
  for eligible enterprise customers; consumer ChatGPT
  and default API retention do not qualify.

<!-- needs-research: confirm OpenAI's current BAA-availability process, endpoint eligibility, and zero-retention gating as of the reader's audit date. -->

### AWS Bedrock

- **AWS Bedrock** is in scope for the AWS HIPAA
  Eligible Services list — see
  [aws.amazon.com/compliance/hipaa-eligible-services-reference](https://aws.amazon.com/compliance/hipaa-eligible-services-reference/)
  and the AWS HIPAA overview at
  [aws.amazon.com/compliance/hipaa-compliance](https://aws.amazon.com/compliance/hipaa-compliance/).
  Customers with the AWS BAA can use Bedrock for
  PHI workloads, subject to the specific model /
  region combinations documented on the Bedrock
  service page.
- AWS BAA is self-serve via AWS Artifact for
  customers with an eligible support plan.

### Azure OpenAI

- **Azure OpenAI Service** is covered under
  Microsoft's HIPAA BAA — see
  [learn.microsoft.com — Azure compliance offerings — HIPAA / HITECH](https://learn.microsoft.com/en-us/azure/compliance/offerings/offering-hipaa-hitech)
  and the Microsoft Trust Center at
  [microsoft.com — Trust Center — HIPAA](https://www.microsoft.com/en-us/trust-center/compliance/hipaa).
  The Microsoft BAA is offered by default to Azure
  enterprise customers via the Online Services Terms.

### Google Cloud Vertex AI

- **Google Cloud Vertex AI** is in scope for
  Google Cloud's HIPAA BAA — see
  [cloud.google.com/security/compliance/hipaa](https://cloud.google.com/security/compliance/hipaa)
  and the HIPAA implementation guide at
  [cloud.google.com — HIPAA on Google Cloud](https://cloud.google.com/architecture/hipaa-compliance-on-gcp).
  The Google BAA is available via the Cloud Console
  BAA workflow for eligible customers.

### The wider vendor stack

The BAA requirement extends to every sub-processor
that touches PHI, not just the foundation-model
vendor. Common founder-scope stack items and their
BAA availability:

- **Cloud provider** (AWS, GCP, Azure) — BAA is
  standard. Self-serve on AWS Artifact; console
  workflow on GCP; Online Services Terms on Azure.
- **Observability** (Datadog, New Relic, Honeycomb,
  Splunk) — most enterprise-tier observability
  vendors offer BAA. Verify per vendor.
- **Email** (SendGrid / Twilio, Mailgun, Postmark,
  Amazon SES) — some offer BAA on specific tiers.
  Twilio SendGrid offers BAA on the Pro plan and
  above; SES BAA falls under the AWS BAA.
- **Support / helpdesk** (Zendesk, Intercom,
  HubSpot) — some tiers include HIPAA add-ons.
- **Analytics** (Segment, Amplitude, Mixpanel) —
  historically BAA-limited; verify per current
  offering.
- **Payment processing** (Stripe) — Stripe Radar and
  the core payments API generally do not receive
  PHI; if the payment description leaks PHI, the
  posture is broken independent of BAA.

Any sub-processor that touches PHI without a BAA is a
Security Rule violation. If a required sub-processor
does not offer a BAA, either (a) architect the PHI
out of their scope (Architecture B / C above), or
(b) replace the sub-processor with one that does.

<!-- needs-research: the vendor list above should be re-verified against each vendor's current compliance page before a founder-scope reader commits to any specific product. -->

## The "don't handle PHI" architecture as a legitimate option

The most under-considered HIPAA strategy at founder
scope is: **do not handle PHI**. Many founders in
health-adjacent verticals discover on inspection that
their product does not actually need PHI to deliver
its core value. The rewrite from Architecture A to
Architecture B, done early, is often a two-to-four-
week engineering task; done late (after production
deployment, after enterprise contracts, after audit
findings), it is a multi-quarter programme.

The founder-scope pattern:

- **List every PHI element the product currently
  handles.** Name, date of birth, medical record
  number, diagnosis, procedure code, clinical note,
  imaging file. If the list is empty, congratulations —
  you are Architecture B.
- **For each element, ask: is this the customer's
  identifier for the patient, or is it PHI?** A
  customer-generated opaque identifier (`patient-1234`)
  is not PHI. A medical record number, in most
  contexts, is.
- **For each PHI element, ask: does the SaaS need to
  see the *plaintext*?** If not, the customer can
  hash it before upload, encrypt it under a
  customer-held key, or tokenise it. Any of those
  removes the element from PHI scope from the SaaS
  perspective (the customer retains the mapping;
  the SaaS never sees the underlying PHI).
- **For each remaining PHI element, ask: does the
  feature that requires it justify the compliance
  cost?** If not, cut the feature.

An honest re-scope from Architecture A to
Architecture B is often the highest-ROI compliance
work a founder-scope startup does.

## The boundary to counsel

HIPAA is a heavily-litigated area. Counsel-scope
activities:

- Determining whether your product renders you a
  business associate at all.
- Reviewing and redlining the customer-facing BAA and
  every vendor-facing BAA.
- Determining whether a specific data element is
  PHI in your specific context.
- Handling a breach-notification decision under 45
  CFR § 164.400–414 — the 60-day HHS OCR
  notification, the individual-notification
  requirement, the media-notification threshold at
  500+ affected individuals.
- Advising on state-law overlays (California CMIA,
  New York SHIELD, and successors).
- Responding to an HHS OCR audit or inquiry.

The CTO produces the technical safeguards, the audit-
control implementation, the sub-processor list with
BAA evidence, and the data-flow diagram. Counsel
turns the package into the BAA redlines and the
breach-response mechanics.

## Summary

- HIPAA applies to business associates that handle
  PHI on behalf of covered entities. There is no
  "small business associate" exemption.
- The scoping call — **PHI-touching vs. PHI-adjacent
  vs. PHI-limited enclave** — is a load-bearing
  architecture decision with multi-quarter compliance
  consequences. Default under uncertainty is
  PHI-adjacent.
- Security Rule technical safeguards at 45 CFR §
  164.312 — access control, audit controls,
  integrity, authentication, transmission security.
  "Addressable" does not mean "optional".
- The audit-control requirement drives architecture:
  every PHI access produces a tamper-evident audit-
  log entry, retained for the contract period,
  queryable by identity / resource / time.
- BAA availability from foundation-model vendors:
  Anthropic (Claude Enterprise / Enterprise API,
  sales-assisted), OpenAI (API BAA path, sales-
  assisted), AWS Bedrock (via AWS Artifact), Azure
  OpenAI (via Microsoft OST), GCP Vertex (via GCP
  BAA workflow). Verify current status against each
  vendor's compliance page.
- The BAA requirement extends to *every* sub-
  processor touching PHI. Any sub-processor without a
  BAA is a violation; either architect the PHI out
  of their scope, or replace them.
- The most under-considered strategy is *don't
  handle PHI*. An early re-scope from Architecture A
  to Architecture B is often the highest-ROI
  compliance work a founder-scope startup does.
- Legal opinion, BAA redlining, breach-notification
  decisions, and OCR correspondence are counsel-
  scope. The CTO produces the technical package.

The exercise for this chapter —
`exercise-04-hipaa-baa-and-technical-safeguards-drill.md` —
walks the scoping call, the safeguards map, and the
BAA acquisition list for your own startup.
