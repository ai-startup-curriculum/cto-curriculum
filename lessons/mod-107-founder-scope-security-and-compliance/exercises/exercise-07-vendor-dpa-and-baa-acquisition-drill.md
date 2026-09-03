# Exercise 07 — Vendor DPA and BAA Acquisition Drill

**Module:** `mod-107-founder-scope-security-and-compliance`
**Planned time:** ~2 hours
**Chapter this builds on:** [`08-vendor-dpa-and-baa-acquisition.md`](../08-vendor-dpa-and-baa-acquisition.md),
supported by [`04-gdpr-and-ccpa-baseline.md`](../04-gdpr-and-ccpa-baseline.md)
for the sub-processor-list mechanics that consume
the inventory and by [`05-hipaa-baseline-and-phi-scoping.md`](../05-hipaa-baseline-and-phi-scoping.md)
for the BAA-required vendor list where PHI is in
scope.

## Problem statement

Author the **vendor compliance inventory** for
your startup, run the **DPA / BAA acquisition
process** for the top-10 vendors, and produce the
**customer-facing sub-processor list** that
becomes the SOC 2 CC9.2 evidence and the GDPR
Article 30 processor-record input.

The point of the drill is not to *finish acquisition
for every vendor in the stack* (some sales-assisted
DPAs take 30 days). The point is to (a) build the
inventory as the single source of truth, (b)
kick off the acquisition process for every vendor
that does not already have a DPA / BAA on file,
and (c) produce the customer-facing sub-processor
list that a design partner can be pointed to at a
public URL.

## Requirements

Author the artifacts under `docs/compliance/vendors/`
(or the equivalent in your working repo).

### Artifact 1 — Vendor compliance inventory (`inventory.md` or `inventory.xlsx`)

The load-bearing spreadsheet from chapter 08. One
row per third-party service touching customer data,
personal data, or the production environment.
Columns per chapter 08:

- **Vendor** — company name.
- **Product / SKU** — the specific offering (e.g.,
  AWS Bedrock — us-east-1, OpenAI API Enterprise,
  Vanta — Startup tier).
- **Purpose** — what the vendor does for you.
- **Data categories** — customer content, personal
  data, PHI (if applicable), payment data, logs,
  metadata.
- **Data volume / access scope** — the fraction of
  customer data the vendor sees; whether the
  vendor sees production or only a subset.
- **Region(s)** — where the vendor processes the
  data.
- **DPA status** — Executed / Pending (initiated
  date) / N/A (with the *why*).
- **DPA link** — URL or file reference to the
  executed DPA.
- **BAA status** — Executed / Pending (initiated
  date) / Not required (PHI-adjacent per exercise
  04) / Not available (vendor does not offer BAA).
- **BAA link** — as above.
- **SCC / DPF / transfer mechanism** — the cross-
  border-transfer mechanism if the vendor is in a
  third country (chapter 04).
- **SOC 2 report** — On file / Requested / Not
  available; with the vendor's compliance page
  URL and the last-review date.
- **ISO/IEC 27001 certificate** — On file / N/A;
  URL to the vendor's certificate registration if
  applicable.
- **Public sub-processor list** — link to the
  vendor's own sub-processor list (evidence of
  their own downstream compliance discipline).
- **Last reviewed** — date of last vendor review.
- **Owner** — the internal owner of the
  relationship.

Cover, at a minimum, the vendor categories from
chapter 08's founder-scope stack list: cloud
infrastructure, CDN / edge, foundation-model API,
vector database (if AI-native), observability,
error tracking, analytics, email, support /
helpdesk, auth / identity, payments, compliance
automation, CRM / marketing, team collaboration.

Aim for **20-30 rows** in the inventory (a typical
founder-scope stack has 15-40 vendors touching
some category of data). If a category is not in
use at your stage, mark it Not in Use with a
one-line note rather than deleting the row.

### Artifact 2 — Acquisition tracker for the top-10 vendors (`acquisition-tracker.md`)

Rank the inventory rows by risk-weighted priority
(chapter 08's framing: data-volume × data-category
× regulatory-scope). Take the top 10. For each:

- **Vendor + product.**
- **Acquisition path** — Self-serve / Sales-
  assisted / Custom-redlined (chapter 08).
- **DPA acquisition status** — Not started /
  Initiated (date) / Executed (date) / N/A.
- **BAA acquisition status** — Not required /
  Not started / Initiated (date) / Executed
  (date) / Not available.
- **Zero-retention configuration** — Not
  applicable / Configured (date) / Requested
  (date) / Not configured (with reason).
- **Region / residency configuration** — Not
  applicable / Configured / Requires migration
  (with plan).
- **Blocker** — what would stop the acquisition
  from completing this quarter (sales cycle,
  legal review on our side, compliance-tier
  gate on vendor side, redlining required).
- **Owner and next-action-date.**

For every row currently at *Not started*, actually
kick off the acquisition — send the email, click
the DPA-accept button in the admin console, file
the BAA request. The drill's discipline includes
starting the work, not just planning it.

### Artifact 3 — Customer-facing sub-processor list (`subprocessors.md` or a public URL)

The GDPR Article 28 / CCPA service-provider
requirement — a public list at
`yourcompany.com/subprocessors` (or the trust
center) containing:

- **Vendor name.**
- **Purpose of processing** (one line each).
- **Categories of data processed.**
- **Location of processing** (country or region).
- (Optional but recommended) **Effective date**
  each vendor was added.

Do not include: internal vendor identifiers,
contract dollar amounts, DPA revision numbers,
pricing tier. The list is for customers, not for
internal reference.

Also produce:

- A **version-history section** (either inline or
  in an `archive/` folder) showing prior versions
  of the list with their effective-date ranges.
  The SOC 2 auditor will ask *"who were your sub-
  processors on 2026-06-01?"*; the archived list
  is the answer.
- A **notice-and-objection policy** — the DPA
  clause committing the company to give
  customers X days' notice (15-30 is standard)
  before engaging a new sub-processor, and the
  process for customer objection. Reference the
  DPA template from exercise 03.

If the working repo is not itself the public site,
produce a **draft list ready to publish** in
`docs/compliance/vendors/subprocessors-public.md`,
along with a note on where it will be published.

### Artifact 4 — Foundation-model vendor deep-dive (`fm-vendors.md`)

*Required if the SaaS uses one or more foundation-
model providers.* A detailed sub-section, one per
provider in use (Anthropic, OpenAI, AWS Bedrock,
Azure OpenAI, GCP Vertex, or others):

- **Product tier in use** (e.g., Claude Enterprise
  API vs. self-serve Claude API; ChatGPT Enterprise
  vs. standard API; Bedrock us-east-1 with model X).
- **BAA availability** — verified against the
  vendor's current compliance page (Anthropic
  Trust Center, OpenAI Trust Portal, AWS HIPAA-
  Eligible Services reference, Azure HIPAA
  offering, Google Cloud HIPAA page), with a
  citation URL and a verified-on date.
- **BAA status for our account** — Executed /
  Requested / Not required (PHI-adjacent).
- **Zero-retention** — Configured / Available on
  request / Not available; the endpoint(s)
  affected; the abuse-monitoring tradeoff.
- **Region residency** — the region(s) our calls
  land in and the residency commitment the
  vendor provides.
- **Data-usage-for-training terms** — the vendor's
  commitment on whether our prompts / completions
  are used for training (cite the vendor's
  current data-privacy page).
- **Sub-processors of the sub-processor** — the
  foundation-model vendor's own sub-processors,
  from the vendor's published list.

### Cover memo (`README.md` in `docs/compliance/vendors/`)

A one-page cover memo naming: the inventory row
count, the acquisition tracker's top-10 status
summary, the sub-processor list publication
status, the counsel-review status for any DPA /
BAA that required redlining, and the next-quarter
plan.

## Starter guidance

- **Start from the corporate credit-card
  statement.** The single most reliable way to
  find every third-party service is to scan the
  past 90 days of card charges. Every recurring
  charge is a vendor; every vendor either has a
  DPA-required data-processing relationship or
  it does not. If you cannot recall what the
  charge is for, add it to the inventory anyway
  and investigate — it may be the vendor a
  contractor onboarded without notice.
- **The vendor's compliance page is authoritative.**
  A blog post from 2023 saying *"OpenAI now offers
  BAAs"* is not the same as the current OpenAI
  Trust Portal wording. Every BAA / DPA row must
  cite the vendor's current compliance page URL
  with a verified-on date; re-check quarterly.
- **Self-serve DPAs are 5 minutes of work.** AWS
  Artifact, Cloudflare, GitHub, Stripe, and
  Google Workspace all publish DPAs at stable
  URLs with self-serve acceptance in the admin
  console. If any of these is not Executed in
  the tracker, close it before starting on the
  sales-assisted vendors.
- **Sales-assisted DPAs take 1-3 weeks. Kick
  them off today.** The tracker's action items
  are *email addresses to write today*. If any
  sales-assisted row is *Not started* at the
  end of the drill, the drill is not complete.
- **The BAA question is *only* relevant if the
  scoping call in exercise 04 landed on
  Architecture A or C.** If Architecture B,
  every BAA-status column reads *Not required
  (PHI-adjacent)* and the drill is faster. If A
  or C, the BAA acquisition list from exercise
  04 is directly consumed here.
- **Zero-retention is a two-column question.**
  *"Do we hold a BAA?"* and *"Is zero-retention
  configured?"* are separate questions with
  separate answers. A BAA without zero-
  retention is still a BAA; zero-retention
  without a BAA does not satisfy HIPAA. Track
  both.
- **The sub-processor list is the public-facing
  artifact.** Every enterprise procurement team
  will read it. Every regulator investigation
  will read it. Every design partner will read
  it. It is the single most-consulted piece of
  the vendor library — invest in the quality of
  the phrasing.
- **Version the sub-processor list.** *"The list
  as of 2026-09-15"* is the format. When you
  add a new vendor, archive the prior version;
  do not overwrite. The SOC 2 auditor's *"who
  were your sub-processors on 2026-06-01?"*
  question depends on this.
- **Use a compliance-automation tool if you can.**
  Vanta / Drata / Secureframe / Sprinto /
  Thoropass each have a vendor-management
  module that centralises the inventory, the
  acquisition tracker, and the annual review.
  The manual alternative is where DPAs get
  lost. Cross-reference the tool selection to
  exercise 02.
- **Do not redline DPAs yourself.** If a vendor's
  DPA does not accommodate your role or is
  otherwise inadequate, escalate to counsel.
  The CTO produces the inventory and the
  acquisition-status; counsel produces the
  redlines.

## Acceptance criteria

Your drill output is complete when:

- The vendor compliance inventory covers every
  third-party service touching customer data,
  personal data, or production — a minimum of
  20 rows, with every column populated per row
  (or a one-line justification for empty cells).
- The top-10 acquisition tracker names the
  acquisition path, current DPA / BAA / zero-
  retention / region status, blocker, and next
  action per row. Every self-serve row is
  Executed; every sales-assisted row is at
  least Initiated (with an email or admin-
  console action taken this week).
- The customer-facing sub-processor list exists
  as a draft ready to publish (or as an
  already-published URL) with vendor name,
  purpose, data categories, and location per
  row; the notice-and-objection policy is
  written; the versioning mechanism is in
  place.
- If foundation-model vendors are in use, the
  deep-dive covers each provider with product
  tier, BAA status, zero-retention status,
  residency, data-usage-for-training terms,
  and the vendor's own sub-processors.
- The cover memo names the inventory count,
  the tracker status summary, the sub-
  processor list publication status, and the
  counsel-review status for any redlining
  required.
- Every citation to a vendor's compliance
  posture points to the vendor's current
  compliance page with a verified-on date; no
  citation is more than 90 days stale.
- A first security hire, an enterprise
  procurement reviewer, or a SOC 2 auditor can
  read the vendor library in 20 minutes and
  answer *"who processes our customer data, on
  what terms, and with what current
  compliance evidence?"*.

## What this feeds into

- **Exercise 01 (posture memo) — Section 3**
  takes the *"DPAs and where applicable BAAs
  signed with every sub-processor including
  [foundation-model vendor], a published sub-
  processor list at [URL]"* clause from this
  inventory.
- **Exercise 02 (SOC 2 readiness) — CC9.2**
  (vendor management) — the inventory is the
  primary evidence artifact.
- **Exercise 03 (GDPR / CCPA baseline)** —
  Artifact 1's sub-processor rows populate the
  Article 30 processor-side records and the
  public sub-processor list.
- **Exercise 04 (HIPAA BAA drill)** — the BAA
  acquisition list from exercise 04 is
  directly consumed as the BAA column of this
  inventory; keep them in sync.
- **The module lab** consolidates the vendor
  library with the other exercise outputs
  into a single `docs/compliance/` sub-tree.
- **Capstone
  [`project-102`](../../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package)** —
  the vendor library and the public sub-
  processor list are one of the polished
  deliverables of the project.

The drill's discipline is *making the vendor
library the single source of truth*. A vendor
inventory that lives in one file and is
re-consulted every time a procurement team asks
*"who is in your sub-processor chain?"* is worth
a founder-scope quarter; a vendor library that is
reconstructed each time from credit-card
statements is the pathology chapter 08 warns
against.
