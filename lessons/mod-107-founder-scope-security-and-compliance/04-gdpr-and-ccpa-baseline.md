# GDPR and CCPA — The SaaS Data-Flow Baseline

> "GDPR and CCPA are not the same law. They rhyme.
> Assuming a control that satisfies one satisfies the
> other is the single most common founder-scope privacy
> mistake." — the vocabulary discipline this chapter is
> written around.

## Motivation

Any SaaS with users, employees, or customer contacts in
the European Union or the United Kingdom is subject to
the General Data Protection Regulation (GDPR). Any SaaS
that meets the applicability thresholds for California's
CCPA / CPRA (revenue, resident-count, or data-sale
thresholds) is subject to that law. Similar state-level
laws in the US — Virginia CDPA, Colorado CPA,
Connecticut CTDPA, Utah UCPA, Texas TDPSA, and a growing
list — apply on similar patterns. A founder-scope SaaS
usually falls under some subset of these on day one and
under all of them by Series-A.

The founder-scope discipline is not to memorise the
statutes. It is to build a **baseline** — a small set of
artifacts and a data-flow diagram — that (a) satisfies
each regime's *documented-programme* requirements, (b)
handles data-subject requests within the statutory
clock, and (c) gives counsel a defensible package to
turn into contract language, privacy-notice copy, and
regulator-facing statements.

This chapter walks the applicability triggers, the
controller / processor / sub-processor vocabulary, the
Article 30 records-of-processing-activities register,
the data-subject-request (DSR) handling process, the
DPA template for downstream vendors, data-residency
choices, cookie consent, and the customer-facing
privacy notice.

## Applicability — when GDPR and CCPA apply

**GDPR** (Regulation (EU) 2016/679) — full text at
[eur-lex.europa.eu/eli/reg/2016/679/oj](https://eur-lex.europa.eu/eli/reg/2016/679/oj):

- Applies to any organisation that processes personal
  data of individuals *in the EU* (Article 3(1)), or
  offers goods / services to individuals in the EU
  (Article 3(2)(a)), or monitors the behaviour of
  individuals in the EU (Article 3(2)(b)) — regardless
  of where the organisation is established.
- **UK GDPR** — see
  [ico.org.uk — Guide to UK GDPR](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/) —
  applies on the same shape for individuals in the UK
  post-Brexit.

**CCPA / CPRA** — the California Consumer Privacy Act
of 2018 as amended by the California Privacy Rights Act
of 2020 — see
[oag.ca.gov/privacy/ccpa](https://oag.ca.gov/privacy/ccpa)
and the California Privacy Protection Agency
regulations at
[cppa.ca.gov](https://cppa.ca.gov/):

- Applies to for-profit businesses that (a) had
  annual gross revenues in excess of $25 million in
  the preceding calendar year, OR (b) alone or in
  combination annually buy, sell, or share the
  personal information of 100,000+ California
  consumers or households, OR (c) derive 50%+ of
  annual revenues from selling or sharing consumers'
  personal information.

Other US state privacy laws — Virginia CDPA, Colorado
CPA, Connecticut CTDPA, Utah UCPA, Texas TDPSA, and
successors — apply on similar patterns; each has
distinct thresholds, DSR mechanics, and definitions.
The IAPP maintains a comparison at
[iapp.org — US State Privacy Legislation Tracker](https://iapp.org/resources/article/us-state-privacy-legislation-tracker/).

The founder-scope disciplining question: *"which
customers, users, or employees do we have in which
jurisdictions, and which laws does that trigger?"* If
your paying customers are US-only and your employees
are US-only but you take signups from an EU IP address,
GDPR applies. If you have a single European team
member, GDPR applies. There is no threshold under GDPR
that lets a small founder-scope SaaS off the hook —
Article 30 provides a partial exemption for
organisations with fewer than 250 employees, but the
exemption itself has exceptions that swallow the rule
for most SaaS.

## Controller / processor / sub-processor — the vocabulary that decides your obligations

GDPR (Article 4) and, in a slightly different shape,
CCPA (business / service provider / contractor / third
party) distinguish three roles:

- **Controller** (GDPR) / **Business** (CCPA) — the
  party that decides *why* and *how* personal data is
  processed. Your customer is the controller of *their*
  end-users' data; you are the controller of *your
  employees'* data and of your own website visitors'
  data.
- **Processor** (GDPR) / **Service Provider** (CCPA) —
  the party that processes personal data *on behalf of*
  the controller, under a written contract. Your SaaS
  is the processor of your customer's end-users' data.
- **Sub-processor** (GDPR) / **Contractor** (CCPA) —
  any downstream vendor that processes data on the
  processor's behalf. Your cloud provider, your
  observability vendor, your foundation-model vendor
  (chapter 08) are all sub-processors of your
  customer's data.

The load-bearing consequence for a SaaS founder:

- You are a **processor** for customer-uploaded data
  (Article 28 processor obligations apply — you need a
  DPA with each customer, you must maintain records,
  you must notify the controller of breaches without
  undue delay, you must not engage sub-processors
  without controller authorisation).
- You are a **controller** for your own employees,
  contractors, prospects, visitors (a separate set of
  obligations — you owe Article 13 / 14 notice, you
  own the DSR process, you decide legal basis under
  Article 6 / 9).

Confusing these two roles is the single most common
founder-scope privacy mistake. Your DPA with a
customer covers the *processor* role. Your privacy
notice on the website covers the *controller* role.
Both must exist; neither substitutes for the other.

## Article 30 — Records of Processing Activities (RoPA)

GDPR Article 30 requires controllers and processors to
maintain a written record of processing activities.
The ICO ROPA template
([ico.org.uk — Documentation of processing activities template](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/accountability-and-governance/documentation/))
gives the columns; the EDPB has a similar template.
The founder-scope RoPA has two sheets:

### Sheet 1 — Controller RoPA (Article 30(1))

Columns per processing activity:

- Name of the processing activity (e.g., *"employee
  payroll"*, *"prospect email marketing"*,
  *"website analytics"*).
- Purpose of the processing.
- Categories of data subjects (employees, prospects,
  visitors, customers).
- Categories of personal data (name, email, IP
  address, employment record).
- Recipients (internal teams; sub-processors — cross-
  referenced to Sheet 3).
- Third-country transfers (which recipient countries;
  which transfer mechanism — SCCs, adequacy decision,
  binding corporate rules).
- Retention schedule (how long, why).
- Description of technical and organisational security
  measures.

### Sheet 2 — Processor RoPA (Article 30(2))

Columns per processing activity done on behalf of a
customer:

- Name and contact of the controller (each customer).
- Categories of processing carried out on behalf of
  the controller (usually one entry per customer that
  describes the SaaS product's processing of the
  customer's uploaded data).
- Third-country transfers (as above).
- Description of technical and organisational security
  measures.

The founder-scope Article 30 shortcut: **one row per
processing activity for controller data; one row per
customer for processor data**. Do not over-decompose;
a five-page RoPA is a founder-scope RoPA, a
fifty-page RoPA is a compliance-theatre RoPA.

### Sheet 3 — Sub-processor inventory

Not required by Article 30 as a separate document, but
required for the RoPA to be coherent and for the
customer-facing sub-processor list (see below):

- Sub-processor name.
- Purpose (what they do for you).
- Categories of data they process.
- Countries where processing takes place.
- Transfer mechanism (SCCs, DPF, other).
- DPA / BAA status (chapter 08).
- Date last reviewed.

## Data-subject requests — the statutory clock

Both regimes give data subjects rights and a clock to
respond:

- **GDPR** — Articles 15–22 grant rights of access,
  rectification, erasure, restriction, portability,
  and objection. Response due **without undue delay
  and at the latest within one month** (Article 12(3)),
  extendable by two further months for complex requests
  with notice to the data subject.
- **CCPA / CPRA** — grants rights to know, to delete,
  to correct, to opt out of sale / sharing, and to
  limit use of sensitive personal information. Response
  due **within 45 days**, extendable once by a further
  45 days with notice.

The founder-scope DSR handling process:

- **Intake channel.** A single email address
  (`privacy@yourcompany.com` is the convention) and a
  webform. Publish in the privacy notice.
- **Identity verification.** A defensible procedure to
  confirm the requester is who they claim to be
  (email round-trip for logged-in users; ID
  verification for high-risk requests, per the ICO
  guidance).
- **Ticket lifecycle.** A ticket in your issue
  tracker with the statutory clock as the SLA. Owner,
  status, action taken, closure evidence.
- **Fulfilment mechanisms.** For access requests —
  export tooling that pulls user data. For deletion —
  a documented deletion mechanism that reaches every
  data store (primary DB, analytics warehouse, backups,
  logs, and every sub-processor with the data). For
  opt-out of sale / sharing — the mechanism your
  privacy notice describes.
- **Backup exception.** For deletion, backups are
  usually handled by an exception rule (the deletion
  is logged as pending; the backup expires under the
  standard retention schedule; the data is
  cryptographically shredded or logically excluded
  from restore).
- **Log.** A DSR log kept as SOC 2 evidence.

The founder-scope discipline: build the DSR process
*before* the first request lands. The first request
lands earlier than you think — typically within weeks
of the first public launch.

## DPA templates for downstream vendors

Under GDPR Article 28, you cannot use a sub-processor
without a written contract that binds them to
processor-appropriate obligations. Under CCPA, similar
service-provider contracting obligations apply. Every
vendor that touches personal data must have a signed
DPA on file.

Almost every mature SaaS vendor publishes a DPA — most
are click-to-accept in the vendor's admin console or
attached to the master service agreement. The
founder-scope acquisition workflow (chapter 08):

- Identify every vendor that receives personal data.
- Locate the vendor's published DPA.
- Confirm signature / acceptance is captured.
- If the vendor does not publish a DPA, request one
  (a sales-assisted step at most enterprise-tier
  vendors); if they refuse or their DPA is inadequate
  under Article 28, they are a compliance risk and
  the vendor decision should be revisited.
- File the executed DPA in the vendor artefact
  library.

The founder-scope trap: do not draft your own DPA to
send to vendors — use the vendor's DPA. Drafting your
own inbound DPA is a counsel-scope activity and adds
weeks to procurement.

For the outbound direction (the DPA *your* customers
sign with *you*), publish your DPA on your website and
make it click-to-accept where possible. The IAPP
maintains a DPA template resource
([iapp.org — Data Processing Agreements](https://iapp.org/resources/topic/data-processing-agreements-dpa/))
and the European Commission publishes standard
contractual clauses
([commission.europa.eu — Standard Contractual Clauses](https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/standard-contractual-clauses-scc_en))
for the cross-border-transfer scenario. Counsel
adapts these to your specific product.

## Data-residency choices

The residency decision is a product choice with legal
consequences. Three founder-scope patterns:

- **US-only residency.** Data lives in US cloud
  regions; EU customer data crosses under an
  appropriate transfer mechanism — since 2023, the
  EU–US Data Privacy Framework
  ([commission.europa.eu — DPF](https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/eu-us-data-privacy-framework_en))
  if the vendor is DPF-certified, or Standard
  Contractual Clauses otherwise. Simplest posture;
  requires transfer-mechanism documentation. Not
  acceptable for some EU public-sector or highly
  regulated buyers.
- **US + EU dual-region.** Customer data can be
  pinned to an EU region at customer request or by
  default for EU-domiciled customers. The most common
  founder-scope pattern once EU customer count is
  material. Requires tenant-region routing at the
  application layer and duplicated infrastructure
  (backups, observability, sub-processors) in both
  regions.
- **Multi-region with sovereignty features.** EU
  region uses EU-sovereign services (AWS European
  Sovereign Cloud
  [aws.amazon.com/compliance/european-sovereign-cloud](https://aws.amazon.com/compliance/european-sovereign-cloud/),
  Microsoft EU Data Boundary
  [microsoft.com — EU Data Boundary](https://www.microsoft.com/en-us/trust-center/privacy/european-data-boundary-eudb),
  Google Sovereign Cloud / partners
  [cloud.google.com — Sovereign solutions](https://cloud.google.com/sovereign-solutions)),
  and no data path exits the EU. Required only for
  specific EU public-sector or regulated-industry
  customers. Do not adopt this posture speculatively
  — the operational cost is a large multiple of
  dual-region.

The founder-scope decision usually goes: start
US-only with DPF / SCC transfer mechanism; commit to
EU-region dual-residency in the design when EU
enterprise pipeline first appears; adopt EU-sovereign
only under a specific customer requirement.

## Cookie consent

Cookie consent is the operational surface most likely
to be caught by a regulator or a complainant, because
it is publicly visible. GDPR (recital 30 + ePrivacy
Directive) and the guidance from EU DPAs
([edpb.europa.eu — Guidelines on consent](https://edpb.europa.eu/our-work-tools/general-guidance/guidelines-recommendations-best-practices_en))
require freely-given, specific, informed, and
unambiguous consent for non-essential cookies. The
founder-scope pattern:

- Only strictly-necessary cookies set by default.
- Analytics, marketing, and functional cookies gated
  behind an opt-in consent banner.
- Consent choice recorded and revocable at any time.
- Cookie policy page enumerating each cookie, its
  purpose, its provider, and its retention.

Consent-management platforms — OneTrust CMP, Osano,
Cookiebot, Termly, Iubenda — do this out of the box.
For a founder-scope SaaS, a self-hosted lightweight CMP
(cookieconsent from Osano, or an equivalent) is
usually fine; escalating to a full CMP vendor is a
Series-A concern.

CCPA equivalents — the "Do Not Sell or Share" link
required at the footer of the website — are a
separate compliance surface with a distinct mechanism
(the Global Privacy Control signal, per the CPPA
regulations). Cover both.

## The customer-facing privacy notice

Under GDPR Articles 13 / 14 and CCPA sections
1798.100 / 1798.130, the privacy notice must
communicate:

- Identity and contact of the controller and, where
  applicable, the data protection officer (see
  [ICO — DPO](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/accountability-and-governance/data-protection-officers/)
  for when a DPO is required — most founder-scope
  SaaS are not required to appoint one).
- Purposes of processing and legal basis (Article 6 /
  9 basis).
- Recipients (categories of, and where transferred).
- Retention periods.
- Data-subject rights and how to exercise them.
- Right to lodge a complaint with a supervisory
  authority.
- Whether provision of data is a statutory /
  contractual requirement.
- Existence of automated decision-making including
  profiling.

The founder-scope privacy notice is a one-page (short-
form) plus long-form structure. Publish both; keep the
short form under 500 words; keep the long form under
3,000 words. Update the *"last updated"* date on every
material change and archive prior versions.

## The boundary to counsel

Every one of the following is a counsel-scope
activity, not a CTO-scope activity:

- Determining the *legal basis* under Article 6 /
  Article 9 for each processing activity.
- Drafting the privacy-notice copy (the CTO drafts
  the technical-facts section; counsel drafts the
  legal-basis and rights sections).
- Deciding whether a Data Protection Impact
  Assessment (Article 35) is required, and
  conducting it.
- Deciding whether a DPO appointment is required
  (Article 37).
- Deciding whether a cross-border transfer requires
  SCCs, DPF, or a Transfer Impact Assessment.
- Drafting the customer-facing DPA and the vendor-
  facing DPA redlines.
- Handling a regulator inquiry (Article 33 breach
  notification within 72 hours; ICO / CNIL / other
  DPA correspondence).
- Handling a subject-access request that raises a
  legal-privilege question, a right-of-others question,
  or a manifestly-unfounded / excessive question.

The CTO produces the *defensible package* — RoPA,
sub-processor list, DPA copies, DSR log,
data-flow diagram, technical-safeguards description.
Counsel turns the package into contract language,
privacy-notice copy, regulator correspondence, and
privileged advice.

## Summary

- GDPR and CCPA are distinct laws that partially
  overlap. Assuming a control that satisfies one
  satisfies the other is the most common founder-
  scope privacy mistake.
- Applicability triggers: GDPR applies to any
  processing of EU-resident personal data regardless
  of establishment; CCPA applies on revenue / volume
  / sale-share thresholds; other US state laws apply
  on similar patterns.
- The controller / processor / sub-processor split
  decides your obligations. Your SaaS is a *processor*
  for customer data and a *controller* for employee
  and prospect data; both roles must be documented
  and both must produce a privacy notice / DPA.
- Article 30 RoPA is the load-bearing document —
  controller sheet + processor sheet + sub-processor
  inventory. Keep it under five pages at founder
  scope; extend as the vendor list grows.
- The DSR process must exist before the first
  request lands. Response clock: GDPR one month
  (extendable by two); CCPA 45 days (extendable by
  45).
- Every downstream vendor that touches personal data
  needs a signed DPA. Use the vendor's DPA — do not
  draft your own inbound.
- Data-residency choices: US-only with DPF / SCC →
  dual-region → EU-sovereign, adopted in that order
  as customer pressure demands.
- Cookie consent and the CCPA *"Do Not Sell or
  Share"* link are separate, publicly-visible
  compliance surfaces; regulators find gaps here
  first.
- Legal basis, DPIA, DPO appointment, and any
  regulator correspondence are counsel-scope, not
  CTO-scope. The CTO produces the defensible
  package; counsel turns it into contract language
  and legal opinion.

The exercise for this chapter —
`exercise-03-gdpr-and-ccpa-saas-baseline-drill.md` —
ships the RoPA v0, the DSR handling process, the DPA
template, the data-residency decision, the cookie-
consent posture, and the customer-facing privacy
notice draft for your own startup.
