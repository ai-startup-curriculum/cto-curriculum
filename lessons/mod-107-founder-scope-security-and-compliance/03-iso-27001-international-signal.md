# ISO/IEC 27001:2022 — The International-Buyer Signal

> "SOC 2 is the report North American buyers ask for.
> ISO/IEC 27001 is the certificate everyone else asks for.
> The overlap is real; the two are not
> interchangeable." — the vocabulary discipline this
> chapter is written around.

## Motivation

A US-headquartered SaaS startup with a mostly-US
customer base can generally close enterprise deals with
a SOC 2 report alone. The moment the customer base
tilts European, Asian, or public-sector-international,
the procurement questionnaire changes. The question
stops being *"send us your SOC 2"* and becomes *"send
us your ISO/IEC 27001 certificate"*.

The two artifacts are similar in spirit — both attest
to a documented information-security management system
— and different in shape. SOC 2 is a US-CPA
attestation with a report as the artifact. ISO/IEC
27001 is an accredited-certification-body certification
against an international standard, with a certificate
and a Statement of Applicability as the artifacts. This
chapter walks the shape of ISO/IEC 27001:2022 as it
applies to a founder-scope SaaS, and answers the *when
to pursue it* question against a specific customer
base.

## What ISO/IEC 27001 actually is

ISO/IEC 27001 is an international standard published
jointly by the International Organization for
Standardization (ISO) and the International
Electrotechnical Commission (IEC). The current revision
is **ISO/IEC 27001:2022** — see the standard page at
[iso.org/standard/27001](https://www.iso.org/standard/27001).
The full text is behind an ISO paywall; the abstract
and scope are free, and the companion guidance
standard ISO/IEC 27002:2022 —
[iso.org/standard/75652](https://www.iso.org/standard/75652.html) —
walks the Annex A control set.

Four properties matter for founder scope:

- **It is a certification, not an attestation.** An
  accredited certification body (a CB, itself
  accredited by a national body such as UKAS in the
  UK, ANAB in the US, DAkkS in Germany) audits your
  organisation and issues a certificate stating that
  your ISMS conforms to the standard. The certificate
  is the customer-facing artifact.
- **The scope is defined by *you*.** Unlike SOC 2,
  where the *system* is the natural scope, ISO/IEC
  27001 requires you to explicitly declare the
  boundary of the ISMS — usually *"the SaaS product
  and all supporting business functions of [company]"*.
- **The audit runs on a three-year certification
  cycle.** Year 1 is the initial certification audit
  (Stage 1 documentation review, Stage 2 controls
  audit). Years 2 and 3 are surveillance audits.
  Year 4 is a recertification audit that restarts the
  cycle.
- **The 2022 revision aligns the Annex A control set
  with ISO/IEC 27002:2022.** The Annex A control
  count dropped from 114 (in the 2013 revision) to
  **93 controls in four themes** — Organisational
  (37 controls), People (8), Physical (14), and
  Technological (34). Older references to "Annex A
  114 controls in 14 domains" describe the 2013
  edition and are out of date.

The load-bearing consequence: the ISO/IEC 27001
programme is *more work than SOC 2* in the initial
year, because the standard's clauses (4 through 10 —
context, leadership, planning, support, operation,
performance evaluation, improvement) require a
top-down management-system posture that SOC 2 permits
but does not require. In the *steady state*, the
maintenance cost is comparable.

## The ISMS structure — clauses 4 through 10

The ISO/IEC 27001 clauses 4–10 define the management-
system substrate. The founder-scope translation of
each clause:

- **Clause 4 — Context of the organisation.** Document
  the internal and external issues that affect the
  ISMS (product shape, regulatory landscape, customer
  base, competitive posture) and the interested
  parties (customers, employees, investors,
  regulators, sub-processors). One or two pages.
- **Clause 5 — Leadership.** The information-security
  policy (a top-level document — usually the same
  policy that heads the SOC 2 ISMS from chapter 02),
  the assignment of information-security roles and
  responsibilities (at founder scope, the CTO is the
  information-security manager; the CEO owns
  top-management commitment). One or two pages plus
  a role assignment matrix.
- **Clause 6 — Planning.** The risk assessment
  methodology, the risk-treatment plan, the ISMS
  objectives, the Statement of Applicability (SoA —
  see the next section). This is the most content-
  heavy clause; the SoA alone is 20–50 pages of
  control-by-control notes.
- **Clause 7 — Support.** Resources (budget and
  headcount for the ISMS), competence (training and
  awareness), documented information (the ISMS
  document set from chapter 02, plus the ISO-specific
  additions in this clause).
- **Clause 8 — Operation.** Operational planning and
  control, risk-assessment execution, risk-treatment
  execution. This is where the controls are actually
  operated — the day-to-day work the evidence-
  collection cadence from chapter 02 captures.
- **Clause 9 — Performance evaluation.** Monitoring
  and measurement (security metrics), internal audit
  (a lightweight founder-scope internal-audit
  programme that reviews the ISMS quarterly),
  management review (a semi-annual CTO / CEO review of
  the ISMS performance).
- **Clause 10 — Improvement.** Nonconformity and
  corrective-action process (how findings are logged,
  root-cause-analysed, and closed), continual
  improvement.

The two artifacts that most distinguish an ISO/IEC
27001 ISMS from a SOC 2 ISMS are the **internal-audit
programme** (Clause 9.2) and the **management review**
(Clause 9.3). SOC 2 will accept a lighter approach to
both; ISO/IEC 27001 requires that they exist as
scheduled activities with documented outputs.

## The Statement of Applicability (SoA)

The Statement of Applicability is the single most
important ISO/IEC 27001 artifact. It is a table with
one row per Annex A control (93 rows in the 2022
edition), and columns:

- **Control reference** — e.g., A.5.1 *Policies for
  information security*.
- **Applicability** — Applicable / Not Applicable.
- **Justification** — one paragraph on *why* the
  control is applicable or not. If Not Applicable, the
  reasoning must be defensible (e.g., *"A.7.4 Physical
  security monitoring — Not Applicable. The
  organisation operates in cloud environments only
  and has no physical premises housing production
  systems; physical security is inherited from the
  cloud provider's own ISO/IEC 27001 certification"*).
- **Implementation status** — Implemented / Partially
  implemented / Planned.
- **Implementation description** — brief description
  of *how* the control is implemented, and where the
  evidence lives.
- **Reference to policy or procedure** — the ISMS
  document that documents the control.

The SoA doubles as the founder-scope **risk register**
because every control's applicability and
implementation status implicitly encodes a risk
decision. Most founder-scope startups can defensibly
mark a subset of the 93 controls as Not Applicable —
common examples include controls that assume physical
premises, controls that assume a large development
team, controls that assume specific regulated
industries. Do not over-defer; the credibility of the
SoA depends on the depth of the justification, not on
how many controls you can strike off.

## The Annex A control set (2022 edition, four themes)

ISO/IEC 27002:2022
([iso.org/standard/75652](https://www.iso.org/standard/75652.html))
groups the 93 Annex A controls into four themes. A
founder-scope walkthrough of each:

- **Organisational controls (37 controls, A.5.1–A.5.37).**
  Governance, policies, roles, threat intelligence,
  supplier relationships, information-security
  incident management, information-security aspects of
  business-continuity management, compliance with
  legal / statutory / regulatory obligations. Most
  overlap with SOC 2 CC1 / CC2 / CC9.
- **People controls (8 controls, A.6.1–A.6.8).**
  Screening, terms of employment, information-security
  awareness / education / training, disciplinary
  process, remote working, information-security event
  reporting. Overlap with SOC 2 CC1 and HR practice.
- **Physical controls (14 controls, A.7.1–A.7.14).**
  Physical security perimeters, entry controls,
  cabling security, equipment maintenance. Mostly
  inherited from the cloud provider at founder scope;
  the founder-scope SoA marks most of these as
  inherited-from-cloud-provider with a citation to the
  cloud provider's own certification (AWS, GCP, Azure
  all publish ISO/IEC 27001 certificates — see
  [aws.amazon.com/compliance/iso-27001-faqs](https://aws.amazon.com/compliance/iso-27001-faqs/),
  [cloud.google.com/security/compliance/iso-27001](https://cloud.google.com/security/compliance/iso-27001),
  [servicetrust.microsoft.com](https://servicetrust.microsoft.com/)).
- **Technological controls (34 controls, A.8.1–A.8.34).**
  User endpoint devices, privileged access rights,
  information access restriction, source code
  protection, secure authentication, capacity
  management, protection against malware, technical
  vulnerabilities, information backup, logging,
  monitoring activities, clock synchronisation,
  installation of software on operational systems,
  networks security, security of network services,
  segregation in networks, web filtering, use of
  cryptography, secure development lifecycle,
  application security requirements, secure system
  architecture, secure coding, security testing in
  development, outsourced development, separation of
  development and production, change management, test
  information, protection of information systems
  during audit testing. Overlap with SOC 2 CC6 / CC7
  / CC8.

The 2022 revision introduced **11 new controls** —
notably A.5.7 (Threat intelligence), A.5.23
(Information security for use of cloud services),
A.5.30 (ICT readiness for business continuity), A.7.4
(Physical security monitoring), A.8.9 (Configuration
management), A.8.10 (Information deletion), A.8.11
(Data masking), A.8.12 (Data leakage prevention),
A.8.16 (Monitoring activities), A.8.23 (Web filtering),
and A.8.28 (Secure coding). Founder-scope teams should
be prepared to justify each of these against their
architecture; several (A.5.23, A.8.9, A.8.28) are
straightforward in a modern cloud-native SaaS.

## When to pursue ISO/IEC 27001

The three founder-scope triggers, in decreasing order
of urgency:

- **A specific customer explicitly requires it.** A
  European enterprise, a UK financial services firm, a
  Japanese conglomerate, or a public-sector buyer
  saying *"we require ISO/IEC 27001"* is the fastest
  path to committing to the programme. Do the math
  the same way as SOC 2 Type II timing (chapter 02) —
  Stage 1 audit → Stage 2 audit is typically 3–4
  months, and each stage requires a prepared ISMS.
- **The account base tilts EU-heavy.** If more than
  20–30% of your enterprise pipeline is EU-domiciled,
  SOC 2 alone will start losing deals. The exact
  threshold depends on vertical (regulated verticals
  demand ISO/IEC 27001 sooner). Pursue ISO/IEC 27001
  when a repeated pattern of EU-buyer *"do you also
  have ISO 27001?"* questions emerges — three or four
  is a signal, not a coincidence.
- **You have completed SOC 2 Type II and want to
  extend the compliance moat.** Once SOC 2 Type II is
  in place, most of the ISMS substrate already
  exists — clauses 4–10 map to work you have already
  done; the SoA is where the incremental effort goes.
  This is the least-cost path to ISO/IEC 27001
  certification.

The two anti-patterns to avoid:

- **Pursuing ISO/IEC 27001 *before* SOC 2 without a
  specific EU driver.** For a US-headquartered SaaS
  with a mostly-US enterprise pipeline, SOC 2 is the
  higher-signal-per-dollar artifact. Pursuing ISO/IEC
  27001 first delays the SOC 2 report every US
  procurement team is expecting.
- **Pursuing *both* simultaneously with a single
  compliance-automation tool as the "unified answer".**
  The tool integrations are real, but each certification
  requires distinct auditor engagement and distinct
  evidence. A parallel-pursuit programme is closer to
  1.6× the cost of a sequential one, not 1.0×.

## The composition with SOC 2

The two frameworks compose well. The overlap:

- **Policy set.** The 12–20 policies from chapter 02
  cover almost all of the ISO/IEC 27001 Clause 5.2
  and Clause 7.5 documented-information requirements.
- **Access control, change management, incident
  response, vulnerability management, vendor risk.**
  SOC 2 CC5 / CC6 / CC7 / CC8 / CC9 controls line
  up almost 1:1 with Annex A organisational and
  technological controls.
- **Evidence-collection cadence.** The cadence built
  for Type II observation-window works directly for
  ISO/IEC 27001 surveillance audits.

The delta from SOC 2 to ISO/IEC 27001:

- **Clauses 4–10 management-system posture** — the
  formalisation of context, leadership, planning,
  performance evaluation, and improvement as
  scheduled processes with documented outputs. SOC 2
  will accept much of this in a lighter form.
- **Statement of Applicability** — the SoA is unique
  to ISO/IEC 27001. There is no direct SOC 2
  equivalent.
- **Internal-audit programme** — SOC 2 does not
  require a formal internal-audit function; ISO/IEC
  27001 does (Clause 9.2).
- **Management review** — SOC 2 does not require a
  formal management review; ISO/IEC 27001 does
  (Clause 9.3).
- **Certification body relationship** — a CB
  relationship is a distinct commercial engagement
  from the CPA firm relationship for SOC 2.

The founder-scope discipline: do not pursue ISO/IEC
27001 *first* unless a specific driver requires it. If
the trigger is *"we want the international-buyer
signal"* without a specific customer, sequence SOC 2
Type I → Type II → ISO/IEC 27001. If the trigger is
*"a specific EU customer requires it in month 12"*,
plan backward from that date the same way chapter 02
plans backward from a Type II customer deadline.

## Summary

- ISO/IEC 27001:2022 is an international-standard
  certification (not an attestation); a certificate
  from an accredited certification body is the
  artifact.
- The management-system clauses (4–10) require a
  top-down posture — context, leadership, planning,
  support, operation, performance evaluation,
  improvement — that SOC 2 permits but does not
  require.
- The **Statement of Applicability** is the load-
  bearing artifact — one row per Annex A control (93
  in the 2022 edition), with applicability,
  justification, implementation status, and evidence
  reference per row. The SoA doubles as the founder-
  scope risk register.
- The 2022 revision groups Annex A into four themes —
  Organisational (37), People (8), Physical (14),
  Technological (34) — and adds 11 new controls
  reflecting cloud, threat intelligence, secure
  coding, and data-protection practice.
- Pursue ISO/IEC 27001 when (a) a specific customer
  requires it, (b) the account base is EU-heavy
  enough to see repeated procurement questions, or
  (c) SOC 2 Type II is done and you are extending
  the compliance moat. Do not pursue it first unless
  a specific driver requires it.
- Composition with SOC 2 is high-overlap; the delta
  is Clauses 4–10 posture, the SoA, the internal-
  audit programme, and the management review.

The exercise for this module aggregates ISO/IEC 27001
readiness into the SOC 2 readiness checklist (exercise
02) rather than being called out as a separate
exercise — the founder-scope discipline is *scope
selection*, and ISO/IEC 27001 is one column in that
scope decision. If your context requires an ISO/IEC
27001-first programme, the exercise 02 template
extends directly.
