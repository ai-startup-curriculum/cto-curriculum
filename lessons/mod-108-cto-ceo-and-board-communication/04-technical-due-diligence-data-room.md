# Technical Due-Diligence Data Room — Architecture, Security, IP, Answers-File

> "The point of the data room is not to *impress* the
> buyer. The point is to remove every reason for the
> buyer's DD lead to type the phrase 'this raises a
> concern' into their partner memo." — the framing
> this chapter is organised around.

## Motivation

Technical due diligence — for a fundraise (Series-A and
beyond) or an acquisition — is one of the highest-
leverage moments in a company's life and one of the
places where preparation most directly translates into
valuation. A well-prepared data room can compress a
6-week diligence window to 2 weeks (letting the round or
the deal close before market conditions shift), can
neutralise the price-cut angles a hostile technical DD
lead would otherwise attack (chapter 05), and can move
the buyer's DD lead from *hunting for risk* to
*confirming the story*.

An unprepared data room does the opposite. Every gap
the buyer discovers on their own — an OSS licence the
company was quietly using without an assignment, a
contributor with no signed CLA, an incident that never
got written up, a dependency inventory that does not
match what the buyer's tooling finds in the repo — is a
price-cut lever the buyer's team has been trained to
identify and exploit.

This chapter is the six-folder data-room layout the CTO
should be able to instantiate in a week when a term
sheet or an LOI arrives, and — more usefully — should
have installed *as a running artifact* so that when the
term sheet arrives, the folder already exists.

## The six-folder DD data-room layout

The public-facing versions of the standard technical-
DD checklists — most notably a16z's technical-DD
checklist at
[a16z.com/tech-diligence-checklist](https://a16z.com/tech-diligence-checklist/) —
converge on a similar breakdown. The layout the CTO
should install as a running artifact:

```text
docs/dd-data-room/
├── 01-architecture-overview/
├── 02-security-posture-packet/
├── 03-ip-hygiene/
├── 04-engineering-org-and-key-persons/
├── 05-incident-history-and-postmortems/
└── 06-answers-file/
```

Each folder has a specific purpose and a specific set
of load-bearing artifacts. The rest of this chapter
walks each folder.

## Folder 01 — Architecture overview

The architecture overview is the buyer's DD lead's
first read and their most-repeated reference throughout
the process. It is not a marketing document; it is a
technical document at the level a senior technical
reviewer can consume in one hour and be able to sketch
your system on a whiteboard.

The load-bearing artifacts:

- **A C4 model context and container diagram** — see
  [c4model.com](https://c4model.com/) — of the system.
  The context diagram names the actors (users, admins,
  external systems, integrations, foundation-model
  providers) and their interaction surface with the
  company's product. The container diagram names the
  services and datastores at the level a new senior
  engineer would need to understand *"what runs
  where"*.
- **A short (2-4 page) narrative** of the architecture:
  the choice of language and framework, the cloud
  provider(s) and region posture, the persistence
  layer, the deployment topology, the multi-tenancy
  model, the AI/model stack (if AI-native).
- **The ADR log** — the running set of architecture
  decision records from
  [`mod-102`](../mod-102-architecture-under-uncertainty/README.md),
  reduced to the material load-bearing ones for the
  DD reader. Each ADR names the decision, the
  alternatives considered, and the reversibility
  posture.
- **A capacity and cost profile** — current per-tenant
  and per-workload cost, current unit economics,
  where the cost curve is going as usage scales, and
  what the largest cost-optimisation levers are.
- **A roadmap of known architectural changes** — the
  next 12-18 months, the ones the CTO would ship
  regardless of the acquisition or the round, and
  the ones that would be re-evaluated inside the
  acquirer's stack.

The negative-space test: a senior engineer at the
buyer, reading only this folder, should be able to
describe your system back to their team in a 45-minute
briefing. If they cannot — if they have to ask
follow-ups that the folder does not answer — the
folder is under-scoped.

## Folder 02 — Security-posture packet

The security-posture packet is where the compliance
package from
[`mod-107`](../mod-107-founder-scope-security-and-compliance/README.md)
lands in the DD data room. The core artifacts:

- **The one-page posture memo** from
  [`mod-107` chapter 01](../mod-107-founder-scope-security-and-compliance/01-founder-scope-security-posture.md)
  — updated to the current quarter.
- **The SOC 2 attestation or readiness report.** If
  Type II is complete, the report; if Type I is
  complete and Type II is in the observation window,
  the Type I report and the Type II timeline; if
  neither is complete, the readiness assessment from
  a qualified auditor with a specific dates-and-scope
  timeline.
- **Penetration-test summary and remediation status.**
  A summary letter from a recent third-party pen test
  (at founder scope, annually is a reasonable
  cadence), the findings by severity, and the
  remediation status of each. The full report is a
  privileged document typically shared only under a
  clean-room NDA.
- **Incident history log** (referenced in folder 05 in
  more depth). The security-posture packet includes
  a summary: how many incidents of what severity in
  the last 24 months, the customer-notification
  history, and any regulator interactions.
- **Dependency inventory / SBOM.** A machine-readable
  Software Bill of Materials — see
  [CycloneDX](https://cyclonedx.org/) or
  [SPDX](https://spdx.dev/) — for each shipping
  service, with the licence and version pinning
  visible. This is one of the most-frequently-asked
  and least-frequently-prepared artifacts.
- **Vendor inventory with DPAs / BAAs.** The signed
  sub-processor list from
  [`mod-107` chapter 08](../mod-107-founder-scope-security-and-compliance/08-vendor-dpa-and-baa-acquisition.md),
  with the DPA or BAA copy referenced per vendor.
- **Data-flow diagram** for the categories of data
  the system processes (PII, PHI where applicable,
  financial data where applicable, customer content),
  with the residency posture per data class.
- **The current OWASP ASVS gap register** from
  [`mod-107` chapter 06](../mod-107-founder-scope-security-and-compliance/06-owasp-asvs-as-appsec-catalog.md)
  and the SLSA build-provenance status from
  [`mod-107` chapter 07](../mod-107-founder-scope-security-and-compliance/07-slsa-and-build-provenance.md).

Every artifact in this folder is *already produced* by
the exercises in mod-107. The DD-data-room discipline
is to keep them in a single sub-tree, updated
quarterly, so that when the term sheet arrives, the
folder is current rather than reconstructed under time
pressure.

## Folder 03 — IP hygiene

IP hygiene is the folder that most reliably surfaces
*hidden* diligence findings — problems the company has
been carrying for a year or more without realising —
and the folder where a prepared data room most
compounds valuation. The load-bearing artifacts:

- **Employment agreements with IP-assignment clauses**
  for every current and former employee, contractor,
  and founder. Every person who has written code (or
  produced any other IP) that ships in the current
  product has signed an assignment of that IP to the
  company. Gaps here are the most-common price-cut
  finding at Series-B and acquisition DD; the fix is
  a *"prior IP assignment amendment"* signed under
  counsel — see the standard startup templates at
  [Cooley GO — Confidential Information and Invention Assignment Agreement (CIIAA)](https://www.cooleygo.com/documents/confidential-information-and-invention-assignment-agreement/).
- **Contributor licence agreements (CLAs) or Developer
  Certificate of Origin (DCO)** for every external
  contributor to any OSS project the company
  maintains or that the company's product depends
  on with a non-standard licence. See the
  [Developer Certificate of Origin](https://developercertificate.org/)
  and the CNCF's
  [CLA guidance](https://github.com/cncf/foundation/blob/main/policies/cla-vs-dco.md).
- **OSS licence audit.** A comprehensive list of every
  OSS dependency in every shipping service, with the
  licence and any redistribution / notice /
  source-availability obligations attached. The
  categories that most-often trip a DD lead:
  copyleft (GPL / AGPL) dependencies with unclear
  boundary handling; SSPL, BSL, or other source-
  available licences with commercial-use
  restrictions; dependencies without a clearly named
  licence at all. Tools like
  [FOSSA](https://fossa.com/),
  [Snyk (licence scanning)](https://snyk.io/),
  [ScanCode Toolkit](https://scancode-toolkit.readthedocs.io/),
  or [ORT — OSS Review Toolkit](https://oss-review-toolkit.org/)
  automate the scan; the human review is the CTO's
  responsibility.
- **Company patents, applications, and trademarks.**
  A list of filed and pending IP, with jurisdiction
  and status per item. Founder patents that were
  never assigned to the company are the single
  highest-cost hidden IP finding.
- **Third-party licence obligations that survive
  acquisition.** Enterprise-vendor obligations,
  reseller agreements, and OEM licences whose terms
  may change on change-of-control. The buyer's DD
  lead will ask; having the list already assembled
  is compounding.
- **Assignment of foundation-model outputs.** Where
  the product is AI-native and includes generated
  content, the current legal posture on the
  ownership of foundation-model outputs — Anthropic,
  OpenAI, Google DeepMind, and the rest publish
  their commercial-use terms
  ([Anthropic Terms of Service](https://www.anthropic.com/legal/consumer-terms),
  [OpenAI Business Terms](https://openai.com/policies/business-terms/),
  [Google Cloud Vertex AI terms](https://cloud.google.com/vertex-ai/generative-ai/docs/terms/generative-ai-terms))
  and the DD lead will ask which set of terms
  applies to which product surface. Route the
  underlying legal opinion to counsel; the CTO
  supplies the technical fact of which model touched
  which surface.

## Folder 04 — Engineering org and key-person register

The buyer's DD lead is looking for key-person risk —
places where the loss of a single named person would
materially harm the buyer's ability to operate the
acquired system. The folder acknowledges the risks
that exist and names the mitigations.

The load-bearing artifacts:

- **Current org chart** with role, tenure, and
  whether-vested-through-cliff status per person.
- **A key-person register.** A short list (typically
  3-8 at seed / Series-A) of the roles where key-
  person risk is genuinely load-bearing today, with
  the specific mitigation for each: cross-training,
  documented runbooks, hiring in flight, retention
  bonus, redundancy in a specific ownership area.
- **Retention posture.** The current equity refresh
  cadence for senior engineers, the retention bonus
  posture, and any explicit retention plan for
  identified key persons. The buyer's DD lead will
  often ask *what percentage of the current
  engineering team is expected to accept a retention
  package post-acquisition* — even the qualitative
  version of this answer is more useful than none.
- **Immigration and work-authorisation status** for
  key persons where relevant. Not published to the
  buyer at first pass — this is a privileged detail
  routed via counsel — but tracked internally.
- **Hiring plan and hiring pipeline health.** The
  approved hiring plan from the last board meeting,
  actuals against the plan, and the current pipeline
  by role (candidates in loop, offer-out, and
  accepted-not-started).

## Folder 05 — Incident history and post-mortems

The single most-under-installed folder in most seed /
Series-A companies and the folder that most-directly
signals the quality of the engineering culture to a
diligent buyer. The buyer expects the answer to *"how
many incidents in the last 24 months?"* to not be
zero. A company that has never had an incident is a
company that either has not been running long enough
to have had one, or does not detect them; both
conclusions favour the buyer.

The load-bearing artifacts:

- **The rolling incident log** from
  [`mod-106` chapter 07](../mod-106-scaling-org-and-stack/07-delivery-cadence-and-on-call.md)
  — every material incident since incorporation, in
  the same numbering scheme, with the customer-
  notification and regulator-notification status per
  incident.
- **Post-mortems** for every P0 and P1 incident, in
  the blameless format the SOC 2 Availability
  criterion measures against. The DD lead reads
  these for two things: the *quality* of the retro
  (real, blameless, action-item-tracked) and the
  *pattern* across retros (is the same class of
  incident recurring?).
- **The customer-notification history.** Every
  customer notification issued under an SLA-breach
  clause or a security-notification clause, with
  the notification text and the customer response
  captured.
- **Regulator interactions** where they have
  occurred. Any HHS OCR contact under HIPAA, any
  supervisory-authority contact under GDPR, any
  state attorney-general breach notification.
  Route the underlying legal opinion via counsel;
  the CTO supplies the fact of the interaction and
  the correspondence log.

## Folder 06 — The answers-file

The answers-file is the single most-time-saving
artifact in the entire data room and the one most
often missing. It is a running document that answers
— in the CTO's own voice — the recurring set of
diligence questions that appear in every DD process.
Its purpose is threefold: to give the buyer's DD lead
answers *before* they ask; to ensure that when they
do ask, the CTO's answer is consistent across meetings
and across DD leads; and to accelerate the DD process
by eliminating the round-trip lag.

A durable answers-file has, at a minimum, answers to:

- **The stack.** What language, framework, cloud,
  datastore, message bus, background-job system, and
  observability stack does the product run on?
- **The tenancy model.** Single-tenant / pooled-
  tenant / multi-tenant hybrid. Data-isolation
  boundaries.
- **The AI/model stack.** Which foundation-model
  providers, which models, which zero-retention or
  BAA-covered API modes; what workloads run on
  self-hosted vs. API models; the fallback posture
  when the primary provider is unavailable.
- **The data lifecycle.** What data classes exist,
  where each is stored, how each is encrypted, what
  the retention posture is, how DSR / DSAR
  (data-subject-request) handling works, how
  deletion is verified.
- **The deployment model.** How releases work, how
  many deploys per week, how rollbacks work, what
  the change-management posture is, whether there
  is a documented release-gating process.
- **The observability and on-call posture.** How
  incidents are detected, who is on-call, what the
  SLA / SLO commitments are, what tooling is used.
- **The scaling posture.** How the system scales
  today, what the next scaling bottleneck is, what
  the architectural response will be.
- **The security posture** (short-form of Section 4
  of the board pre-read and folder 02 of the DD
  data room).
- **The compliance posture.** Which attestations are
  in place, which are in progress, which are
  deliberately deferred and why. The one-paragraph
  posture articulation from
  [`mod-107` chapter 01](../mod-107-founder-scope-security-and-compliance/01-founder-scope-security-posture.md)
  serves as the anchor.
- **The engineering-team posture.** Team size,
  seniority distribution, ownership model, on-call
  distribution, the growth plan for the next 12
  months.

The answers-file is *not* legalese — it is a
technical document written for a technical reader.
Every answer is short (typically 1-3 paragraphs),
concrete (specific vendors, versions, numbers), and
current (dated on the last-revised line).

## The running-artifact discipline

The single biggest determinant of whether the data
room works is whether it exists *before* the term
sheet or LOI arrives. Two patterns:

- **Pattern A — reactive.** The founders receive the
  term sheet, spend two weeks assembling the data
  room from source materials scattered across
  Slack, Notion, Google Docs, GitHub, and personal
  drives, and produce a version that has gaps the
  buyer's DD lead identifies within a week. The
  round or the deal extends by three-to-four weeks
  and the buyer has time to renegotiate.
- **Pattern B — running artifact.** The
  `docs/dd-data-room/` sub-tree is a first-class
  part of the repo. Every quarterly board pre-read
  refresh (chapter 03) updates the security-posture
  and incident-history folders. Every ADR from
  [`mod-102`](../mod-102-architecture-under-uncertainty/README.md)
  flows into folder 01. Every new hire triggers an
  employment-agreement / IP-assignment check into
  folder 03. Every incident flows through the on-call
  postmortem process from
  [`mod-106`](../mod-106-scaling-org-and-stack/README.md)
  and lands in folder 05. When the term sheet
  arrives, the data room is a matter of a
  final-quarter refresh, not a two-week build.

Pattern B is what this chapter — and the exercise
for it — is designed to install. The upfront cost is
low (one week to scaffold, then quarterly touches);
the compounding benefit is that the data room is
*ready* on any month of any year, not only on the
months the founders happened to be preparing for a
round.

## Signals the data room needs work

- **The buyer asks a question the answers-file does
  not cover** more than twice in a diligence
  process. Each such question goes into the
  answers-file for next time.
- **Two DD leads (same or different buyer) get
  different answers** to the same question from the
  CTO in different meetings. The answers-file is
  not the anchor, or it is and it is not being
  used. Re-anchor.
- **The security-posture folder is more than one
  quarter out of date.** The DD lead reads the date
  on the SOC 2 attestation, the last pen-test
  summary, the last dependency-inventory refresh.
  Stale artifacts *look* like sloppy engineering.

## Summary

- The DD data room has a **six-folder standing
  layout**: (1) architecture overview, (2) security-
  posture packet, (3) IP hygiene, (4) engineering
  org and key-person register, (5) incident history
  and post-mortems, (6) the answers-file.
- Folder 02 is where the mod-107 compliance package
  *lands* — SOC 2 report, pen-test summary, incident
  history, dependency inventory, DPA / BAA library,
  data-flow diagram, ASVS gap register, SLSA
  posture.
- Folder 03 (IP hygiene) is where hidden diligence
  findings most-often surface — employment IP
  assignment, CLAs / DCO, OSS licence audit, patent
  and trademark filings, third-party licence
  survival, foundation-model output ownership.
- Folder 06 (the answers-file) is the CTO's
  standing brief on the recurring DD questions —
  stack, tenancy, AI/model stack, data lifecycle,
  deployment, observability, scaling, security,
  compliance, team.
- The **running-artifact discipline** — updated
  quarterly through the same cadence that produces
  the board pre-read — is what turns the data room
  from a two-week reactive build into a matter of
  a final-quarter refresh.

The exercise for this chapter —
`exercise-04-technical-due-diligence-data-room-scaffold.md`
— walks the six-folder scaffold for your own repo
and produces the inventory of what you own, what you
owe, and what the answers-file must say.
