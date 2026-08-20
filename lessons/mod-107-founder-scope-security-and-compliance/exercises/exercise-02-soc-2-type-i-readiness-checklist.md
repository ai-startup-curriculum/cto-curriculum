# Exercise 02 — SOC 2 Type I Readiness Checklist

**Module:** `mod-107-founder-scope-security-and-compliance`
**Planned time:** ~3 hours
**Chapter this builds on:** [`02-soc-2-type-i-readiness.md`](../02-soc-2-type-i-readiness.md),
supported by [`03-iso-27001-international-signal.md`](../03-iso-27001-international-signal.md)
for the ISMS composition, and by
[`mod-106` chapter 07](../../mod-106-scaling-org-and-stack/07-delivery-cadence-and-on-call.md)
for the incident-response substrate the SOC 2 IR
control lands on.

## Problem statement

Author the **SOC 2 Type I readiness checklist** for
your startup. The checklist is the single artifact
that answers *"where are we against SOC 2 Type I,
what remains, and by when?"* — for the CTO, for the
CEO, for the compliance-automation vendor, and for
the auditor at the pre-audit readiness review.

The point of the drill is not to *complete* the
readiness (that is the multi-week programme the
checklist scopes). The point is to force yourself to
(a) pick a defensible scope across the five Trust
Services Criteria, (b) sketch the small-team ISMS
shape, (c) design the evidence-collection cadence
that becomes the Type II observation window, and
(d) plan the Type I → Type II timeline backward from
your first credible customer commitment.

## Requirements

Author a Markdown document at
`docs/compliance/soc2-readiness.md` (or the
equivalent in your working repo).

### Section 1 — Scope selection (300-500 words)

- Which of the five Trust Services Criteria you
  include (Security is mandatory; Availability,
  Processing Integrity, Confidentiality, Privacy are
  optional). Cite chapter 02's scope-selection
  sentence and justify each optional criterion by a
  specific customer or regulatory driver — or
  explicitly rule it out.
- The system boundary — which product(s), which
  environment(s), which supporting business
  functions. One paragraph.
- Whether you are also pursuing ISO/IEC 27001
  concurrently or sequentially, and why (chapter
  03).
- Whether Type II follows Type I in a specific
  timeline (see Section 5 below).

### Section 2 — The ISMS document set

A table listing each policy from chapter 02's
small-team ISMS shape (15 policies), plus any
additional policies your context requires. Columns:

- Policy name.
- Status — Exists / Draft / Not yet.
- Owner — CTO, VP Eng, CEO, contractor.
- Target adoption date.
- Storage location (link or path).

Every policy that does not yet exist must have an
owner and a target date.

### Section 3 — The control-mapping register (spreadsheet or table)

A table with one row per SOC 2 Common Criteria
(CC1.1 through CC9.2 — the Common Criteria; add
Availability A1.1–A1.3, Confidentiality C1.1–C1.2,
etc., only for criteria in scope from Section 1).
Columns:

- SOC 2 criterion (ID and short description).
- Policy that satisfies it (link to the policy from
  Section 2).
- Evidence artifact(s) — the specific artifact that
  proves the control operates (e.g., *"AWS
  CloudTrail logs stored in S3 with 12-month
  retention"*, *"Quarterly access review recorded
  in `access-reviews/YYYY-QN.md`"*).
- Evidence collection cadence (daily / weekly /
  monthly / quarterly / annual).
- Status — Implemented / Partial / Gap.
- Owner and target close date for Partial / Gap.

You do not need to author the full 60+ rows of the
Common Criteria in this drill; a minimum of 20 rows
covering CC5 (Control Activities), CC6 (Logical and
Physical Access), CC7 (System Operations), and CC8
(Change Management) is the drill target. The rest
extend the same format.

### Section 4 — The evidence-collection cadence

A cadence table from chapter 02, tailored to your
startup:

- Daily items (e.g., backup succeeded, MFA policy
  in effect).
- Weekly items (dependency-scan triage, on-call
  handover).
- Monthly items (access review, security-metric
  roll-up, vendor list update).
- Quarterly items (full user access review, sub-
  processor list re-confirmation, policy review
  rotation).
- Annual items (policy review, risk-assessment
  refresh, penetration test, SOC 2 audit).

Each item: what is captured, where it is stored, who
owns it, and what triggers a follow-up if it is
missed.

### Section 5 — The Type I → Type II timeline

The timing math from chapter 02, planned backward
from the first credible customer commitment:

- Customer commitment date (real or hypothetical) —
  the date by which the customer expects Type II.
- Observation window length (3 / 6 / 12 months —
  6 is the founder-scope default; justify any
  deviation).
- Observation window start date and end date.
- Type I report target date (before observation-
  window start).
- Type I readiness kickoff date (8–16 weeks
  before Type I audit).
- Auditor selection deadline (before Type I
  kickoff).
- Compliance-automation vendor selection deadline
  (before Type I kickoff).

If the math does not fit — the customer commitment
is sooner than the earliest defensible Type II —
name the honest response (shorter observation
window if the auditor allows; longer contract
runway if the customer allows; a Type I report as
an interim signal if neither).

### Section 6 — Auditor and compliance-automation-vendor selection

A short paragraph per selection (or per candidate):

- Auditor — three candidate CPA firms considered,
  with the enterprise-buyer reputation, tool-
  integration, startup-scale pricing, and pre-audit
  readiness review criteria from chapter 02. Pick
  one; explain the pick.
- Compliance-automation tool — Vanta / Drata /
  Secureframe / Sprinto / Thoropass / other. Which
  candidates were considered, which was picked, the
  build-vs-buy justification (chapter 03 of
  [`mod-103`](../../mod-103-build-vs-buy-and-platform-economics/README.md)).

## Starter guidance

- **Start with the AICPA Trust Services Criteria
  document itself.** The full text is at
  [aicpa-cima.com — Trust Services Criteria](https://www.aicpa-cima.com/resources/download/trust-services-criteria).
  Read the Common Criteria points-of-focus for CC5
  through CC9 before writing Section 3 — the
  auditor tests against the points of focus, not
  against your paraphrase.
- **Default to Security-only scope.** Adding
  optional criteria multiplies audit effort and
  ISMS depth. Every optional criterion must map to
  a specific customer or regulatory driver named in
  Section 1.
- **The 20-row minimum on Section 3 is enough for
  the drill's discipline.** The full register will
  extend to 60+ rows during actual readiness; the
  drill target is that the rows you *do* author
  are complete, evidenced, and honest about gaps.
- **The evidence cadence is a *ritual*, not a
  spreadsheet.** For each cadence item, name where
  it lands on the calendar or the on-call
  rotation. *"Monthly access review — first
  Monday of every month, on the CTO's calendar,
  30-minute recurring meeting"* is the format that
  survives.
- **The Type I → Type II math is the load-bearing
  discipline.** If the customer commitment does not
  survive contact with the observation-window
  reality, the compliance-vs-sales conversation has
  to happen now, not in month 11.
- **Auditor selection is not the compliance
  vendor's decision.** Ask three of your
  prospective enterprise customers *"whose SOC 2
  reports do you accept?"* before selecting an
  auditor. If your customers all use one buyer-
  side security tool that already ingests reports
  from specific auditors, that is a data point.
- **Vanta / Drata / Secureframe / Sprinto /
  Thoropass are similar at founder scope.** Pick
  on onboarding speed, auditor-integration list,
  and pricing model rather than feature depth. All
  of them will get you to Type I at founder
  scope.
- **If ISO/IEC 27001 is on the roadmap, name it in
  Section 1.** The composition-with-ISO from
  chapter 03 changes the ISMS shape (internal audit
  programme, management review, SoA), even if the
  audit itself is a year out.

## Acceptance criteria

Your drill output is complete when:

- The readiness checklist exists at
  `docs/compliance/soc2-readiness.md` and is no
  more than eight pages when rendered (or a short
  memo pointing at the register spreadsheet if
  Section 3 is externalised).
- Section 1 makes the scope call across the five
  TSC with a specific justification per optional
  criterion.
- Section 2 lists every policy from chapter 02's
  ISMS with owner and target date; every gap has
  a plan.
- Section 3 covers at least 20 SOC 2 rows across
  CC5 / CC6 / CC7 / CC8, with evidence artifact,
  cadence, and gap-status per row.
- Section 4 turns the cadence into calendar / on-
  call rotation items with ownership and missed-
  item triggers.
- Section 5 does the Type I → Type II math
  backward from a concrete customer commitment
  and identifies the honest response if the math
  does not fit.
- Section 6 names a picked auditor and a picked
  compliance-automation tool with the selection
  criteria applied.
- The checklist can be handed to a compliance-
  automation vendor's onboarding engineer or a
  prospective auditor, and they can read it in
  20 minutes and name the top three gaps.

## What this feeds into

- **Exercise 01 — Section 3** — this exercise
  turns the *"SOC 2"* clause of the posture memo
  into a full plan.
- **Exercise 03 — DPA and privacy notice** — the
  processor RoPA feeds SOC 2 CC9.2 (vendor
  management) evidence.
- **Exercise 06 — SLSA baseline** — SLSA Build L2
  posture is one line of the SOC 2 CC8 (change
  management) evidence.
- **Exercise 07 — vendor DPA / BAA** — the vendor
  compliance inventory is the SOC 2 CC9.2
  evidence.
- **The module lab** consolidates this readiness
  checklist with the other exercise outputs into a
  `docs/compliance/` sub-tree.
- **Capstone
  [`project-102`](../../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package)**
  extends the readiness checklist into the SOC 2
  Type I scope-and-readiness document that is the
  first deliverable of the project.
