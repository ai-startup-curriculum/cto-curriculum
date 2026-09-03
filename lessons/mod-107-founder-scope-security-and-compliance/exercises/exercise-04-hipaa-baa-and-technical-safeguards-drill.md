# Exercise 04 — HIPAA BAA and Technical Safeguards Drill

**Module:** `mod-107-founder-scope-security-and-compliance`
**Planned time:** ~2 hours
**Chapter this builds on:** [`05-hipaa-baseline-and-phi-scoping.md`](../05-hipaa-baseline-and-phi-scoping.md),
supported by [`08-vendor-dpa-and-baa-acquisition.md`](../08-vendor-dpa-and-baa-acquisition.md)
for the BAA acquisition mechanics and by
[`mod-102` chapter 02](../../mod-102-architecture-under-uncertainty/README.md)
for the ADR format the PHI-scoping decision lands in.

## Problem statement

Decide — deliberately, on paper — whether your startup
is **PHI-touching**, **PHI-adjacent**, or a
**PHI-limited enclave** under the Architecture A / B / C
split in chapter 05. Then, for whichever architecture
you land on, ship the artifacts that make the decision
defensible to a healthcare-customer procurement team,
to a Security Rule auditor, and (if PHI-touching) to
HHS OCR in a hypothetical breach investigation.

The drill has two paths depending on the scoping call:

- **If PHI-adjacent (Architecture B).** Ship the
  *scoping ADR* that names how PHI is kept out, the
  *input controls* that prevent inadvertent intake,
  and the *"we do not sign BAAs"* stance for the
  vendor list. This is the shorter path and is the
  right default under uncertainty.
- **If PHI-touching or PHI-limited enclave
  (Architecture A / C).** Ship the *scoping ADR*, the
  *Security Rule technical-safeguards map*, the
  *audit-control implementation plan*, and the *BAA
  acquisition list* covering every downstream vendor
  that will see PHI.

The point of the drill is not to *become HIPAA
compliant* (that is a multi-quarter programme with
counsel-driven contract work). The point is to
produce the founder-scope package a counsel, an
auditor, and a first security hire can extend without
rewriting.

## Requirements

Author the artifacts under
`docs/compliance/hipaa/` (or the equivalent in
your working repo).

### Artifact 1 — PHI-scoping ADR (`phi-scoping-adr.md`)

An ADR in the Nygard format (chapter 02 of
[`mod-102`](../../mod-102-architecture-under-uncertainty/README.md)):

- **Context** — the healthcare-customer profile
  (existing customers or target customers), the
  product surface area, the data elements the SaaS
  currently ingests or plans to ingest, the specific
  regulatory pressure driving the decision.
- **Decision** — one of Architecture A (PHI-touching),
  B (PHI-adjacent), or C (PHI-limited enclave). If C,
  name the enclave (feature, tenant tier, or data
  path) and the mechanism that keeps it demonstrably
  separable from the main SaaS.
- **Consequences** — the compliance obligations the
  decision creates (BAAs, safeguards, breach
  notification), the customer eligibility it buys
  (which healthcare customer segments become
  reachable), and the engineering cost.
- **Alternatives considered** — the other two
  architectures, each with a one-line rejection
  reason. If the *"don't handle PHI"* option was
  ruled out, name the specific feature or revenue
  reason that required PHI in the flow.
- **Reversibility** — how expensive the decision
  would be to change (engineer-quarters and
  compliance-days) at 5, 50, and 500 healthcare
  customers.

### Artifact 2 — Data-element inventory (`phi-element-inventory.md`)

A table with one row per data element the SaaS
currently handles (or plans to handle in the
committed roadmap). Columns:

- **Element** — the field name (e.g., `patient_name`,
  `dob`, `medical_record_number`, `visit_note_text`,
  `imaging_file`, `cpt_code`, `insurance_member_id`).
- **Source** — where it enters the system (API,
  form field, uploaded file, third-party sync,
  customer-provided identifier).
- **PHI classification** — Yes / No / Depends-on-
  context. Cite the HIPAA definition at 45 CFR §
  160.103 and the 18 HIPAA identifiers at
  [hhs.gov — De-identification](https://www.hhs.gov/hipaa/for-professionals/privacy/special-topics/de-identification/index.html).
- **Justification** — one sentence per row on why
  the element is / is not PHI in your specific
  context (a `patient-1234` opaque customer identifier
  is not PHI; a medical record number usually is).
- **Handling** — plaintext / hashed / encrypted-
  client-side / tokenised / not stored.
- **Reachable systems** — which downstream systems
  the element flows into (primary DB, analytics
  warehouse, logs, backups, LLM API, email vendor,
  support tool).

The inventory is the direct input to the safeguards
map (Artifact 3) and the BAA list (Artifact 4).

### Artifact 3 — Security Rule technical-safeguards map (`technical-safeguards-map.md`)

*Required only if Architecture A or C.* A table with
one row per Security Rule technical safeguard from
45 CFR § 164.312. Columns:

- **Safeguard citation** (e.g., `§ 164.312(a)(1) —
  Access control — Unique user identification —
  Required`).
- **Required or addressable** — verbatim from the
  regulation.
- **Implementation** — the specific technical
  control that satisfies it (SSO with per-user
  identities via [vendor], MFA on admin routes via
  [vendor], TLS 1.2+ on every PHI-touching endpoint,
  etc.).
- **Evidence** — the artifact that proves it (config
  file, IaC module, audit-log query, screenshot,
  vendor certificate).
- **Owner** — the engineer (or the CTO) accountable
  for the control.
- **Status** — Implemented / Partial / Gap.
- **Gap-close plan** — for Partial / Gap rows,
  the plan and target date.

Cover all five clauses (a) access control, (b) audit
controls, (c) integrity, (d) authentication, (e)
transmission security. For any *addressable*
safeguard not implemented, provide the *documented
equivalent alternative* (chapter 05); do not simply
mark it N/A.

### Artifact 4 — Audit-control implementation plan (`audit-controls.md`)

*Required only if Architecture A or C.* A short
design document (1-3 pages) covering:

- **PHI access paths** — enumerate every path in the
  application where PHI is read, written, printed,
  exported, or fetched (list the specific API
  routes, background jobs, admin queries, and
  export mechanisms).
- **Audit-log schema** — the fields captured per
  entry (user identity, action, timestamp, PHI
  resource identifier, source system, request
  correlation ID).
- **Tamper evidence** — the mechanism that makes
  the log append-only or cryptographically
  verifiable (WORM S3 with Object Lock, GCS with
  retention policy, Azure Immutable Blob Storage,
  or an equivalent).
- **Retention** — the retention period (default 6
  years per HIPAA guidance; verify against your
  customer contract) and the storage tier that
  supports it economically.
- **Query interface** — how a breach-investigation
  team answers *"who accessed patient X's records
  between date A and date B?"* — SQL query, log
  aggregator saved search, or purpose-built
  console. Include the runbook step-by-step.
- **Gap register** — the routes / systems that do
  not yet emit audit logs, with owner and target
  close date.

### Artifact 5 — BAA acquisition list (`baa-list.md`)

*Required only if Architecture A or C.* A table with
one row per downstream vendor that will see PHI —
cross-referenced from Artifact 2's *Reachable
systems* column and from the vendor compliance
inventory in exercise 07. Columns:

- **Vendor** and **product / SKU** (e.g., AWS
  Bedrock — us-east-1 — Claude 3 Sonnet).
- **PHI scope with this vendor** — what elements
  the vendor will see and in what volume.
- **BAA availability** — Available (self-serve) /
  Available (sales-assisted) / Not available.
  Cite the vendor's compliance page.
- **BAA status** — Executed / Requested (date) /
  Blocked (reason).
- **Alternative if BAA not available** — the
  architectural change or the substitute vendor.
- **Region / residency** — where the vendor
  processes the data.
- **Zero-retention configuration** — whether
  configured, which endpoint, verified by whom on
  what date.
- **Owner** — internal owner of the vendor
  relationship.

Cover, at a minimum: cloud provider, foundation-
model provider, observability, email, support tool,
error tracking, and any other vendor whose row in
Artifact 2 shows PHI in scope.

### Artifact 6 — Input controls memo (`input-controls.md`)

*Required for Architecture B and recommended for
A / C.* A short memo (1 page) covering the input
controls that prevent inadvertent PHI intake:

- **Form-field validation** — patterns / lengths /
  types that reject obvious PHI in fields not
  intended to carry it.
- **Support / helpdesk DLP** — the mechanism (or
  the acknowledgement that there is none) that
  detects PHI in inbound support tickets.
- **Customer-facing reminders** — the wording in
  the customer contract, the product UI, and the
  API documentation that reminds customers not
  to submit PHI where the SaaS does not accept
  it.
- **Detection** — the mechanism (or the
  acknowledgement that there is none) that
  detects inadvertent PHI-in-logs, PHI-in-
  analytics, or PHI-in-error-reports.
- **Response** — what happens on discovery of
  inadvertent PHI — the redaction runbook, the
  customer notification path, the retro process.

### Cover memo (`README.md` in `docs/compliance/hipaa/`)

A one-page cover memo naming: the architecture the
scoping ADR landed on, the artifacts produced, the
counsel-review status of the BAA list, and the
specific customer commitment (real or hypothetical)
that gates any remaining gap-close work.

## Starter guidance

- **Do the scoping call before anything else.**
  Every other artifact depends on Architecture
  A / B / C. Do not draft the safeguards map
  before the ADR is written; you may waste half a
  day on scope that changes.
- **The default under uncertainty is B.** If you
  cannot name a specific product-market-fit reason
  that the SaaS must handle PHI to deliver its
  core value, the architecture is B and the
  scoping ADR should say so explicitly. This is
  the highest-ROI outcome of the drill for most
  founder-scope startups.
- **Read the 18 HIPAA identifiers at
  [hhs.gov — De-identification methods](https://www.hhs.gov/hipaa/for-professionals/privacy/special-topics/de-identification/index.html)
  before writing the element inventory.** The
  Safe Harbor list is the reference for whether an
  identifier makes a record PHI.
- **The "PHI-limited enclave" (Architecture C) is
  only defensible if the boundary is drawable.** If
  a reviewer cannot see, from the data-flow
  diagram, exactly which VPC / account / data
  store / access-control boundary separates the
  enclave from the main SaaS, the strategy is not
  defensible and the whole SaaS is in scope.
- **"Addressable" does not mean "optional".** The
  chapter's warning bears repeating in the drill.
  Any addressable safeguard the safeguards map
  marks as not-implemented needs a documented
  equivalent alternative, not a blank cell.
- **The audit-control requirement drives the
  architecture, not the other way round.** If
  your current stack does not have an application-
  layer audit-log path for PHI access, that gap
  goes at the top of Artifact 4's gap register —
  it is usually a multi-sprint engineering
  investment, not a config change.
- **BAA availability changes.** Every entry in
  the BAA list must cite the vendor's own current
  compliance page (Anthropic Trust Center, OpenAI
  Trust Portal, AWS HIPAA-Eligible Services list,
  Azure HIPAA compliance offering, Google Cloud
  HIPAA page). Do not rely on the chapter's
  vendor-state snapshot without re-verifying.
- **Zero-retention is not BAA.** Two separate
  vendor configurations. A BAA without zero-
  retention is still a BAA; zero-retention
  without a BAA does not satisfy HIPAA. The BAA
  list must track both columns.
- **If BAA is not available for a required
  vendor, decide *now*.** The escape hatch —
  architect the PHI out of the vendor's scope,
  or replace the vendor — is much cheaper before
  production integration than after.
- **The scoping ADR is the counsel hand-off.**
  Counsel will ask *"which customers are PHI-
  covered entities?"*, *"what elements does the
  SaaS see?"*, and *"what BAA coverage do you
  have?"*. The ADR + element inventory + BAA
  list answer those three questions directly.

## Acceptance criteria

Your drill output is complete when:

- The scoping ADR exists at
  `docs/compliance/hipaa/phi-scoping-adr.md` and
  names Architecture A, B, or C with the required
  context, decision, consequences, alternatives,
  and reversibility sections.
- The data-element inventory (Artifact 2) covers
  every data element the SaaS currently ingests
  and every element on the committed roadmap; PHI
  classification is Yes / No / Depends-on-context
  with a one-sentence justification per row.
- If Architecture A or C: the technical-safeguards
  map covers all five clauses of 45 CFR § 164.312;
  every safeguard row has implementation, evidence,
  owner, status, and (for gaps) a close plan;
  every addressable safeguard is either
  implemented or has a documented equivalent
  alternative.
- If Architecture A or C: the audit-control
  implementation plan enumerates every PHI access
  path in the application, defines the audit-log
  schema, names the tamper-evidence mechanism,
  states the retention period, and provides the
  runbook for the *"who accessed patient X?"*
  query.
- If Architecture A or C: the BAA acquisition
  list covers every downstream vendor that will
  see PHI, cites each vendor's compliance page,
  and states BAA / zero-retention / region /
  status per row.
- If Architecture B: the input-controls memo
  names the mechanisms that prevent inadvertent
  PHI intake and the mechanisms that detect it
  when the prevention fails.
- The cover memo names the architecture, the
  produced artifacts, and the counsel-review
  status.
- A technical reviewer who does not know your
  startup can read the package in 20 minutes and
  answer *"is this startup a HIPAA business
  associate, what PHI does it see, and what
  BAAs does it hold?"*.

## What this feeds into

- **Exercise 01 (posture memo) — Section 1** takes
  the Architecture A / B / C decision as the
  *"regulated data"* line.
- **Exercise 02 (SOC 2 readiness)** — the audit-
  control implementation is CC7 (system
  operations) evidence; the BAA list feeds CC9.2
  (vendor management) evidence.
- **Exercise 03 (GDPR / CCPA baseline)** — the
  data-element inventory is a direct input to the
  RoPA and the sub-processor list.
- **Exercise 07 (vendor DPA / BAA acquisition)** —
  the BAA acquisition list is the cross-referenced
  starting point for the wider vendor artifact
  library.
- **The module lab** consolidates the HIPAA
  artifacts with the other exercise outputs into
  a single `docs/compliance/` sub-tree.
- **Capstone
  [`project-102`](../../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package)** —
  the HIPAA scope call and (if applicable) the
  safeguards + BAA package are one of the
  deliverables.

The drill's discipline is *making the scoping call
deliberately*. A founder-scope startup that
consciously chose Architecture B and can defend the
choice is much better positioned than one that
drifted into Architecture A without ever writing
down the decision.
