# Exercise 03 — GDPR and CCPA SaaS Baseline Drill

**Module:** `mod-107-founder-scope-security-and-compliance`
**Planned time:** ~3 hours
**Chapter this builds on:** [`04-gdpr-and-ccpa-baseline.md`](../04-gdpr-and-ccpa-baseline.md),
supported by [`08-vendor-dpa-and-baa-acquisition.md`](../08-vendor-dpa-and-baa-acquisition.md)
for the sub-processor list mechanics.

## Problem statement

Ship the **GDPR / CCPA baseline** for your startup's
SaaS data flow — the six artifacts that together
answer the *"describe your privacy programme"*
question from any enterprise procurement
questionnaire and give counsel the defensible package
to turn into privacy-notice copy, contract language,
and regulator responses.

The six artifacts:

1. **Records of Processing Activities (RoPA v0)** —
   controller sheet, processor sheet, sub-processor
   inventory.
2. **Data-subject-request (DSR) handling process**
   documented as a runbook, with the statutory clock
   as the SLA.
3. **Data Processing Agreement (DPA) template** you
   send to customers, plus the vendor DPA
   acquisition list.
4. **Data-residency decision** (US-only with DPF /
   SCC, dual-region, EU-sovereign — chapter 04).
5. **Cookie-consent posture** — the mechanism, the
   cookie-inventory table, the *"Do Not Sell or
   Share"* mechanism for CCPA.
6. **Customer-facing privacy notice** — short-form
   and long-form drafts.

The point of the drill is not to *ship every artifact
to production* (some — the privacy notice, the DPA —
require counsel review before publication). The
point is to produce a defensible **v0** of each
artifact that counsel can turn into the published
version.

## Requirements

Author the six artifacts under
`docs/compliance/privacy/` (or the equivalent in
your working repo).

### Artifact 1 — RoPA v0 (`ropa.md` or `ropa.xlsx`)

Three sheets / sections:

- **Controller RoPA (Article 30(1))** — one row per
  processing activity where you are the controller.
  Minimum three rows (employees / prospects /
  visitors is the founder-scope starter). Columns
  per chapter 04.
- **Processor RoPA (Article 30(2))** — one row per
  customer (or one row per customer *category* if
  your customer base is homogeneous). Columns per
  chapter 04.
- **Sub-processor inventory** — one row per
  downstream vendor that receives personal data on
  your behalf, cross-referenced from the vendor
  compliance inventory in exercise 07.

Cap the total document at 10 pages.

### Artifact 2 — DSR handling runbook (`dsr-runbook.md`)

A runbook (1-3 pages) covering:

- Intake channels (`privacy@yourcompany.com`, webform
  URL) — published.
- Identity-verification procedure per request type.
- Ticket lifecycle (owner, status, SLA per
  statutory clock — GDPR one month; CCPA 45 days).
- Fulfilment mechanisms — the *specific tools /
  scripts* used to satisfy each right (access,
  deletion, portability, correction, opt-out of
  sale / sharing, limit use).
- Backup-exception rule (deletion vs. backup-
  retention interaction).
- DSR log format and retention (SOC 2 evidence).
- Escalation path when a request raises legal
  privilege, right-of-others, or manifestly-
  unfounded questions (route to counsel).

### Artifact 3 — DPA template + vendor DPA acquisition list

Two parts:

- **Customer-facing DPA template**
  (`dpa-template.md`) — a one-to-three-page
  scaffold naming the parties, the roles
  (controller / processor), sub-processor list
  reference, data categories, security measures
  reference, breach-notification clock, DSR
  cooperation obligation, sub-processor engagement
  process (notice window, objection right), transfer
  mechanism (DPF, SCCs), termination and return /
  deletion. **Explicitly flagged as
  counsel-reviewed-before-use**; the template is a
  starter, not a published contract. Cite the IAPP
  DPA resource ([iapp.org — Data Processing
  Agreements](https://iapp.org/resources/topic/data-processing-agreements-dpa/))
  and the EU Commission SCCs page
  ([commission.europa.eu — SCCs](https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/standard-contractual-clauses-scc_en)).
- **Vendor DPA acquisition list** (`vendor-dpas.md`
  — cross-referenced from exercise 07) — for the
  top 10 vendors from the vendor inventory,
  current DPA status (Executed / Pending / N/A)
  and next action if not executed.

### Artifact 4 — Data-residency decision (`data-residency-adr.md`)

A short ADR (chapter 02 of
[`mod-102`](../../mod-102-architecture-under-uncertainty/README.md)):

- **Context** — customer / user distribution across
  jurisdictions; which regulators care (GDPR EU,
  UK GDPR, CCPA California, state privacy laws).
- **Decision** — US-only with DPF / SCC transfer
  mechanism; dual-region (US + EU); EU-sovereign;
  or another defensible posture.
- **Consequences** — what the decision buys
  (customer eligibility, procurement compliance),
  what it costs (engineering complexity, sub-
  processor duplication, ongoing operational
  overhead).
- **Reversibility** — how expensive the decision
  would be to change at 10, 50, and 500 customers.
- **Alternatives considered** — the two other
  postures, each with a one-line rejection reason.

### Artifact 5 — Cookie-consent posture (`cookies.md`)

- **Consent mechanism** — the CMP vendor or the
  self-hosted solution, with the opt-in vs. opt-
  out logic per jurisdiction (opt-in for EU / UK,
  opt-out for CCPA "Sale or Share").
- **Cookie inventory** — a table with columns:
  cookie name, purpose, provider (first-party /
  third-party), category (strictly necessary /
  functional / analytics / marketing), retention.
- **CCPA "Do Not Sell or Share" mechanism** —
  where the link appears; how the request is
  honored; how the Global Privacy Control signal
  is handled.
- **Cookie policy page** — a link (or an
  attachment) to the customer-facing cookie
  policy.

### Artifact 6 — Privacy notice draft (`privacy-notice.md`)

Two versions:

- **Short-form** (under 500 words) — the
  digestible summary linked from the site
  footer / product footer.
- **Long-form** (under 3,000 words) — the full
  notice covering GDPR Articles 13 / 14 and CCPA
  1798.100 / 1798.130 requirements.

Explicitly flagged as **counsel-reviewed-before-
publication**. The CTO drafts the technical-facts
sections (what data is collected, how, from where,
retention, security measures, sub-processor
categories); counsel drafts the legal-basis, rights,
and legal-recourse sections.

### Cover memo (`README.md` in `docs/compliance/privacy/`)

A one-page cover memo naming: the six artifacts,
the counsel-review status of each, and the specific
regulator or customer commitment that gates each
artifact's publication.

## Starter guidance

- **Start with the customer/employee jurisdiction
  map.** Before writing any artifact, produce a
  one-paragraph geographic map — where are our
  users, where are our employees, where are our
  paying customers, where are our target enterprise
  buyers. This decides which laws apply and which
  DPA transfer mechanism you need.
- **The controller / processor split is the most
  common source of RoPA mistakes.** For every row
  in the controller RoPA, the controller is *you*
  and the data subjects are your employees /
  prospects / visitors. For every row in the
  processor RoPA, the controller is your customer
  and the data subjects are their end-users. If
  a row confuses the two, revisit chapter 04.
- **Use the vendor's DPA — do not draft your own
  inbound.** Every self-serve vendor has a
  published DPA; every sales-assisted vendor will
  provide one. Drafting your own inbound DPA is a
  counsel-scope activity and slows procurement.
- **The DSR runbook must include the tools, not
  just the process.** *"Data export is via the
  `scripts/export_user.py` script; run as `python
  scripts/export_user.py --user-id <id>` and the
  output lands at `s3://exports/<request-id>/`"*.
  If the runbook only names the process without
  the tool, the first request will land in the
  gap between them.
- **Do not skip the deletion mechanism.** The most
  common founder-scope DSR failure is
  *"we know how to answer access requests but
  our deletion path only reaches the primary
  database — the analytics warehouse and the
  logs still have the data"*. The runbook must
  enumerate every store the deletion reaches and
  every store it does not (with the exception
  rule).
- **The data-residency decision is a real
  engineering commitment.** Dual-region is not a
  configuration flag; it is a multi-quarter
  architectural investment. Do not commit to
  dual-region in the ADR unless you can name the
  engineering delivery plan.
- **Cookie-consent gaps are what regulators find
  first.** The regulator sees the public site,
  not the ISMS. A misconfigured cookie banner
  (analytics cookies set before opt-in, "reject
  all" absent from the banner) is the easiest
  enforcement target.
- **The privacy notice draft is a *draft*.** The
  drill is not writing the customer-facing
  version; it is producing the technical-facts
  layer counsel converts into the legal-basis
  layer. Flag every legal-basis line as
  *"counsel to complete"*.
- **Cite the primary regulator or DPA source per
  artifact.** RoPA — the ICO template; DSR — the
  ICO / EDPB guidance; DPA — the EU Commission
  SCCs; cookie consent — the EDPB Guidelines on
  Consent; privacy notice — the GDPR text and the
  CCPA text; residency — the DPF page.

## Acceptance criteria

Your drill output is complete when:

- All six artifacts exist under
  `docs/compliance/privacy/`, plus the cover memo.
- The RoPA has at least three controller rows,
  the processor row(s) for your customer(s), and
  the sub-processor inventory cross-referenced
  from exercise 07.
- The DSR runbook names the specific tools,
  scripts, or console operations used to satisfy
  each request type, and covers the backup-
  exception rule.
- The DPA template covers all clauses named in
  the requirements, is flagged as counsel-
  reviewed-before-use, and cites the SCC / IAPP
  sources.
- The vendor DPA acquisition list covers at
  least 10 vendors with current status per row.
- The data-residency ADR includes the
  reversibility unit (engineer-quarters) at 10,
  50, and 500 customers.
- The cookie-consent posture names a specific
  mechanism, includes the cookie inventory
  table, and covers both GDPR opt-in and CCPA
  "Do Not Sell or Share" mechanisms.
- The privacy-notice draft has both short-form
  (< 500 words) and long-form (< 3,000 words)
  versions, is flagged as counsel-reviewed-
  before-publication, and enumerates the
  GDPR / CCPA-required content categories.
- The cover memo names which artifacts require
  counsel review before publication and which are
  ready for immediate use.
- A technical reviewer who does not know your
  startup can read all six artifacts in 30
  minutes and answer *"what personal data do
  they process, from whom, on what legal basis,
  and how do they honour data-subject
  requests?"*.

## What this feeds into

- **Exercise 02 (SOC 2 readiness) — CC9.2 (vendor
  management)** takes the sub-processor inventory
  as evidence.
- **Exercise 07 (vendor DPA / BAA)** is the
  cross-referenced acquisition drill for the
  vendors in Artifact 3.
- **The module lab** consolidates the privacy
  artifacts with the other exercise outputs into
  a single `docs/compliance/` sub-tree.
- **Capstone
  [`project-102`](../../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package)** —
  the GDPR / CCPA baseline is the second
  deliverable of the project.

The drill's discipline is producing a *defensible
package for counsel*, not a production-ready
privacy programme. Any artifact you would be
comfortable publishing without counsel review is
either (a) very well-scoped or (b) not yet
lawful — the honest posture is to flag counsel
review as the gate.
