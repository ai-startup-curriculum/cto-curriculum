# Org Chart, Career-Ladder v0, and Compensation Band — Artifacts That Survive Eighteen Months

> "You can't outsource your career ladder. If you don't
> write one, the hiring market writes one for you — one
> conversation at a time, in your Slack DMs, at the exit
> interview." — the honest version of a line the CTO who
> has been through the first calibration cycle will
> recognise; Camille Fournier's *The Manager's Path*
> ([oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/))
> is the canonical reading on why.

## Motivation

The three artifacts this chapter is about — the **org
chart**, the **career-ladder v0**, the **compensation
band** — are the paperwork that makes the earlier
decisions in this module real. They are also the
paperwork the CTO defers on for the longest, because
each of them looks premature at 5 engineers and
suddenly overdue at 15.

The correct time to author v0 of each is roughly *at
the trigger for the first EM* (see [`chapter 05`](05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md))
— which is also the point at which the org has
enough shape to make the artifacts meaningful and
not so much shape that retrofitting them is a
politically expensive rewrite.

Two failure modes are the reason CTOs put them off:

- **The "we're too small to need a ladder" reflex.** No
  ladder is a *ladder*: it's the implicit one every
  compensation and promotion conversation is
  triangulated against, invisibly, inconsistently, and
  in the founder's head. It routes on charisma and
  proximity to the CTO. It fails the first time an
  engineer asks the CTO to justify a compensation
  difference between two peers.
- **The "we'll copy the Google ladder" reflex.** The
  team downloads someone else's public engineering
  ladder ([progression.fyi](https://www.progression.fyi/)
  aggregates a good sample), pastes it into a Notion
  page, and calls it done. The result is a ladder
  written against a different company's problems, and
  the team learns fast that the ladder does not describe
  their actual work.

The correct v0 is written for *this* company at *this*
stage, borrows structure from public references without
inheriting their specifics, and is explicit about being
a v0 that will be re-written at the next stage
transition. The three artifacts are also the specific
hand-off surface to the peer-track owners
[`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
(day-two management craft) and
[`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum)
(People pillar — HR / people-ops / compensation
depth) — this chapter defines the CTO's ownership
line, and names what the CTO consumes from those
tracks rather than re-teaches.

## The org chart

The org chart at pre-Series-B scale is a **one-page
picture** — not an HR system export — that shows every
person in the engineering org, their role, their team
(per [`chapter 04`](04-team-topologies-at-startup-scale.md)),
and their reporting line. It is versioned in the same
repo as the ADR index and the build-vs-buy matrix; it
is re-read at every stage transition; it is legible to
a first-round investor's technical-DD reviewer.

The org chart carries:

- **Every current person** — name, role, team.
- **Every open requisition** — role, team, target start
  (from the hiring plan in chapter 01), a "TBD" name
  slot.
- **The reporting lines** — including the CTO's own
  direct reports, and any temporary reporting lines
  (an enabling engineer who reports to the CTO but is
  embedded with a stream-aligned team).
- **The team-type label** for each team — stream-
  aligned, platform, enabling, complicated-subsystem
  (per chapter 04).
- **The version and date** — the org chart is a
  living artifact. A chart without a version is one
  nobody trusts is current.

An org chart the size this module targets (5-25
engineers) fits on one landscape page. Do not use an
HR tool's org-chart export at this stage; the tool
optimises for a much larger org and the picture
becomes unreadable. A simple hand-drawn or Mermaid
diagram is the right density.

A minimum shape (Mermaid) for a 15-engineer org:

```
graph TD
  CEO --> CTO
  CTO --> EM1[EM — Acquisition]
  CTO --> TL1[Tech Lead — Enterprise]
  CTO --> ENAB[Enabling engineer — SRE / DevEx]
  EM1 --> A1[Senior FE]
  EM1 --> A2[Senior BE]
  EM1 --> A3[Full-stack]
  EM1 --> A4[Open req — full-stack]
  TL1 --> E1[Senior BE]
  TL1 --> E2[ML engineer]
  TL1 --> E3[Data engineer]
  TL1 --> E4[Open req — senior BE]
```

The diagram is not just a picture. It is the artifact
the CTO points at when the board asks "walk me through
your org", when an interviewing candidate asks "where
would I sit", and when a customer's technical due-
diligence team asks "who owns X".

### What the org chart is *not*

- **Not a title inventory.** Titles proliferate if the
  chart is the primary title-negotiation surface.
  Keep titles conservative at seed / Series-A stage.
- **Not the seniority ladder.** Seniority is on the
  career ladder (below); the org chart shows
  reporting and team, not level.
- **Not permanent.** Every stage transition (see
  [`mod-106`](../mod-106-scaling-org-and-stack/README.md))
  re-shapes the chart; the current chart is a snapshot,
  not a settlement.

## The career-ladder v0

The career ladder is the document that says, for each
role family (usually two: **engineering IC** and
**engineering management**), what each level
*is* — the scope, the impact, the behaviour, the
technical depth — and what it takes to move between
levels.

At seed / Series-A stage a workable v0 has **three or
four levels per track**, not the eight-plus levels a
Series-C+ ladder needs. Compression at v0 is a
feature: with 15 engineers you cannot meaningfully
distinguish four grades of "senior".

### The IC track — a workable v0

Four levels:

- **L1 — Engineer.** New-grad / early-career. Owns
  scoped tasks; ramp; makes correct small decisions
  and asks for help on larger ones.
- **L2 — Senior Engineer.** Owns features end-to-end;
  makes design decisions for a subsystem; mentors L1s;
  reliable on-call presence.
- **L3 — Staff Engineer.** Owns technical direction of
  a subsystem or a team's work; authors ADRs (see
  [`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md));
  mentors L2s; the Larson archetypes (Tech Lead,
  Architect, Solver, Right Hand) apply here — see
  [staffeng.com/book](https://staffeng.com/book).
- **L4 — Principal Engineer.** Cross-team technical
  scope; often paired with the CTO on the biggest
  architectural calls. At pre-Series-B most orgs have
  0-1 L4s; do not create the level unless there is a
  specific person the level describes.

### The EM track — a workable v0

Three levels at v0 (add more later):

- **M1 — Engineering Manager.** Manages a team of
  3-8 engineers; owns hiring, 1:1s, feedback,
  performance-management, delivery cadence, career
  conversations. Day-two craft owned by
  [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (level 30).
- **M2 — Senior Manager / Group EM.** Manages other
  managers or a very large IC team; owns cross-team
  planning, calibration, hiring at scale.
- **M3 — Director / VP Engineering.** Owns the
  engineering-org operating system (chapter 05); may
  or may not have EMs reporting.

### The per-level content

Each level entry has **four dimensions**, and each
dimension has **two-to-four short behavioural anchors**:

- **Scope.** How large is the surface this person owns?
  How ambiguous can the surface be?
- **Impact.** What is the size of the outcome this
  person is responsible for?
- **Behaviour.** How do they work with others?
  Mentoring, feedback, disagreement, collaboration?
- **Craft.** What is the technical depth expected
  (for IC) or the management craft expected (for EM)?

The v0 anchors are **specific to your company** — the
IC level 2 anchor for "makes design decisions for a
subsystem" should reference the actual subsystems the
team has, not the generic ones. Copy structure from
public ladders (below); do *not* copy their anchors.

### Public references to borrow structure from

Read at least two of these before authoring, to
calibrate on structure. Do *not* paste any of them into
your own ladder.

- **progression.fyi** — [progression.fyi](https://www.progression.fyi/)
  — a public library of published engineering ladders
  from real companies (Rent the Runway, Kickstarter,
  Monzo, GitLab, and dozens of others). The single
  best-organised starting point.
- **Rent the Runway engineering ladder** — the ladder
  Camille Fournier open-sourced during her time as CTO,
  the reference *The Manager's Path* itself points
  toward. Available at
  [dresscode.renttherunway.com/blog/ladder](https://dresscode.renttherunway.com/blog/ladder)
  (and mirrored at [github.com/renttherunway/dresscode-project](https://github.com/renttherunway/dresscode-project)).
- **CircleCI engineering competency matrix** — public
  engineering ladder — see the CircleCI blog at
  [circleci.com/blog](https://circleci.com/blog/) and
  the linked GitHub repository at
  [github.com/circleci/engineering-competency-matrix](https://github.com/circleci/engineering-competency-matrix).
- **Camille Fournier — *The Manager's Path*** —
  [oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/)
  — the CTO / VP-Eng / EM chapters describe the
  behaviour-anchor structure the v0 uses.
- **Will Larson — *Staff Engineer*** —
  [staffeng.com/book](https://staffeng.com/book) —
  the Tech-Lead / Architect / Solver / Right-Hand
  archetype vocabulary the L3 anchors reference.

### What the ladder v0 is *not*

- **Not a promotion checklist.** The ladder describes
  what each level *is*, not what an individual
  engineer must accomplish to be promoted. Promotion
  is a separate calibration conversation (see
  [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  for the practice).
- **Not a compensation table.** Level maps to a
  compensation band (below); level itself is a
  scope-and-behaviour description.
- **Not final.** V0 is designed to be re-written at
  the next stage transition. Explicit "v0, expected
  rewrite at Series-B" in the document header.

## The compensation band

The compensation band is the document that says, for
each level on the ladder, what the company pays. It
has three components:

- **Base salary band** — a low / mid / high range per
  level, adjusted by geography.
- **Equity grant band** — a low / mid / high range per
  level, expressed as % of the current cap table (with
  the current-round implied $ value as a *snapshot*).
- **Non-cash benefits band** — the health plan tier,
  the 401(k) match, the parental leave, the equipment
  budget.

The comp band is the CTO's artifact at pre-Series-A;
it is a **shared artifact with the CEO / CFO / People
lead** at Series-A and beyond. The People-lead
hand-off is the specific interface to
[`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum)
(People pillar); once a People lead is hired, the CTO
consumes the band and the People lead maintains it.

### Public references for calibrating the band

- **Levels.fyi** — [levels.fyi](https://www.levels.fyi/)
  — crowdsourced comp by level, location, and stage.
- **Pave** — [pave.com](https://www.pave.com/) — the
  paid startup-compensation benchmark most People
  leads at seed / Series-A subscribe to; the CTO
  consumes the report the People lead compiles.
- **Radford Global Technology Survey** —
  [radford.aon.com](https://radford.aon.com/) — the
  established enterprise-comp survey; less useful at
  seed than Pave but appears in later-stage
  conversations.
- **Carta State of Startup Compensation** —
  [carta.com/blog](https://carta.com/blog/) — aggregate
  cap-table and equity data by stage.
- **Index Ventures Option Plan** —
  [indexventures.com/optionplan](https://www.indexventures.com/optionplan/)
  — the equity-grant band by role, seniority, and
  stage.

### The geography row

At pre-Series-B stage the comp band should be *simple*
about geography. Two workable defaults, either of
which is fine, neither of which is "we'll figure it
out":

- **Location-adjusted band** — a single band expressed
  as "Tier 1 / Tier 2 / Tier 3" cities, with the tier
  definition published.
- **Location-independent band** — a single band, no
  adjustment; the company pays the same for the same
  work regardless of where the employee lives. Popular
  with remote-first companies; the compensation-per-
  employee is higher in absolute terms.

Do not default to "we'll negotiate per candidate". That
is not a band; it is the absence of one, and it will
produce compensation inequities the team will find and
resent.

### What the comp band is *not*

- **Not a floor for negotiation.** Publishing the band
  internally (or in an inbound-recruiting policy) is
  what makes it real. A band that is only ever quoted
  as the outcome of a negotiation is a band that
  doesn't do the equity work it is supposed to do.
- **Not the compensation the CTO owns forever.** The
  People lead — hired via
  [`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum)
  — takes ownership as the org grows. This chapter is
  the CTO's ownership *before* that hand-off.
- **Not the same as the equity band.** The equity band
  is on a different axis (cap-table %, not $ per
  year) and moves on a different rhythm (major
  refreshers, not annual increases).

## The peer-track hand-off (boundaries)

Two boundaries are explicit in this chapter, per the
module's learning objectives:

- **[`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (level 30)** owns **day-two management craft**:
  1:1s, feedback, performance-management, difficult
  conversations, the coaching craft of running a team
  well. This module owns the *decision to hire the
  first EM* and the *ladder v0 that describes the EM
  role*; the *day-two work* of being that EM is that
  peer track. The CTO consumes it themselves while
  onboarding the first EM, and routes the first EM to
  it during their first quarter.
- **[`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum)
  (People pillar)** owns **HR / people-ops /
  compensation depth**: employment law, benefits
  administration, payroll operations, the actual
  running of a performance-review cycle, the
  compensation-band survey subscriptions and
  maintenance. This module owns the *CTO's first
  version of the band as an engineering-org artifact*;
  the *ongoing maintenance and depth* are that peer
  track. The CTO consumes it — reads the survey the
  People lead compiles, participates in the
  compensation-review cycle the People lead runs —
  rather than owning it.

## The annual re-run rhythm

The three artifacts are living. The rhythm at seed /
Series-A / early-Series-B:

- **Org chart.** Re-read every monthly board update;
  re-drawn whenever the topology changes (per
  [`chapter 04`](04-team-topologies-at-startup-scale.md));
  re-baselined at every stage transition (see
  [`mod-106`](../mod-106-scaling-org-and-stack/README.md)).
- **Career-ladder v0.** Re-read every calibration
  cycle (typically once every 6 months); rewritten at
  each stage transition. V0 → v1 at first-EM trigger;
  v1 → v2 at VP-Eng trigger; v2 → v3 at Series-B.
- **Compensation band.** Re-priced against the public
  references at least once a year, and any time the
  hiring plan shifts the band's assumed geography /
  stage; re-published to the team on the same cadence.

The re-run is not a rewrite from scratch. It is a
version-and-diff — what changed, why, and what
triggered the change — the same discipline the
ADR-index re-review uses in [`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md).

## Failure modes

- **The unwritten ladder.** No document. Every
  compensation and promotion conversation triangulates
  against the CTO's head. Fix: v0 with three or four
  levels per track, one page each.
- **The copied ladder.** The team's ladder is a
  verbatim paste from another company's public ladder.
  Anchors reference systems the team does not have.
  Fix: keep the structure, rewrite the anchors against
  your actual systems.
- **The comp band without geography rule.** Every
  compensation offer is a bespoke negotiation. The
  team finds the inequities, and the CTO has a
  difficult conversation on their hands. Fix: publish
  a geography rule (adjusted or independent), and
  offer within the band.
- **The org chart nobody trusts.** Chart is out of
  date; team refers to a mental model instead. Fix:
  version and date; re-drawn at every topology change;
  posted in the same repo as the ADR index.
- **The v0-that-was-v-final.** V0 is written once and
  never revisited. The team scales past it, and the
  ladder now describes a company that no longer
  exists. Fix: explicit "v0, expected rewrite at
  Series-B" in the document header, and an annual
  re-read even if the rewrite is not yet due.

## Summary

- The **org chart** at pre-Series-B scale is a
  one-page picture — every person, every open
  requisition, reporting lines, team-type labels,
  version and date. Fits on one landscape page. Re-
  drawn at every topology change.
- The **career-ladder v0** has **three or four levels
  per track** (IC and EM), with per-level anchors on
  **scope / impact / behaviour / craft** that are
  specific to *your* company. Borrow structure from
  the public references
  ([progression.fyi](https://www.progression.fyi/),
  Rent the Runway, CircleCI); do not copy anchors.
- The **compensation band** has base / equity / non-
  cash-benefits components, is anchored to public
  references (Levels.fyi, Pave, Carta, Index Ventures
  Option Plan), and includes a **geography rule**
  (location-adjusted or location-independent) that is
  the same for every candidate.
- The three artifacts sit on **explicit peer-track
  boundaries**:
  [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (level 30) owns day-two management craft;
  [`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum)
  (People pillar) owns HR / people-ops / comp
  depth. The CTO owns the *engineering-org first
  version*; the peer tracks own the *depth and the
  ongoing maintenance*.
- The **annual re-run rhythm** — monthly for the org
  chart, semi-annually for the ladder, annually for
  the comp band, rewritten at each stage transition —
  keeps the artifacts from decaying to fiction.

The chapter's paired exercise —
[`exercise-06-org-chart-career-ladder-v0-comp-band-authoring.md`](exercises/exercise-06-org-chart-career-ladder-v0-comp-band-authoring.md)
— walks the authoring of all three artifacts for your
(or a real reference) startup, wired together as a
single reviewable package. The whole-module lab
scaffolds off the exercise outputs; the capstone
[`project-101`](../../../projects/project-101-first-year-technical-strategy-for-one-seed-startup)
integrates the outputs into the first-year technical-
strategy artifact.
