# Boundaries to `founder-ceo-curriculum` and `startup-exit-curriculum`

> "The CTO does not raise the round and does not
> negotiate the acquisition. The CTO produces the
> defensible technical package that lets the CEO
> raise the round and negotiate the acquisition
> from a stronger position." — the framing this
> chapter is organised around.

## Motivation

This module has walked six pieces of engineering-
leadership craft: a synchronised decision cadence
with the CEO, a cofounder-dispute mechanic, a board
pre-read, a technical-DD data room, a hostile-DD
response reflex, and the risk-engineering slice of a
board-ready narrative. All six sit *underneath* two
related but separately-owned disciplines that are
outside the scope of this track:

- **Deep CEO-craft** — the construction of a
  fundraising narrative, the ongoing management of
  the board as CEO, the hiring of executives, and
  the strategic allocation of capital. This is the
  domain of
  [`founder-ceo-curriculum`](https://github.com/ai-startup-curriculum/founder-ceo-curriculum),
  and the CTO consumes its outputs rather than
  authoring them.
- **Deep M&A and integration craft** — running the
  full acquisition sale process, negotiating LOI
  and definitive-agreement terms, structuring
  earn-outs and escrows, secondary-transaction
  design, and post-close integration planning.
  This is the domain of `startup-exit-curriculum`
  at level 40 in the shared curriculum ladder, and
  is a stage beyond the pre-seed → Series-A
  scope this track owns.

This chapter names the boundary in each direction —
what the CTO *does* own at those interfaces, and
what belongs to the peer track.

## The boundary to `founder-ceo-curriculum`

The founder-CEO track owns the CEO seat: the
construction and evolution of the fundraising
narrative, the direct relationship with the board
as the primary board-communication channel, the
hiring of the executive team, and the allocation
of capital across the business. The CTO's role at
each of those interfaces is well-defined and
specifically bounded.

### Fundraising narrative construction

The fundraising narrative — the *"what is this
company becoming, and why now"* story the CEO
uses with investors — is authored by the CEO.
The CTO consumes it: every commitment in the
board pre-read (chapter 03) is tied to the
narrative, every risk in the register (chapter 06)
is framed against the narrative, every DD-data-
room artifact (chapter 04) supports the
narrative.

The CTO's role at the narrative interface:

- **Serve the narrative with technical
  commitments and their evidence.** SAML SSO for
  an enterprise-narrative company; SOC 2 Type II
  for a regulated-buyer narrative; multi-region
  posture for an international-narrative company.
  Each is a technical deliverable that makes the
  narrative real.
- **Flag when a technical decision *changes* the
  narrative.** A decision to build a bespoke
  inference stack rather than depend on a
  foundation-model provider changes the *"what
  are we"* answer. A decision to standardise on
  a specific cloud region for EU data residency
  changes the *"who can we sell to"* answer.
  Chapter 03 walks the narrative-tie discipline
  in the board pre-read; the same discipline
  applies in the fundraising narrative.
- **Do not author the narrative itself.** The
  fundraising narrative synthesises market
  positioning, product roadmap, competitive
  landscape, financial model, and technical
  posture. Only one of those five is the CTO's
  primary craft; authoring the whole is the
  CEO's job.

`founder-ceo-curriculum` walks the narrative-
construction craft in depth: narrative arc,
positioning language, investor psychology, round-
sizing, and pitch-deck construction. The CTO who
wants to be a *better consumer* of the narrative —
a better serving partner to the CEO — reads that
track. The CTO who tries to *become* the CEO's
narrative primary is stepping outside the seat.

### Board management as CEO

The CEO owns the ongoing relationship with the
board — meeting cadence, individual director
1:1s between meetings, the composition of the
board (adding independent directors, adding
investor-side directors at each round), and the
board's operating norms.

The CTO's role:

- **Attend the board meeting** and present the
  technical section of the pre-read (chapter 03).
- **Take direct 1:1 briefs** with the lead
  director or the board's DD-liaison director
  before any material board-escalation item
  (chapter 03's no-surprises rule).
- **Route board-composition questions to the
  CEO.** The CTO may have views on adding an
  independent director with a specific
  background (a former CTO of a similar-stage
  company, a specialist in a regulated-domain
  compliance posture); those views go to the
  CEO in the 1:1, not directly to the board.
- **Do not develop parallel narratives.** Board
  members who receive different stories from
  the CEO and the CTO between board meetings
  lose confidence in both founders. Every
  board-directed communication from the CTO
  goes through, or is briefed to, the CEO.

`founder-ceo-curriculum` walks board-management
craft as CEO in depth: board recruiting, meeting
design, director relationships, and the mechanics
of raising a fundraise from an existing board.

### Executive hiring

The founding team's first executive hires — VP
Engineering, VP Product, Head of Sales, CFO,
Head of Marketing — are joint decisions between
CEO and CTO with the map from chapter 01 (they
sit in the consensus column for all but VP
Engineering, which the CTO leads with CEO consent,
and Head of Product / Sales, which the CEO leads
with CTO consent). The board is a distribution
channel for candidates (chapter 03, Section 3 of
the pre-read).

The CTO owns:

- **The technical-executive loops** — VP
  Engineering, Head of Product where technical,
  and any specialist-domain roles (Head of AI,
  Head of Infrastructure, Head of Security).
  Loop design, panel composition, technical
  interview rubric, and reference-check
  discipline for these roles live here.
- **The technical review of candidates for
  non-technical roles.** The CTO participates in
  the interview loops for the first Head of
  Sales, first CFO, first CS lead — the
  technical-fluency screen and the *"can they
  work with engineering"* screen live with the
  CTO.

The CTO does not own the compensation-band
design, the equity-refresh policy, the executive-
onboarding programme, or the executive-team
operating cadence. Those are CEO / People-Ops
functions that `founder-ceo-curriculum` and
`startup-operations-governance-curriculum` walk in
depth.

### Capital allocation

The CEO — with the board — is the primary
capital-allocation decision-maker. The founder-
CEO track walks the discipline in depth:
runway-driven planning, headcount-vs-revenue-
efficient allocation, the go-to-market vs.
product-engineering spend ratio, and the
build-vs-fund-a-vendor decisions at each stage.

The CTO's role at this interface:

- **Own the engineering-org spend proposal** —
  headcount plan, tooling and cloud spend, and
  any specialist-domain investment (a compliance
  auditor, a pen-test provider, a foundation-
  model commitment). The proposal is briefed at
  the annual planning cycle and re-baselined at
  material re-plans.
- **Own the *cost-to-carry* estimates for
  technical-debt items** from
  [`mod-105`](../mod-105-technical-debt-as-business-decision/README.md).
  The CEO cannot make an allocation decision
  between a new hire, a new market, and a
  refactor without the refactor's cost-to-carry
  in the mix.
- **Own the *build-vs-buy* recommendations**
  from
  [`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md)
  at the material threshold — any decision above
  the consensus-column threshold in the map from
  chapter 01.

Everything else — corporate-treasury policy,
runway-management, the fundraise sizing, and the
board's capital-allocation dashboard — lives with
the CEO and the finance track.

## The boundary to `startup-exit-curriculum` (level 40)

`startup-exit-curriculum` at level 40 in the
shared curriculum ladder is the deep track for
M&A, integration planning, and secondary-
transaction depth. The founder-scope CTO
consumes it (as a founder navigating an
acquisition offer) and cites it (as a peer
role-track); the CTO does not author its
deliverables.

The specific interfaces the CTO owns are inside
the scope of this module; the deeper deliverables
belong to the level-40 track.

### What lives here

- **The DD data room** (chapter 04). The six-
  folder scaffold, the running-artifact
  discipline, and the answers-file are load-
  bearing from Series-A onward. They are as
  useful for a Series-A round as for an
  acquisition and are owned by the CTO
  regardless of the transaction type.
- **The hostile-DD response reflex** (chapter
  05). The three-angle attack pattern
  (architectural risk, key-person risk, hidden
  compliance debt) and the *"don't argue,
  produce the artifact"* reflex are craft the
  CTO practices whether the counterparty is an
  investor or an acquirer.
- **The board-ready risk narrative** (chapter
  06). The three-class filter and the narrative
  arc are used for every board meeting; they
  are not acquisition-specific.

### What lives in `startup-exit-curriculum`

- **The full acquisition sale-process**
  playbook — banker selection, buyer
  identification, teaser and CIM design, indication-
  of-interest management, and the mechanics of
  running a competitive process.
- **LOI and definitive-agreement negotiation** —
  representations and warranties, indemnification
  caps, escrow structure, earn-out design, the
  interaction between the transaction agreement
  and the founding-team vesting instruments.
- **Post-close integration planning** —
  organisational integration, system-integration
  planning, customer-migration playbooks, and
  the mechanics of the first 100 days as an
  acquired company.
- **Secondary-transaction design** — the
  founders'-liquidity mechanics in a secondary
  round or in a bolt-on to a primary round, and
  the interaction with the cap-table and the
  investors' pro-rata rights.
- **The full tax-and-structuring layer** —
  stock-vs-asset-sale, jurisdictional structure,
  the founders' personal-tax outcome across the
  possible deal structures. Every one of these
  is a legal / tax / structuring specialist
  question; the CTO does not decide these and
  the `startup-exit-curriculum` track routes to
  the specialist counsel.

The CTO in an active acquisition process consumes
`startup-exit-curriculum` outputs — the CEO or an
outside advisor briefs the CTO on the sale-process
plan and the transaction-agreement structure, and
the CTO participates in the technical-DD sessions
(chapters 04, 05) and the board-communication
around the transaction (chapters 03, 06). The
depth of the sale-process and the transaction-
agreement design belongs to the deeper track.

## The composed view — one CTO, three cited tracks

The CTO seat this curriculum trains for sits at
the intersection of three peer tracks, each with
its own primary owner:

- **`founder-ceo-curriculum`** owns deep CEO
  craft — fundraising narrative, board management
  as CEO, exec hiring, capital allocation. The
  CTO consumes and serves.
- **`startup-exit-curriculum`** (level 40) owns
  deep M&A, integration, and secondary-
  transaction craft. The CTO consumes and
  participates in the technical slice.
- **The engineering-family higher-level tracks
  cited across the module** —
  [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (level 30) for day-two engineering-management
  craft;
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) for deeper architectural craft;
  [`chief-ai-officer`](../../../chief-ai-officer-learning)
  (level 70) for C-suite AI-org scope — own the
  engineering-craft depth beyond the founder-
  scope this track covers.

The CTO's discipline is to know where each depth
lives, cite it correctly, and consume its
outputs rather than duplicating them badly. Every
one of the six previous chapters names its
boundary explicitly for that reason.

## Summary

- Deep **CEO craft** — fundraising narrative
  construction, board management as CEO,
  executive hiring, capital allocation — lives
  in
  [`founder-ceo-curriculum`](https://github.com/ai-startup-curriculum/founder-ceo-curriculum).
  The CTO *serves* the narrative, participates in
  board management as the technical seat next to
  the CEO, co-owns technical-executive hiring,
  and owns the engineering-spend proposal that
  feeds capital-allocation decisions.
- Deep **M&A, integration, and secondary-
  transaction craft** lives in
  `startup-exit-curriculum` at level 40. The
  CTO owns the technical-DD data room (chapter
  04), the hostile-DD response reflex (chapter
  05), and the board-communication around the
  transaction; the sale process, transaction-
  agreement design, integration planning, and
  secondary-transaction design belong to the
  deeper track.
- The **composed view** — the CTO seat sits at
  the intersection of the founder-CEO,
  startup-exit, and engineering-family tracks,
  consuming from each and citing the boundary
  in every chapter of this module.

This chapter closes the module. The next step is
the module lab and capstone
[`project-103`](../../projects/project-103-scaling-plan-from-five-to-fifty-engineers)
— where the artifacts produced by the six
exercises are consolidated and *presented* to a
board or an investor in the vehicle the six
chapters have built.
