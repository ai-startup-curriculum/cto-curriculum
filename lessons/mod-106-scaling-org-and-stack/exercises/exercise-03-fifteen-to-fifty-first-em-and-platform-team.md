# Exercise 03 — Fifteen-to-Fifty: First EM and First Platform Team

**Module:** `mod-106-scaling-org-and-stack`
**Planned time:** ~3 hours
**Chapter this builds on:** [`03-fifteen-to-fifty-first-management.md`](../03-fifteen-to-fifty-first-management.md),
supported by [`mod-103` on build-vs-buy and the
earn-its-keep test](../../mod-103-build-vs-buy-and-platform-economics/README.md),
[`mod-104` chapter 05 on EM promote-vs-hire](../../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md),
and [`mod-104` chapter 06 on the career ladder and
comp band](../../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md).

## Problem statement

Author the **four 15-to-50 artifacts** as a
`docs/scaling/15-to-50/` sub-tree in the working repo:

1. **First-EM role charter** (one page) with the
   promote-vs-hire decision explicit.
2. **Earn-its-keep test result** (one to two pages)
   for the first platform team, running the
   framework from
   [`mod-103`](../../mod-103-build-vs-buy-and-platform-economics/README.md).
3. **Career ladder v1** (a directory — one file per
   level, three to five levels).
4. **First-annual-budget outline** (one page — the
   structure and category breakdown, not the
   spreadsheet).

The purpose is to force the CTO to make the four
15-to-50 decisions *in writing*, in the format the
board / CFO / new hires can read. Every one of these
becomes a durable artifact the org will maintain for
the next two years; every one of them has a well-
documented failure mode (chapter 03) that the exercise
is designed to make visible.

## Requirements

### Artifact 1 — First-EM role charter

`first-em-charter.md` — one page. Sections:

- **Team.** Which team does the EM manage? Named,
  with the current roster (5-8 engineers is typical
  for a first EM).
- **Responsibilities.** 6-10 bullet points. Cover:
  1:1s, hiring loops, performance conversations,
  delivery cadence for the team, cross-team
  representation.
- **Decision — promote or hire.** A paragraph
  naming the decision and the reasoning. Reference
  the two-column checklist in
  [`mod-104` chapter 05](../../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md).
- **If promoting** — name the internal candidate
  (or the profile if you cannot yet name), and the
  ramp-plan (what does the CTO's coaching load look
  like for the first six months).
- **If hiring** — name the candidate profile (title
  bands, target companies, comp band), the search
  timeline, and the interim plan (who does the EM
  work during the search).
- **What the EM is NOT.** 3-5 bullet points. Cover:
  the CTO (not a smaller version of), the tech
  lead (a distinct role — reference the tech lead
  charter from exercise 02).
- **Success criteria at 6 months.** 3-5 bullet
  points. Concrete, measurable where possible.
- **References** — Fournier
  ([oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/))
  and Zhuo
  ([juliezhuo.com/book](https://www.juliezhuo.com/book)).

### Artifact 2 — Earn-its-keep test result for the first platform team

`platform-team-earn-its-keep.md` — one to two pages.
The five-question framework from chapter 03 artifact 2
plus a decision:

- **Which platform capability?** Named. One of:
  build / CI-and-deploy, shared observability,
  shared data platform, internal developer portal.
- **Named internal customer(s).** At least two
  stream-aligned teams actively asking for the
  capability. Named team leads, current pain
  points, quoted where possible (*"the CI queue is
  costing my team 6 engineer-hours per week"*).
- **Sized cost-to-carry.** Engineering-hours per
  week currently paid across the affected teams.
  Reference the sizing methodology from
  [`mod-105` chapter 03](../../mod-105-technical-debt-as-business-decision/03-cost-to-carry-and-depreciation-schedule.md).
- **Explicit vs.-buy alternative.** Named vendor(s).
  Cost estimate. Why buy would or would not solve
  the problem.
- **Product-team-first alternative.** Could a
  stream-aligned team own this part-time? Why
  yes / no.
- **Time-boxed pilot.** Charter of the first 6-8
  weeks, with the explicit cancel-criteria
  (adoption target, satisfaction target).
- **Decision.** Charter the platform team, defer,
  or buy. If chartered, name the initial team (2-4
  engineers) and the tech-lead-or-EM for the team.

### Artifact 3 — Career ladder v1

`ladder/` directory. Files:

- `README.md` — one page. Introduction: the
  purpose of the ladder, the two tracks (IC and
  management), the review cadence (usually
  quarterly to biannual). Pointer to
  [progression.fyi](https://www.progression.fyi/)
  as a starting library of public ladders.
- `L1-engineer.md`, `L2-senior-engineer.md`,
  `L3-staff-engineer.md` (and optionally
  `L4-principal-engineer.md`) — the IC track,
  one file per level.
- `M1-engineering-manager.md` (and optionally
  `M2-senior-em.md`) — the management track, one
  file per level.

Per level file (one page):

- **Summary.** One paragraph — the shape of the
  role at this level.
- **Scope.** Named — subsystem, team, org.
- **Expectations across dimensions.** Four to six
  dimensions, each with a paragraph of expectations
  at this level. Suggested dimensions: technical
  scope, delivery, collaboration, mentorship,
  business awareness, company-specific dimension.
- **Comp band.** The salary + equity band. Name the
  range or the mid-point. Reference the comp band
  from
  [`mod-104` chapter 06](../../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md).
- **Progression signals.** 3-5 bullet points on
  what signals promotion to the next level.

The IC and management tracks converge (at your
company) at what level? Name it explicitly in the
`README.md`.

### Artifact 4 — First-annual-budget outline

`annual-budget-outline.md` — one page. The structure
of the budget, not the numbers themselves (the
numbers are a spreadsheet the CFO co-owns; the
outline is the framework).

Sections:

- **Headcount plan.** Break-down by role, by
  quarter, for the next four quarters. Reference
  the hiring plan from
  [`mod-104` chapter 01](../../mod-104-first-engineering-hires-and-team-topology/01-hiring-plan-against-roadmap-and-runway.md).
- **Compensation plan.** Salary + equity + benefits
  + on-call stipend, broken down by comp band.
  Reference the comp band from
  [`mod-104` chapter 06](../../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md).
- **Non-headcount spend.** Categories: cloud
  infrastructure, SaaS tools, contractor spend,
  training / conferences, hardware, professional
  services. Rough percentage of total engineering
  spend per category. Named vendors where relevant.
- **Top-down target.** The number the CFO gave you.
  Named. If you do not have one, name the process
  by which you will get one.
- **Per-team allocation.** A rough breakdown of the
  budget across the current teams. Named.
- **Contingency.** How much headroom for
  unexpected? Typical 5-15%. Named.
- **References** —
  [bvp.com/atlas/state-of-the-cloud](https://www.bvp.com/atlas/state-of-the-cloud)
  for benchmarks; the pointer to
  [`mod-108`](../../mod-108-cto-ceo-and-board-communication/README.md)
  for the CFO/CTO conversation shape.

## Starter guidance

- **The promote-vs-hire decision for the first EM
  is load-bearing.** Read
  [`mod-104` chapter 05](../../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md)
  before authoring the EM charter. If your rationale
  is *"they've been here a long time"* (promote) or
  *"we need external experience"* (hire), the
  reasoning is under-cooked; both promotions and
  external hires have specific triggers named in
  the checklist.
- **The platform-team earn-its-keep test should be
  honest.** If the answer is *"the tests do not
  pass yet"*, that is a valid answer — the exercise
  is to write down the negative result and defer.
  If every platform-team charter authored in every
  exercise instance ended in *"yes, charter it"*,
  the discipline is not real.
- **The career ladder is written for the *current*
  team, not for a hypothetical 200-engineer future.**
  If you cannot map every current engineer to a
  level in your ladder, either the ladder is wrong
  or you are avoiding a hard conversation. Both are
  data. Read three ladders from
  [progression.fyi](https://www.progression.fyi/)
  before writing yours; do not import wholesale.
- **The comp band on each level must be a real
  range, not a placeholder.** *"$X-$Y"* is not a
  comp band; *"$140k-$170k base, 0.15-0.30% equity"*
  is. Reference the comp-band-sourcing chapter from
  [`mod-104` chapter 06](../../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md).
- **The budget outline should force a top-down
  target.** If the CFO has not given you one, name
  the process by which you will elicit one. A
  bottom-up budget without a top-down target is the
  chapter 03 anti-pattern.
- **Non-headcount spend is often under-planned.**
  Cloud spend at 15-50 engineers can be 5-20% of
  the total engineering budget; SaaS tools (CI
  vendor, observability vendor, feature-flag
  vendor, IDE-copilot vendor, etc.) can be another
  5-10%. Do not leave *"other"* as an unbounded
  category.

## Acceptance criteria

Your drill output is complete when:

- The `docs/scaling/15-to-50/` directory contains
  the four artifacts in the shape above.
- The EM charter names a decision (promote or hire)
  and the reasoning against the
  [`mod-104` ch. 05](../../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md)
  checklist.
- The platform-team earn-its-keep result names all
  five test elements (customer, cost-to-carry,
  buy-alternative, product-team alternative, pilot)
  AND a decision — charter, defer, or buy.
- The career ladder has one file per level, with a
  real comp band and progression signals at each
  level. At least 3 IC levels and 1 EM level.
- The annual-budget outline names a top-down
  target (or the elicitation process), a per-team
  allocation, and a non-headcount spend breakdown
  with concrete percentages.
- All four artifacts cross-reference each other:
  the EM charter references the ladder, the
  platform-team charter references the budget, etc.
- The four artifacts together can be handed to the
  new EM (once hired / promoted) as the *"here is
  the shape of the org you are inheriting"* pack.

## What this feeds into

- **Exercise 04** — the 50-to-150 playbook builds
  on this. The VP Eng job spec is the natural next
  layer above the EM charter.
- **Exercise 06** — the platform-investment sizing
  at 15-50 is where the platform team's charter
  from artifact 2 lands in the four-category
  sizing.
- **The lab** — the four artifacts are the
  15-to-50 slice of the `docs/scaling/` runbook.

The 15-to-50 exercise is where the CTO stops being an
individual contributor and starts being a systems
designer of the engineering org. If any of the four
artifacts feels like *"I could do this later"*, the
exercise has not yet forced the discipline; go back
and finish it before moving to exercise 04.
