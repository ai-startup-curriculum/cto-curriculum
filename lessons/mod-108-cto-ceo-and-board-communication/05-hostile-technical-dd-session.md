# The Hostile Technical DD Session — When the Buyer Is Hunting for a Discount

> "The DD lead who is hunting for a discount is not
> your adversary. They are a professional doing
> their job. Your job is to have already produced
> the artifact that answers their question before
> they walk into the room." — the framing this
> chapter is organised around.

## Motivation

Not every technical due-diligence session is
adversarial. A friendly Series-B lead who has already
priced the round and is confirming the story runs a
relatively cooperative process. A strategic acquirer
who wants the deal at the LOI price does the same.

Some sessions are not those. A price-driven acquirer,
a competitive Series-B where the price is contested,
or a strategic buyer looking for a reason to walk from
an over-priced LOI runs a *hostile* technical DD
session — one where the buyer's technical DD lead is
specifically looking for architectural risk, key-
person risk, or hidden compliance debt they can use to
justify a discount, a price adjustment, or a walk-away.

This is not a failure of the process. It is the process
working as designed. The buyer's job is to bound their
risk; hostile DD is one of the tools by which they do
it. The CTO's job is not to *defuse* the hostility —
that is a category error — but to have already
produced the artifact that pre-empts each of the three
angles the hostile DD lead is trained to attack from.

This chapter names those three angles, the specific
questions each produces, and the evidence artifacts
that neutralise each.

## The three angles a hostile technical DD lead attacks from

A trained technical DD lead — from a large PE house, a
strategic-acquirer corp-dev function, or a late-stage
VC — has three main levers to reduce a price. Every
question in the hostile session is designed to open
one of these three:

- **Architectural risk.** *"The system will not scale
  to our customer base."* / *"The architecture is
  brittle to their next scaling milestone."* / *"We
  will have to rewrite a load-bearing piece within
  the first year."* Each of these justifies a price
  discount sized to the cost-to-carry of the
  identified debt.
- **Key-person risk.** *"The system's ability to
  function depends on a small named list of people
  whose retention we cannot guarantee."* / *"Loss of
  key persons X and Y post-close would take us more
  than 90 days to recover from."* This justifies
  retention pools carved out of the seller's
  proceeds, or an outright discount.
- **Hidden compliance debt.** *"The company has been
  operating with un-scoped compliance obligations
  that will cost us $N to remediate post-close."*
  / *"We cannot bound the regulatory exposure
  without a full compliance audit at our expense."*
  This justifies both a discount and an escrow.

Each of the three has a *pattern* — a specific set of
questions the DD lead will ask, in a specific order,
with a specific set of follow-ups they are trained to
push on. The pre-empting evidence for each is
predictable and can be produced *before* the session
rather than *during* it.

## Angle 1 — Architectural risk

The DD lead attacking this angle is looking for signs
that the current architecture will not survive the
buyer's post-close plan. The specific questions,
roughly in order:

- *"Walk me through the largest single component of
  the system that would need to be rewritten to
  support [buyer-scale] load."*
- *"What is your current unit economics per
  transaction / per tenant / per query? How does
  that curve change at 10× current volume?"*
- *"What is the largest single vendor / provider /
  dependency the system is bound to? What would it
  cost to switch off? How long would it take?"*
- *"Show me the deploys per week and the rollback
  rate. If they are low, why? If they are high,
  where does the noise come from?"*
- *"Show me the last three material outages and the
  post-mortems. What is the pattern?"*
- *"What is the largest known technical-debt item
  the team is carrying today, sized in
  engineer-months?"*

The pre-empting evidence — every one of these
artifacts already exists in the DD data room from
chapter 04 if the running-artifact discipline is
followed:

- **Unit-economics profile.** Concrete numbers on
  cost per tenant, per transaction, per model
  inference (for AI-native products), with the
  scaling curve to 10× the current volume plotted
  explicitly and the largest cost-optimisation
  levers named. This lives in folder 01 of the DD
  data room and refreshes quarterly with the board
  pre-read.
- **Rewrite / rearchitecture roadmap.** The 12-18
  month roadmap of architectural changes from
  folder 01, with each item classified as one-way
  door / two-way door (chapter 02 of mod-102's ADR
  discipline). The load-bearing property: the CTO
  has *already sized* the rewrites they know are
  coming and produced the estimates. The hostile
  DD lead's *"you will have to rewrite X"* becomes
  *"yes, X is on our 18-month roadmap for the
  following reason, sized at N engineer-months"* —
  a boring exchange, not a discount lever.
- **Dependency-cost analysis** for the top-5
  vendors. What each costs, what the switching cost
  would be, what the alternatives are, and what
  the current-vendor-lock exposure is. If a single
  vendor is load-bearing (foundation-model
  provider, cloud, database), the analysis names
  the exposure explicitly rather than hoping the
  DD lead misses it.
- **DORA four-key metrics** from
  [`mod-106` chapter 05](../mod-106-scaling-org-and-stack/05-dora-four-keys-as-signal.md)
  — deploy frequency, lead time for changes,
  change-failure rate, mean time to recover.
  Current numbers and 12-month trajectory. The
  hostile DD lead reading DORA metrics that place
  the team in the Elite or High DORA band moves
  from *hunting* to *confirming*.
- **The incident register and post-mortem library**
  from folder 05, with the pattern-analysis note
  the CTO wrote themselves — the specific classes
  of incident recurring, the specific investments
  underway to close each class, and the trajectory
  of each class over the last four quarters.
- **The technical-debt portfolio** from
  [`mod-105`](../mod-105-technical-debt-as-business-decision/README.md)
  — Fowler quadrants, cost-to-carry sizing per
  item, and the refactor-budget-versus-roadmap plan
  from that module. The DD lead's *"what is the
  largest technical debt item you're carrying"*
  becomes *"here is the portfolio, sized, with the
  budget attached to it"*.

The reflex — the load-bearing habit the CTO installs
before the session — is: *don't argue, produce the
artifact*. The hostile DD lead who receives the
pre-empting artifact before they finish their
question stops looking for the discount and starts
looking for the next question. The CTO who tries to
argue their way out of the finding without the
artifact hands the DD lead the discount.

## Angle 2 — Key-person risk

The DD lead attacking this angle is looking for named
people whose loss would materially harm the buyer's
ability to operate the acquired system. The specific
questions:

- *"Who is the single person who understands the
  most about the architecture? What is their
  vesting status? What is their retention
  posture?"*
- *"Which components of the system have a single
  named owner? What is the bus-factor for the
  top-5 components?"*
- *"Show me the last three departures from senior
  engineering. Voluntary or regretted?"*
- *"What retention plan do you have for the top-5
  engineers post-close?"*
- *"Which team members have alternative offers
  active today?"*

The pre-empting evidence:

- **The key-person register** from folder 04 of
  the DD data room. The CTO has *already named*
  the key persons — by role, not necessarily by
  name in the shared document — and *already
  attached* the specific mitigation to each
  (cross-training, documented runbooks, hiring in
  flight, retention grant, redundancy). The
  hostile DD lead reading the register does not
  discover key-person risk; they see the CTO's
  own bounded articulation of it and the
  mitigations underway.
- **Bus-factor analysis** per major component. For
  each of the top 5-10 components in the C4
  container diagram, the primary owner, the
  secondary owner, and (if bus-factor is 1) the
  named mitigation.
- **The retention-and-refresh posture.** The
  equity-refresh cadence for senior engineers, the
  retention-grant policy, any current retention-
  bonus commitments. This is a *company* posture
  that the CTO briefs on, not a per-person
  disclosure; the per-person disclosure is
  privileged and routed through counsel.
- **Departure history** with cause classification
  (regretted / non-regretted / performance /
  voluntary-for-external / restructure). Any
  pattern of regretted departures in a specific
  team is a *known* pattern the CTO can brief on,
  including the response.
- **Founders' own vesting and retention posture.**
  The single most-load-bearing key-person answer:
  what does the founder-CTO's own vesting look
  like, what does a post-close retention grant do
  to it, and is the founder committed to a
  post-close operating period. This is the answer
  the DD lead will ask directly; the CTO briefs
  the CEO and counsel before answering, but
  answers.

The reflex is the same: *don't argue, produce the
artifact*. The key-person register that names the
risks explicitly and the mitigations concretely
neutralises the *"we have discovered key-person
risk"* line in the DD memo.

## Angle 3 — Hidden compliance debt

The DD lead attacking this angle is looking for
regulatory or compliance obligations the company has
acquired without scoping. The specific questions:

- *"You have customer data in [jurisdiction]. What is
  your legal basis under [GDPR / CCPA / other]? Show
  me the RoPA."*
- *"You handle [PHI / financial / regulated] data.
  Show me the BAA / DPA chain."*
- *"You have a SOC 2 Type I. When does the Type II
  observation window complete? Show me the
  fieldwork status."*
- *"You use foundation-model providers. Show me the
  BAA / zero-retention posture per provider per
  data class."*
- *"Show me the incident history. Any of them
  triggered a regulator interaction? Any of them
  triggered a customer-notification clock that was
  missed?"*
- *"Show me the current sub-processor list and the
  DPA for each. When did each get signed?"*

The pre-empting evidence — again, all of it already
lives in mod-107's compliance package and folders 02
and 05 of the DD data room:

- **The one-page posture memo** from mod-107, with
  every deferral named explicitly and the *why
  deferrable* rationale attached (mod-107 chapter
  01's four founder-scope questions). The hostile
  DD lead reading *"we defer bug-bounty programme,
  formal threat modelling, SIEM, and DPO
  appointment until the first security hire in
  Q[N]; here is why each is deferrable at our
  scale"* has less to attack than one reading
  silence on the same items.
- **The compliance-obligation register.** Every
  compliance obligation the company has acquired
  since incorporation — through a customer
  contract, a jurisdiction, a data type, a
  vendor — and its scope-in status. Any un-scoped
  obligation is *named* here rather than hidden.
  The DD lead's *"we discovered un-scoped
  compliance debt"* becomes *"the register lists
  it, sized at N months of work, on the roadmap"*.
- **The RoPA (Article 30 records of processing
  activities)** from mod-107 chapter 04.
- **The BAA / DPA library** from mod-107 chapter
  08 for every vendor that touches regulated data.
- **The incident register with the notification-
  clock evidence.** For every incident that met a
  customer- or regulator-notification threshold,
  the evidence that the notification was made
  within the clock. Missed clocks are a
  discount-lever regardless; naming the miss and
  the remediation is materially better than the
  DD lead discovering the miss.
- **The current SOC 2 scope + timeline.** Not just
  the certificate — the observation-window plan,
  the gap-remediation status, and the customer
  commitments that anchor the timeline.

## When to escalate to the CEO

Some DD findings are technical questions with
technical answers; the CTO handles them in the room.
Others are *commercial* questions dressed in
technical clothing:

- The buyer is asking about a compliance gap that,
  even if remediated, changes the acquisition
  economics. The escalation is to the CEO and to
  counsel, not to a solutioning discussion in the
  room.
- The buyer is proposing a retention pool carved
  out of the seller's proceeds. The escalation is
  to the CEO and to the founders' counsel; the
  CTO does not negotiate the pool structure.
- The buyer is proposing an earn-out tied to
  post-close technical milestones. The escalation
  is to the CEO and to counsel; the CTO's job is
  to size the milestones honestly.
- The buyer has proposed a walk-away tied to a DD
  finding. The escalation is immediate — to the
  CEO in the next break, and (post-session) to
  the board's DD-liaison director. The founders
  respond together, not in-session.

The tell that the DD session has crossed the
technical / commercial line: the DD lead has
stopped asking questions and started proposing
terms. At that moment, the CTO's job is to *note
the shift* — *"that sounds like a question for
[CEO] and counsel; can we take it off the technical
DD agenda and route it to the commercial
discussion?"* — and to keep the technical DD
session on the technical DD agenda.

## The "don't argue, produce the artifact" reflex

The single most-important habit in the hostile DD
session is that every finding is met with an
artifact rather than a defence. Four failure modes
the reflex prevents:

- **Defensive posture.** The CTO who argues against
  the finding — *"that's not actually a risk
  because…"* — is heard as denying the finding.
  The CTO who says *"here is the artifact we
  produced against that risk"* is heard as bounding
  the finding.
- **Ad-hoc estimation.** The CTO who does the sizing
  live in the room — *"let me think, that would
  probably take about three engineer-months…"* —
  produces a number that the DD lead will hold to
  and that will typically be under-sized. The CTO
  who reads from the technical-debt portfolio (mod-
  105) produces a *bounded* number the buyer's team
  cannot argue with.
- **Discovered surprise.** The CTO who is genuinely
  surprised by a question — *"we hadn't considered
  that risk"* — signals to the DD lead that the
  risk is real *and* unbounded. The CTO who has a
  written answer, even if the answer is *"yes we
  know about that, here is the register entry"*,
  neutralises the surprise.
- **Cross-answer inconsistency.** Two DD leads at
  the same buyer, or the same DD lead across two
  sessions, receive inconsistent answers to the
  same question. The answers-file from chapter 04
  is the anchor. The CTO reads from the answers-
  file even when the question feels like it
  deserves a fresh answer, because the fresh answer
  will not match the record.

## The post-session discipline

Every hostile DD session — every DD session, actually —
gets a same-day retro:

- **Answers-file updates.** Any question the answers-
  file did not fully cover goes into the answers-
  file for the next session.
- **Artifact gaps.** Any DD-lead question that the
  data room did not have an artifact for becomes an
  action item for a new artifact (or a rejection
  with a written *why not*).
- **Escalations logged.** Any commercial-question-in-
  technical-clothing that was escalated to the CEO
  and counsel gets a written entry in the decision
  log.
- **CEO brief.** The CTO briefs the CEO on what was
  asked, what was answered, what was escalated, and
  what the DD lead's read on the answers seemed to
  be. This is the input to the commercial
  negotiation that runs in parallel.

## Summary

- The hostile technical DD session is a *professional*
  process where the buyer's DD lead is attacking
  from three angles: **architectural risk**, **key-
  person risk**, and **hidden compliance debt** — each
  to justify a specific discount or a walk-away.
- Every angle has a **predictable set of questions**
  and a **pre-empting evidence artifact** that
  already exists in the DD data room (chapter 04)
  and the mod-107 compliance package if the
  running-artifact discipline is followed.
- The **reflex** is *don't argue, produce the
  artifact*. Defensive posture, ad-hoc estimation,
  discovered surprise, and cross-answer
  inconsistency are the four failure modes the
  reflex prevents.
- **Commercial-questions-in-technical-clothing** —
  retention pools, earn-outs, walk-away triggers,
  materially-priced remediation — are escalated to
  the CEO and to counsel, not solved in the
  session.
- Every session gets a **same-day retro** — answers-
  file updates, artifact-gap action items,
  escalation log entries, and a CEO brief.

The exercise for this chapter —
`exercise-05-hostile-tech-dd-response-drill.md` —
runs the three-angle attack against your own DD data
room and produces the pre-empting evidence artifact
for each identified gap.
