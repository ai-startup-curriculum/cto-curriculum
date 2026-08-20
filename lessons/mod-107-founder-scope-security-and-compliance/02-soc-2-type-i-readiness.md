# SOC 2 Type I Readiness — Trust Services Criteria, Scope, ISMS, Evidence

> "A SOC 2 Type I says *your controls existed on the day
> the auditor looked*. A SOC 2 Type II says *your controls
> operated over a six-to-twelve-month window*. The two
> reports are not the same product; enterprise buyers know
> the difference." — the vocabulary discipline this
> chapter is written around.

## Motivation

SOC 2 is the single most-asked-for compliance artifact
in US B2B SaaS procurement. It is also the artifact most
often misunderstood by first-time founder-CTOs, who
either (a) treat it as a checkbox exercise and are
shocked when the audit takes six months instead of six
weeks, or (b) treat it as an insurmountable enterprise
programme and defer it until they lose the first design
partner over its absence.

Neither reaction is correct. SOC 2 Type I readiness is a
**bounded, self-directed programme** — the CTO scopes
the criteria, writes the policies, deploys the
tooling, and collects the evidence, and then the auditor
attests to what is there. At founder scale, the
programme is measured in weeks of focused work, not in
headcount. The chapter walks the scoping call, the
Trust Services Criteria vocabulary, the ISMS shape the
audit expects to see, and the evidence-collection
cadence that becomes the Type II observation window.

## What SOC 2 actually is

SOC 2 is an American Institute of Certified Public
Accountants (AICPA) attestation framework — see the
[AICPA SOC 2 overview](https://www.aicpa-cima.com/topic/audit-assurance/audit-and-assurance-greater-than-soc-2)
and the *Trust Services Criteria* description at
[aicpa-cima.com — TSC](https://www.aicpa-cima.com/resources/download/trust-services-criteria).
Four properties matter for founders:

- **It is an attestation, not a certification.** A
  licensed CPA firm issues an opinion. There is no
  central SOC 2 registry; the report itself is the
  artifact.
- **It applies to the service organisation, not to a
  product.** The scope is the *system* — usually the
  production SaaS environment — plus the supporting
  people, processes, and infrastructure.
- **It comes in two report types.** Type I attests to
  the *design* of controls as of a point in time.
  Type II attests to both the *design* and the
  *operating effectiveness* over an *observation
  window* — typically 6 or 12 months.
- **It has five Trust Services Criteria (TSC), of
  which only one is mandatory.** *Security* (the
  Common Criteria) is required. Availability,
  Processing Integrity, Confidentiality, and Privacy
  are optional add-ons that answer specific customer
  questions.

The load-bearing consequence: a SOC 2 Type I report
issued in month 6 followed by a Type II report issued
in month 12 (after a 6-month observation window) is a
standard sequence. If a customer demands Type II *now*
and you have not started, the earliest a Type II report
can exist is 6–12 months from today. Planning backward
from the customer commitment is the point of chapter 08
of the AICPA guidance and of this chapter.

## The five Trust Services Criteria and the scope call

The 2017 TSC (updated 2022) name five criteria. Each
criterion is a set of *points of focus* — implementation
suggestions the auditor uses to test whether the
criterion is met. The full TSC document is available at
[aicpa-cima.com — Trust Services Criteria](https://www.aicpa-cima.com/resources/download/trust-services-criteria).

### Security — always in scope (the "Common Criteria")

The Common Criteria (CC series — CC1 through CC9) are
mandatory for every SOC 2. They cover:

- **CC1 — Control Environment.** Governance, tone at
  the top, code of conduct, background checks.
- **CC2 — Communication and Information.** Internal
  communication of policies; external communication of
  commitments; whistleblower channel.
- **CC3 — Risk Assessment.** Objectives, risks
  identification, risk-tolerance framework, fraud risk.
- **CC4 — Monitoring Activities.** Ongoing evaluations,
  separate evaluations, communication of deficiencies.
- **CC5 — Control Activities.** Selection of controls,
  technology general controls, policies.
- **CC6 — Logical and Physical Access.** IAM, MFA,
  network security, encryption, workstation security.
- **CC7 — System Operations.** Vulnerability
  management, incident response, change monitoring,
  data backup.
- **CC8 — Change Management.** Change authorisation,
  design, testing, and deployment.
- **CC9 — Risk Mitigation.** Business-continuity
  planning, vendor risk management.

A founder-scope SOC 2 that covers only Security is a
**complete, defensible report** on its own. Do not add
optional criteria unless a specific customer or
regulatory driver requires them.

### Availability — add if the customer contract commits to uptime SLAs

Availability adds the A series criteria (A1.1–A1.3) —
capacity monitoring, environmental protections,
recovery. Add this criterion if you have a signed uptime
SLA or a public one. Skip it if you do not — the *"we
were down two hours last quarter"* answer becomes an
audit finding rather than a customer conversation.

### Processing Integrity — add if the SaaS produces or moves financial or measurable output

Processing Integrity adds the PI series
(PI1.1–PI1.5) — completeness, accuracy, and timeliness
of processing. Add this if you are a fintech, a
billing engine, an analytics platform whose outputs are
used for reporting, or any product where the
*correctness* of a computed output is the value being
sold. Skip it if you are a collaboration tool, an
internal-communications app, or any product where
processing correctness is not the differentiator.

### Confidentiality — add if you hold customer-designated confidential data beyond the standard SaaS baseline

Confidentiality adds the C series (C1.1–C1.2) —
protection of confidential information during processing
and after retention. Add this if your customers upload
information they contractually mark as confidential
(intellectual property, unpublished financials, trade
secrets) that is above the standard SaaS-tenancy
protection. Skip it if the standard tenant-isolation
posture is sufficient for the data types you handle.

### Privacy — add if you are a controller of personal information under a US privacy law

Privacy adds the P series (P1.1–P8.1) — notice, choice,
collection, use, retention, disclosure, quality,
monitoring. Add this if you are a controller (not a
processor) of significant personal information under
CCPA / CPRA or another US state privacy law and want a
US-flavoured attestation of your privacy programme.
Skip it if GDPR / CCPA are already covered by the
Article 30 register and DSR process from chapter 04 —
Privacy adds attestation cost without adding customer
signal in most B2B SaaS cases.

### The scope-selection call in one sentence

For a US B2B SaaS founder pursuing enterprise
procurement, the default scope is **Security only** for
the first report; **Security + Availability** if there
is a signed uptime SLA; **Security + Availability +
Confidentiality** if the customer procurement team
explicitly lists Confidentiality. Add Processing
Integrity only where the SaaS is fintech-adjacent, and
Privacy only where a US privacy-law compliance signal
is a specific ask.

## The small-team ISMS shape

The Information Security Management System (ISMS) is
the collection of policies, procedures, and evidence
that the auditor tests against. At founder scale, the
ISMS is 12–20 policies, each 2–5 pages, plus a
control-mapping register and a set of evidence
collection artifacts.

The founder-scope ISMS document set:

- **Information Security Policy** — the top-level
  policy the rest of the ISMS extends. Names the
  security officer role (usually the CTO at founder
  scope), the risk-appetite statement, the annual
  policy-review cadence.
- **Acceptable Use Policy** — how employees use
  company systems, BYOD rules, prohibited activities,
  incident-reporting obligation.
- **Access Control Policy** — the SSO / MFA
  requirement, the least-privilege discipline, the
  quarterly access review, the offboarding checklist.
- **Change Management Policy** — how code and
  configuration changes are proposed, reviewed, and
  deployed; ties to the PR-review, CI, and deployment
  practices from
  [`mod-106` chapter 01](../mod-106-scaling-org-and-stack/01-zero-to-five-first-process.md).
- **Incident Response Policy and Runbook** — severity
  levels, on-call rotation, escalation path, customer-
  notification clock, root-cause analysis format
  (ties to the blameless-post-mortem practice in
  [`mod-106` chapter 07](../mod-106-scaling-org-and-stack/07-delivery-cadence-and-on-call.md)).
- **Business Continuity and Disaster Recovery
  Policy** — RTO / RPO targets, backup cadence,
  restore-test frequency.
- **Vulnerability Management Policy** — dependency-
  update cadence, patch SLA, penetration-test
  cadence, remediation-tracking process.
- **Vendor / Third-Party Risk Management Policy** —
  vendor onboarding review, sub-processor tracking,
  DPA / BAA acquisition process (chapter 08), annual
  vendor review.
- **Data Classification and Handling Policy** — the
  data classes (public / internal / confidential /
  restricted, or your equivalent), the handling
  rules per class, the retention schedule per class.
- **Encryption and Key Management Policy** — in-
  transit (TLS 1.2+ or 1.3), at-rest (cloud-managed
  keys or customer-managed keys), key-rotation
  cadence.
- **Data Retention and Deletion Policy** — retention
  periods per data class, deletion process, backup-
  retention interaction.
- **Physical and Environmental Security Policy** —
  even for a cloud-only SaaS, this covers office
  physical security, workstation security, and cloud
  provider physical inheritance (referencing the
  cloud provider's own SOC 2 as inherited controls).
- **Human Resources Security Policy** — background
  checks, onboarding security training, role change
  and offboarding procedures.
- **Secure Software Development Lifecycle Policy** —
  the discipline the OWASP ASVS (chapter 06) and
  SLSA (chapter 07) chapters give teeth to.
- **Risk Management Policy and Register** — how risks
  are identified, scored, and tracked; the risk
  register itself (frequently the Statement of
  Applicability from ISO/IEC 27001 doubles as the
  founder-scope risk register — see chapter 03).

The two artifacts every founder-scope ISMS needs beyond
the policy set:

- **Control-mapping register** — a spreadsheet with one
  row per SOC 2 criterion (CC1.1, CC1.2, …), one column
  per policy that satisfies it, one column per piece of
  evidence that proves it, and one column per remediation
  item if it is not yet satisfied.
- **Evidence-collection manifest** — the list of what
  evidence is collected on what cadence (daily / weekly
  / monthly / quarterly / annually), by whom, and where
  it is stored.

Compliance automation vendors —
[Vanta](https://www.vanta.com/),
[Drata](https://drata.com/),
[Secureframe](https://secureframe.com/),
[Sprinto](https://sprinto.com/),
[Tugboat Logic (now OneTrust)](https://www.onetrust.com/products/certification-automation/),
[Thoropass](https://thoropass.com/) — automate a
significant fraction of the evidence collection.
Selection of a tool is a build-vs-buy decision
([`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md)):
at founder scope, one of these tools almost always
earns its keep, since the alternative is that a
substantial fraction of the CTO's quarter goes into
manual evidence collection. See the tool-selection
scorecard from
[`mod-103` chapter 05](../mod-103-build-vs-buy-and-platform-economics/README.md)
for the framing.

## The evidence-collection cadence

Type I attests to controls *as of a point in time*.
Type II attests to controls *operating over an
observation window*. The cadence at which you collect
evidence during founder-scope readiness *is* the
cadence the Type II auditor will look for during the
observation window. If you build the cadence during
readiness for Type I, Type II is a much shorter step.

A founder-scope evidence-collection cadence:

- **Daily** — automated backups run and succeed;
  vulnerability-scanner ran; MFA-enforcement policy
  still in effect (cloud-provider-side attestation).
- **Weekly** — dependency-update PRs merged;
  vulnerability-scan findings triaged; on-call
  rotation confirmed for the following week.
- **Monthly** — access review of privileged accounts;
  security-metric roll-up (open findings, MTTR on
  security findings, dependency freshness); vendor
  onboarding / offboarding log update; incident-log
  update.
- **Quarterly** — full user access review across all
  systems; sub-processor list re-confirmed and
  re-published; policy review (rolling — one or two
  policies per quarter, not all at once); business-
  continuity restore test.
- **Annually** — full policy review; risk-assessment
  refresh; penetration test; SOC 2 audit.

The evidence cadence is *not* a set of aspirational
target dates — it is a *ritual*. If any monthly
evidence artifact is missed twice in a row, the
cadence is broken and the auditor will find it. The
discipline is to build the cadence into the calendar
and the on-call rotation from day one.

## The Type I → Type II timeline

The founder-scope timing question is *"when should
Type II be ready?"*, not *"when should Type I be
ready?"*. The Type II observation window is customer-
facing; the Type I is an internal milestone.

The realistic timing math, planned backward from a
customer commitment:

- The customer says *"we need Type II by month 12
  from contract signing"*.
- Type II report requires a completed observation
  window (default: 6 months, sometimes 3, sometimes
  12 depending on customer negotiation and auditor
  posture). So the observation window ends at month 12
  and starts at month 6.
- The Type II observation window can only start once
  Type I is issued (or, per some auditors, once the
  controls are attestable — but the safer plan
  assumes Type I first).
- Type I readiness is typically 8–16 weeks of focused
  work at founder scope for the *first* attestation;
  faster for subsequent renewals.
- Therefore Type I readiness must start no later than
  month 2–3 of the customer relationship for the
  Type II deadline at month 12 to be credible.

If the timeline math does not fit, the honest answer
to the customer is a shorter observation window
(auditor-negotiable, sometimes 3 months for a Type II
"early bird" report) or a longer contract runway. The
dishonest answer — *"yes we'll have Type II by month
12"* when the math does not fit — is the classic
founder-scope compliance breach that destroys the
relationship in month 11 rather than month 3.

## The auditor-selection decision

The auditor is a licensed CPA firm. At founder scope,
the practical selection criteria:

- **Reputation with enterprise procurement.** Some
  auditors' reports are perceived as more rigorous
  than others by buyer-side security teams. Ask three
  of your prospective enterprise customers *"whose
  SOC 2 reports do you accept?"* before selecting.
- **Familiarity with the compliance-automation
  tool you selected.** Vanta / Drata / Secureframe /
  Sprinto / Thoropass each have a list of auditor
  partners whose workflow is integrated with the tool.
  Selecting from that list saves 20–40% of auditor
  time in the first engagement.
- **Startup-scale pricing.** SOC 2 Type I audits at
  founder scale should be in the low five figures for
  the first engagement, higher for the Type II. If
  a quote is a large multiple of this, either the
  scope has ballooned or the auditor is not startup-
  scale.
- **Pre-audit readiness review.** A pre-audit
  readiness review — sometimes called a "gap
  assessment" — from the auditor before formal audit
  fieldwork begins is standard and worth every
  hour. Some auditors bundle it; some sell it
  separately.

The founder-scope discipline: do not delegate auditor
selection to the compliance-automation vendor. The
compliance vendor and the auditor are two separate
relationships; they interact, but they answer to
different parties.

## Summary

- SOC 2 is an AICPA attestation, not a certification;
  it applies to a *system*; it comes in Type I (point-
  in-time design) and Type II (observation-window
  operation).
- Five Trust Services Criteria — Security (mandatory,
  the Common Criteria), Availability, Processing
  Integrity, Confidentiality, Privacy. Founder-scope
  default is *Security only*; add other criteria only
  for a specific customer or regulatory driver.
- The ISMS at founder scope is 12–20 policies + a
  control-mapping register + an evidence-collection
  manifest. Compliance-automation tools (Vanta / Drata
  / Secureframe / Sprinto / Thoropass) generally earn
  their keep at founder scale.
- The evidence-collection cadence built during Type I
  readiness *is* the cadence the Type II observation
  window will look for. Build it as a ritual on the
  calendar and the on-call rotation.
- Type II timing is planned backward from the customer
  commitment; the 6-month observation window is the
  load-bearing constraint. Type I readiness starts
  8–16 weeks before the observation window starts.
- Auditor selection is a distinct decision from
  compliance-tool selection; enterprise-buyer
  reputation, tool-integration, startup-scale pricing,
  and a pre-audit readiness review are the criteria
  that matter.

The exercise for this chapter —
`exercise-02-soc-2-type-i-readiness-checklist.md` —
walks the scope selection, the ISMS shape, and the
evidence cadence for your own startup.
