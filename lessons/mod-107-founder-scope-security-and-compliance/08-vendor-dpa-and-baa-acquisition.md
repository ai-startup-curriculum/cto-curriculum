# Vendor DPAs and BAAs — Acquiring the Downstream Compliance Artifacts

> "A vendor without a signed DPA in your compliance
> library is not a vendor you can defend on an enterprise
> questionnaire. A foundation-model vendor without a BAA
> — where PHI is in scope — is a HIPAA violation.
> Acquiring both is a procurement discipline, not an
> engineering one." — the discipline this chapter is
> written around.

## Motivation

Enterprise procurement, healthcare procurement, and
Series-B technical due diligence all reach the same
question: *"who processes your customer's data, on
what terms, and under what compliance obligations?"*.
The answer is a **vendor artifact library** — a
folder containing a signed DPA (and, where PHI is in
scope, a BAA) for every sub-processor of customer
data.

At founder scope, the artifact library is often the
single most-overlooked compliance artifact. Vendor
onboarding happens ad-hoc, DPAs are clicked-to-accept
in someone's browser and never centrally filed, BAAs
are signed and forgotten, and when the enterprise
buyer asks for the sub-processor list you are
reconstructing it from memory and Stripe invoices.

This chapter walks the vendor inventory, the DPA and
BAA acquisition process, the specific state of BAA
availability from foundation-model providers as of
this writing, the zero-retention API modes that most
change the AI-native SaaS posture, and the EU-only
data-residency options that unlock EU-heavy account
bases.

## The vendor compliance inventory

The load-bearing artifact this chapter produces is a
**vendor compliance inventory** — a spreadsheet (or a
table in `docs/compliance/vendors.md`) that lists
every third-party service touching customer data,
personal data, or the production environment.
Columns:

- **Vendor** — the company name.
- **Product** — the specific SKU (Vanta, AWS Bedrock —
  us-east-1, OpenAI API Enterprise, etc.).
- **Purpose** — what the vendor does for you.
- **Data categories** — customer content, personal
  data, PHI (if applicable), payment data, logs,
  metadata.
- **Data volume / access scope** — the fraction of
  customer data the vendor sees.
- **Region(s)** — where the vendor processes the
  data (us-east-1, eu-west-1, multi-region, etc.).
- **DPA status** — Executed / Pending / N/A (with
  the *why*).
- **DPA link** — URL or file reference to the
  executed DPA.
- **BAA status** — Executed / Pending / Not required
  (PHI-adjacent) / Not available (vendor does not
  offer BAA).
- **BAA link** — as above.
- **SCC / DPF / transfer mechanism** — the cross-
  border-transfer mechanism, if the vendor is in a
  third country.
- **SOC 2 report** — On file / Requested / Not
  available (with the vendor's own attestation link
  or the last-review date).
- **ISO/IEC 27001 certificate** — On file / N/A.
- **Public sub-processor list** — link to the
  vendor's own sub-processor list.
- **Last reviewed** — date of last vendor review.
- **Owner** — the internal owner of the relationship.

The inventory does two jobs at once: it is the raw
material for the **customer-facing sub-processor
list** (chapter 04's Article 30 requirement), and it
is the *evidence pack* for the vendor-risk-
management control in SOC 2 CC9.2.

## Categorising vendors by acquisition path

Vendor DPAs and BAAs fall into three acquisition
patterns. Knowing which pattern a vendor uses
compresses the acquisition timeline from weeks to
hours.

### Self-serve

The vendor publishes a DPA (and sometimes a BAA) at
a stable URL. You accept it in the admin console or
counter-sign a click-through. No sales interaction
needed. Examples: Stripe DPA
([stripe.com/legal/dpa](https://stripe.com/legal/dpa)),
GitHub DPA
([github.com — GitHub Data Protection Agreement](https://docs.github.com/en/site-policy/privacy-policies/github-data-protection-agreement)),
Cloudflare DPA
([cloudflare.com/cloudflare-customer-dpa](https://www.cloudflare.com/cloudflare-customer-dpa/)),
AWS Artifact for the AWS DPA and BAA
([aws.amazon.com/artifact](https://aws.amazon.com/artifact/)),
Google Workspace DPA
([workspace.google.com/terms/dpa_terms.html](https://workspace.google.com/terms/dpa_terms.html)).

Founder-scope target: **every self-serve DPA / BAA
executed within the week of vendor onboarding**.

### Sales-assisted

The vendor offers a DPA (and sometimes a BAA), but
acquisition requires a sales interaction — an email
to legal, a request via the account manager, a
security-review form. Turnaround usually 1–3 weeks.
Examples: OpenAI API BAA path (via the sales team),
Anthropic Claude Enterprise BAA (via sales), most
enterprise-tier SaaS with a legal-review process.

Founder-scope target: **acquisition initiated
within the week of committing to the vendor**;
executed within 30 days.

### Custom-redlined

The vendor's DPA is a starting point; you counter-
propose changes and negotiate. Rare at founder scope
because the leverage usually is not there; common
at Series-B and beyond. If you are receiving a
DPA that requires redlining, that is a counsel-scope
task, not a CTO-scope task.

## The DPA acquisition workflow

Per vendor:

1. **Confirm the vendor is a data processor.** If
   the vendor never receives personal data (a
   marketing tool that only sees your team's
   accounts, a build-tool that sees no customer
   data), a DPA may not be required. Document the
   determination in the inventory.
2. **Locate the vendor's DPA.** Check the footer of
   the vendor website; check the legal / trust page;
   check the admin console for a *"accept DPA"*
   toggle.
3. **Confirm the DPA covers your role.** You are
   almost always the *controller* (in the DPA
   vocabulary) and the vendor is the *processor* /
   *sub-processor*. If the vendor's DPA does not
   accommodate that shape, escalate to counsel.
4. **Sign / accept.** Capture the executed DPA
   somewhere durable (cloud drive folder in
   `Compliance/Vendors/<vendor>/DPA-<date>.pdf`).
5. **Update the vendor compliance inventory.**
6. **Update the customer-facing sub-processor list**
   if the vendor is a new sub-processor of customer
   data (chapter 04).
7. **Diarise for annual re-review.**

The founder-scope automation: several compliance-
automation tools (Vanta, Drata, Secureframe, etc.)
have vendor-management modules that centralise this
workflow. Use them; the manual alternative is where
DPAs get lost.

## The BAA acquisition workflow — foundation-model providers in detail

The BAA question is the single most-asked HIPAA-
adjacent question at AI-native SaaS founder scope.
The current state, verified as of 2026-08-20 against
each vendor's public compliance pages:

### Anthropic — Claude Enterprise and Enterprise API

- **BAA availability.** Anthropic offers HIPAA
  support with BAA on Enterprise-tier products —
  see the Trust Center at
  [trust.anthropic.com](https://trust.anthropic.com/)
  and the legal / privacy pages at
  [anthropic.com/legal](https://www.anthropic.com/legal).
- **Acquisition path.** Sales-assisted; contact
  Anthropic's sales team via the enterprise contact
  form or your existing account manager.
- **Zero-retention / data-handling.** Claude
  Enterprise and Enterprise API deployments support
  zero-day retention for prompt / completion data
  (with defensible exceptions such as abuse
  monitoring — verify the current wording per the
  contract).
- **What does not carry BAA.** Consumer Claude.ai
  and self-serve Claude API without an Enterprise
  agreement do not carry BAA.

<!-- needs-research: verify Anthropic's current BAA availability wording, self-serve vs. sales-assisted gating, and the zero-retention configuration options as of the reader's audit date. -->

### OpenAI — API BAA path and ChatGPT Enterprise

- **BAA availability.** OpenAI offers a BAA to
  eligible enterprise customers on the API and
  ChatGPT Enterprise — see
  [openai.com/enterprise-privacy](https://openai.com/enterprise-privacy)
  and the Trust Portal at
  [trust.openai.com](https://trust.openai.com/).
- **Acquisition path.** Sales-assisted; the API BAA
  path requires an eligibility review by OpenAI.
- **Zero-retention / data-handling.** ChatGPT
  Enterprise and eligible API endpoints support
  zero-retention configuration; the standard
  consumer ChatGPT and default API paths do not.
- **What does not carry BAA.** Consumer ChatGPT,
  ChatGPT Plus, and standard API access without an
  Enterprise agreement do not carry BAA.

<!-- needs-research: verify OpenAI's current BAA-acquisition process, endpoint eligibility, and zero-retention gating as of the reader's audit date. -->

### AWS Bedrock (and the wider AWS HIPAA-Eligible Services list)

- **BAA availability.** AWS offers a BAA to
  qualifying customers with an eligible Support
  plan; Bedrock is on the AWS HIPAA-Eligible
  Services list — see
  [aws.amazon.com/compliance/hipaa-eligible-services-reference](https://aws.amazon.com/compliance/hipaa-eligible-services-reference/)
  and the AWS HIPAA overview at
  [aws.amazon.com/compliance/hipaa-compliance](https://aws.amazon.com/compliance/hipaa-compliance/).
- **Acquisition path.** Self-serve via AWS Artifact
  ([aws.amazon.com/artifact](https://aws.amazon.com/artifact/))
  once support-plan and identity-verification
  requirements are met.
- **Zero-retention / data-handling.** Bedrock's data-
  privacy commitments — no use of customer data to
  train foundation models, encryption at rest, VPC
  endpoints — are documented in the Bedrock service
  documentation. The specific model-provider terms
  vary; verify per model.
- **What does not carry BAA.** AWS services *not*
  on the HIPAA-Eligible Services list cannot be
  used for PHI even under the AWS BAA.

### Azure OpenAI Service

- **BAA availability.** Microsoft's HIPAA BAA covers
  Azure OpenAI Service — see
  [learn.microsoft.com — HIPAA / HITECH offering](https://learn.microsoft.com/en-us/azure/compliance/offerings/offering-hipaa-hitech)
  and the Microsoft Trust Center at
  [microsoft.com — Trust Center — HIPAA](https://www.microsoft.com/en-us/trust-center/compliance/hipaa).
- **Acquisition path.** BAA is embedded in the
  Microsoft Online Services Terms (the OST) for
  eligible enterprise customers.
- **Zero-retention / data-handling.** Azure OpenAI
  offers a documented data-handling and
  abuse-monitoring model, including a process for
  requesting modification of the abuse-monitoring
  retention where required — see
  [learn.microsoft.com — Azure OpenAI data privacy](https://learn.microsoft.com/en-us/legal/cognitive-services/openai/data-privacy).

### Google Cloud Vertex AI

- **BAA availability.** Google Cloud offers a BAA
  covering Vertex AI to qualifying customers — see
  [cloud.google.com/security/compliance/hipaa](https://cloud.google.com/security/compliance/hipaa)
  and the HIPAA implementation guide at
  [cloud.google.com — HIPAA on Google Cloud](https://cloud.google.com/architecture/hipaa-compliance-on-gcp).
- **Acquisition path.** BAA workflow in the Cloud
  Console for eligible customers.
- **Zero-retention / data-handling.** Vertex AI's
  data-handling commitments — customer data not
  used to train foundation models by default,
  encryption at rest, VPC Service Controls — are
  documented in the Vertex AI documentation.

<!-- needs-research: the four vendor entries above should be re-verified against each vendor's current compliance page and BAA-acquisition workflow before a founder-scope reader commits to any specific product. -->

## Zero-retention API modes

Separate from BAA availability, several foundation-
model providers offer **zero-retention** or
**customer-controlled retention** modes that
substantially change the compliance posture even for
non-HIPAA workloads. The founder-scope value:

- Reduces the data-flow risk if the prompt or
  completion contains regulated data (PII, PHI,
  intellectual property).
- Reduces the sub-processor scope for GDPR / CCPA —
  a vendor that retains no data has a smaller
  processor footprint.
- Reduces the incident-response blast radius —
  there is less to be exposed in a hypothetical
  vendor incident.

The founder-scope pattern is to configure zero-
retention (or the shortest defensible retention) on
every foundation-model API path where PII, PHI, or
regulated data can enter the prompt. The tradeoff
is usually the loss of abuse-monitoring features,
which some vendors gate the zero-retention mode
behind an eligibility review to preserve.

## EU-only data-residency options for foundation-model providers

The residency question (chapter 04) applies to
foundation-model vendors as much as to any other
sub-processor. Founder-scope state as of this
writing:

- **AWS Bedrock** — available in specific EU regions
  (eu-central-1, eu-west-3, and others depending on
  the model). Verify per model at
  [aws.amazon.com/bedrock — model availability](https://aws.amazon.com/bedrock/).
- **Azure OpenAI Service** — available in specific
  EU regions and includes an EU Data Boundary
  commitment for many services (
  [microsoft.com — EU Data Boundary](https://www.microsoft.com/en-us/trust-center/privacy/european-data-boundary-eudb)).
- **Google Cloud Vertex AI** — available in
  specific EU regions; Google Sovereign Cloud
  partners provide additional sovereignty options
  ([cloud.google.com — Sovereign solutions](https://cloud.google.com/sovereign-solutions)).
- **Anthropic** — Claude on AWS Bedrock and GCP
  Vertex AI inherits region availability from the
  underlying cloud; direct Anthropic API region
  availability should be verified with Anthropic
  directly.
- **OpenAI** — Azure OpenAI Service is the primary
  path to EU-resident OpenAI models; direct OpenAI
  API region availability should be verified with
  OpenAI directly.

<!-- needs-research: verify current EU-region and EU-Data-Boundary availability per foundation-model vendor as of the reader's audit date. -->

The founder-scope pattern: if your EU pipeline is
material, prefer the cloud-hosted path (Bedrock,
Azure OpenAI, Vertex) over the direct-vendor API
because the cloud-provider's residency posture
extends to the model inference; if your EU pipeline
is not material, the direct-vendor API is simpler.

## The wider SaaS stack — a founder-scope vendor list

The vendors that most reliably appear on a founder-
scope SaaS's compliance inventory:

- **Cloud infrastructure** — AWS, GCP, Azure, or a
  smaller cloud (Fly.io, Render, Vercel, Netlify).
  DPA and BAA (where applicable) via the cloud's
  own compliance page.
- **CDN / edge** — Cloudflare, Fastly, AWS
  CloudFront. DPA via the vendor.
- **Foundation-model API** — Anthropic, OpenAI, AWS
  Bedrock, Azure OpenAI, GCP Vertex, or a smaller
  provider. DPA and BAA per the section above.
- **Vector database** — Pinecone, Weaviate,
  Chroma-hosted, Qdrant Cloud. Verify DPA per
  vendor; verify data-residency options.
- **Observability** — Datadog, New Relic, Honeycomb,
  Splunk, Sentry. DPA via vendor; BAA on
  enterprise tier where applicable.
- **Error tracking** — Sentry, Rollbar. DPA via
  vendor.
- **Analytics** — Mixpanel, Amplitude, PostHog,
  Segment, Rudderstack. DPA per vendor.
- **Email** — SendGrid / Twilio, Postmark, Mailgun,
  AWS SES. DPA per vendor.
- **Support / helpdesk** — Zendesk, Intercom,
  HubSpot, Front. DPA per vendor.
- **Auth / identity** — Auth0 / Okta, Clerk,
  WorkOS, Stytch. DPA per vendor.
- **Payments** — Stripe, Braintree, Adyen. DPA per
  vendor; note the PCI DSS boundary.
- **Compliance automation** — Vanta, Drata,
  Secureframe, Sprinto, Thoropass. DPA per vendor.
- **CRM / marketing** — HubSpot, Salesforce.
  Controller relationship (your prospect data), DPA
  per vendor.
- **Team collaboration** — Slack, Notion, Linear,
  Google Workspace. Controller relationship (your
  team data), DPA per vendor.

Every entry above should have a row in the vendor
compliance inventory. Every entry above where the
vendor touches customer data should be on the public
sub-processor list. Every entry above where the
vendor touches PHI (Architecture A / C from chapter
05) must have a BAA.

## Publishing the customer-facing sub-processor list

The sub-processor list is a public URL, usually at
`yourcompany.com/subprocessors` or in the trust
center. GDPR Article 28(2) requires that the
processor obtain the controller's prior specific or
general authorisation for engaging a sub-processor —
the standard SaaS pattern is:

- Publish the list.
- Commit in the DPA to give customers X days'
  notice (usually 15–30) before engaging a new
  sub-processor.
- Give customers the right to object; if the customer
  objects and the objection cannot be resolved,
  either terminate the contract or exempt the
  customer's data from the new sub-processor.

The list should contain: vendor name, purpose of
processing, categories of data processed, location
of processing. Do not publish internal vendor
identifiers, contract details, or pricing.

Version the list — archive prior versions with the
effective-date range. When the SOC 2 auditor or a
customer asks *"what were your sub-processors on
2026-06-01?"*, the archived list is the answer.

## The boundary to counsel

Counsel-scope activities in the vendor-DPA / BAA
domain:

- Redlining any DPA or BAA the vendor's default is
  inadequate for your use.
- Drafting the customer-facing DPA and the customer-
  facing MSA.
- Legal-basis analysis for cross-border transfers
  (which mechanism — DPF, SCCs, BCRs — applies to
  which sub-processor in which country).
- Legal opinion on whether a specific vendor's terms
  satisfy Article 28 or the CCPA service-provider
  requirements.
- Notice-and-cure mechanics if a vendor breach
  occurs.

The CTO produces the vendor inventory, the
sub-processor list, the DPA / BAA artifact library,
and the flow-of-data documentation. Counsel turns
the package into contract language and legal
opinion.

## Summary

- The vendor compliance inventory is the load-
  bearing artifact — one row per third-party
  service touching customer data, personal data, or
  production, with DPA / BAA / SOC 2 / ISO 27001
  status, region, and last-reviewed date.
- Vendors fall into three DPA-acquisition
  patterns: self-serve (click-through), sales-
  assisted (1–3 weeks), custom-redlined (counsel-
  scope). Founder-scope target: self-serve within
  the onboarding week, sales-assisted within 30
  days.
- Foundation-model BAA availability (verified as of
  writing): Anthropic (Claude Enterprise /
  Enterprise API, sales-assisted), OpenAI (API BAA
  path, sales-assisted), AWS Bedrock (via AWS
  Artifact), Azure OpenAI (via Microsoft OST), GCP
  Vertex (via Cloud BAA workflow).
- Zero-retention API modes reduce the sub-processor
  scope and the incident-response blast radius;
  configure on any path where regulated data can
  enter the prompt.
- EU-residency for foundation-model inference is
  most reliably reached via the cloud-hosted path
  (Bedrock, Azure OpenAI, Vertex) rather than the
  direct-vendor API; verify per model and per
  region.
- The wider founder-scope SaaS vendor list (cloud,
  CDN, observability, email, auth, payments, CRM,
  team-collab, compliance-automation) must all be
  covered by the inventory. Every vendor touching
  PHI must have a BAA; every vendor touching
  customer data must be on the public sub-processor
  list.
- Publish the sub-processor list at a public URL,
  version it, and commit in the DPA to a notice
  window and an objection right.
- DPA redlining, cross-border-transfer legal-basis
  analysis, and vendor-contract opinion are
  counsel-scope. The CTO produces the artifact
  library.

The exercise for this chapter —
`exercise-07-vendor-dpa-and-baa-acquisition-drill.md` —
walks the vendor inventory, the DPA / BAA
acquisition process for your top-10 vendors, and the
sub-processor list that becomes the SOC 2 and GDPR
evidence.
