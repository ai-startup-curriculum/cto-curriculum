# The 15→50 Transition — First EM, Platform Team, Ladder, Budget, Departure

> "The stage at which the CTO stops being the substrate
> for every technical decision and starts being the
> substrate for every *management* decision — and then,
> around engineer thirty-five, discovers that they
> cannot be the substrate for that either." The 15→50
> transition is when the org acquires its first
> management layer, its first horizontal team, its
> first written career ladder, its first real annual
> budget, and its first voluntary departure. Each of
> those is a new failure mode the 5-15 handbook did not
> plan for.

## Motivation

The 5-15 handbook (chapter 02) buys the team a lot of
runway. Somewhere between engineer 18 and engineer 25,
though, the shape of the CTO's day changes again:

- The tech leads from the 5-15 phase are now doing 1:1s
  informally, running performance conversations without
  a framework, hiring without a rubric — and pushing
  the shape back to the CTO because they do not want
  to be the ones deciding who gets a promotion.
- A cross-team need has emerged (a shared CI system, a
  shared observability stack, a data platform) that no
  single stream-aligned team wants to own but which
  every team relies on. The CTO is spending time
  arbitrating between teams about it.
- The CFO — or the founder-CEO in the CFO role — asks
  for the engineering budget for the next fiscal year
  as an actual document, and the CTO does not have one.
- The first engineer to leave voluntarily hands in
  notice, and the CTO realises that a lot of tribal
  knowledge is walking out the door with them.

The 15→50 transition is the phase in which the CTO
installs the *management infrastructure* — role, layer,
document, calendar, ritual — that lets the org survive
the loss of the small-team assumptions.

Five artifacts do the work at this stage:

1. The first engineering manager (promote-vs-hire).
2. The first platform team, subject to earn-its-keep.
3. The career ladder v1.
4. The first annual budget cycle.
5. The first offsite and the first voluntary departure
   / culture-loss reckoning.

Each is treated below.

## Artifact 1 — The first engineering manager

The first engineering manager is the point at which the
CTO delegates the *management* side of the CTO job to a
second person. The mechanics of the promote-vs-hire
decision are covered in
[`mod-104` chapter 05](../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md);
this chapter's contribution is what changes about the
org shape when the EM is in place.

Three concrete deltas:

- **The EM owns 1:1s, performance conversations, and
  hiring loops for their team.** The CTO stops being
  the primary skip-level manager for those engineers.
  Camille Fournier's *The Manager's Path*
  ([oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/))
  and Julie Zhuo's *The Making of a Manager*
  ([juliezhuo.com/book](https://www.juliezhuo.com/book))
  are the two load-bearing reads on the shape of the
  role.
- **The EM owns the delivery cadence for their team.**
  The team's planning meetings, retrospectives, and
  weekly reporting go through the EM, not the CTO.
- **The EM is the CTO's peer in staff meetings.** Not a
  senior IC reporting up; a peer whose role is bounded
  by their team but whose judgment on their team's
  work is the source of truth for the CTO.

The 15-50 posture on the EM: the *first* EM sets the
shape of every subsequent EM. If the first EM is
promoted from within, they carry the founder's culture
into the role — and the next three EMs are hired
against a shape that assumes the founder's culture. If
the first EM is hired externally, they *import* a
culture — and the org either absorbs it or rejects it
loudly. Neither answer is wrong; both are load-bearing.
See
[`mod-104` chapter 05](../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md)
for the checklist.

The concrete artifact: a written **EM role charter** in
the engineering handbook (chapter 02, artifact 6).
Names the responsibilities, the meetings the EM owns,
the escalation paths, and the boundary against the tech
lead role. Two paragraphs; fits on one page.

## Artifact 2 — The first platform team, subject to earn-its-keep

The first platform team is the point at which the org
acquires its first *horizontal* team — one whose
customers are the other engineering teams rather than
external users. Team Topologies
([teamtopologies.com](https://teamtopologies.com/))
names this the *platform team* pattern; the earn-its-keep
test is the discipline that guards against premature
adoption.

The mistake the 15-50 CTO commonly makes: hires a
"platform team" of two or three engineers to work on a
shared internal tool, on the theory that *"we should
have a platform team by now"*. Three failure modes
follow:

- The platform team builds a tool nobody uses because
  they built the wrong tool. Six months later the
  platform team disbands and the tool is deprecated.
- The platform team builds a tool everyone is required
  to use but nobody wants to, because it is worse than
  the ad-hoc solutions each stream-aligned team had
  already built. Six months of "why is the platform
  team blocking us" complaints follow.
- The platform team's existence eats the *headcount*
  the product teams needed. Product velocity regresses;
  the CEO asks why.

The remedy is the **earn-its-keep test** from
[`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md).
Applied here:

- **Named internal customer.** At least two stream-
  aligned teams have to be actively asking for the
  capability. Not "would be nice"; "we are currently
  paying the tax the platform would remove". The
  Team Topologies book calls this being *"user-facing"*
  even for internal-only tools.
- **Sized cost-to-carry.** The stream-aligned teams
  have already been paying the tax; how many
  engineering-hours per week? See
  [`mod-105` chapter 03](../mod-105-technical-debt-as-business-decision/03-cost-to-carry-and-depreciation-schedule.md)
  on cost-to-carry sizing.
- **Explicit vs. buy alternative.** Is there a vendor
  (a CI-as-a-service, an observability platform, a
  feature-flag SaaS) that would do the job? If yes and
  the cost is acceptable, buy it and defer the platform
  team.
- **Product-team-first alternative.** Can one of the
  stream-aligned teams own the capability part-time
  instead of the platform team being a standalone team?
  At 15-25 engineers this is usually the right answer.
- **Time-boxed pilot.** The platform team's first
  charter is a 6-8 week pilot with an explicit
  cancel-criteria (adoption target, satisfaction
  target). If the pilot fails the team is disbanded,
  not extended.

The 15-50 posture: the *first* platform team is the one
you can defend against a board question. If the CEO
cannot repeat back the earn-its-keep test result, the
platform team is premature and the CTO should re-defer.
See
[`mod-103` chapter 03](../mod-103-build-vs-buy-and-platform-economics/README.md)
for the full framework.

Concrete first platform teams that commonly earn-their-
keep at 15-50 (in rough order of appearance):

- **A build / CI-and-deploy platform** — usually the
  first, because CI has become the shared bottleneck
  by ~15 engineers.
- **A shared observability stack** — logging, metrics,
  tracing. Usually second, driven by the second or
  third serious production incident.
- **A shared data platform** — data warehouse, ETL,
  analytics. Usually third, when the CEO wants
  self-serve product analytics and the ad-hoc
  spreadsheets stop scaling.
- **An internal developer platform** — the "we now have
  enough engineering-org internal tooling that it
  needs its own owner" team. Usually fourth, and often
  premature — see the
  [Team Topologies](https://teamtopologies.com/) book
  and the
  [platformengineering.org](https://platformengineering.org/)
  community for the vocabulary.

## Artifact 3 — Career ladder v1

At 15-50 engineers the promotion conversation stops
being *"the CTO decides who is a senior engineer"*
and starts being *"the team has a shared framework
against which promotion is decided"*. Without the
framework, three failure modes appear:

- **Title inflation.** Every engineer negotiates their
  own title on hire. Two years in, "senior engineer"
  means whatever the individual negotiated. The org
  cannot compare seniority across teams.
- **Promotion stalls.** An engineer who has clearly
  outgrown their current level cannot be promoted
  because the CTO has no vocabulary for what the next
  level looks like. The engineer leaves for a company
  that does.
- **The comp gap.** External hires come in at a comp
  band the internal engineers did not know existed,
  because there is no written band structure. The
  internal engineers find out (they always find out).
  Morale drops.

The career ladder v1 is a *written* document — one page
per level — that names the expectations at each level.
Three references worth having open:

- **Rent the Runway's engineering ladder** (Camille
  Fournier's open-source ladder that many startups
  adapt) — [github.com/kickstarter/eng-ladder](https://github.com/kickstarter/eng-ladder)
  (Kickstarter's fork is the most-cited variant;
  original writeup at
  [medium.com/@skamille/an-incomplete-list-of-skills-senior-engineers-need-beyond-coding-8ed6a940b6a5](https://skamille.medium.com/an-incomplete-list-of-skills-senior-engineers-need-beyond-coding-8ed6a940b6a5)).
- **progression.fyi** —
  [progression.fyi](https://www.progression.fyi/) — a
  compilation of publicly-published career ladders from
  a hundred-plus companies. Read three or four before
  writing your own.
- **CircleCI's engineering competency matrix** —
  [github.com/circleci/engineering-competencies](https://github.com/circleci/engineering-competencies).
  Concrete, granular, worth adapting.

The 15-50 ladder v1 shape:

- Three to five levels — typical: Engineer, Senior
  Engineer, Staff Engineer, Principal Engineer. Do not
  invent Level 1a / 1b / 1c distinctions at this scale.
- Two tracks past Senior — IC track and management
  track. The IC track goes to Staff and Principal; the
  management track goes to EM and Senior EM. At 15-50
  the tracks converge again at the CTO level; the
  divergence at Staff / Senior EM is the first written
  affirmation that IC-track leadership is a real
  seniority level.
- One page per level, describing expectations across
  four to six dimensions (technical scope, delivery,
  collaboration, mentorship, business awareness, and
  usually one company-specific dimension).
- The **comp band** attached to each level. See
  [`mod-104` chapter 06](../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md)
  for the comp-band shape.

The 15-50 discipline: the ladder is *published to the
whole team* and every engineer knows the level they are
at and the level immediately above. If an engineer
cannot articulate their current level or the gap to the
next, the ladder is not doing its work.

Two 15-50 anti-patterns to name:

- **The ladder as a compliance document.** Fifteen
  pages, three hundred bullet points, nobody reads it,
  nobody uses it. If the ladder v1 runs longer than
  ten pages the CTO has borrowed a big-tech ladder
  meant for a thousand engineers. Cut ruthlessly.
- **The ladder that only measures technical output.**
  Missing the mentorship / collaboration / business
  awareness dimensions means the org promotes on
  code-shipped alone and finds itself with a bench of
  Senior Engineers who cannot lead a project. The
  ladder needs multiple dimensions.

## Artifact 4 — The first annual budget cycle

At 15-50 engineers the CFO (or the CEO acting as CFO)
starts asking for engineering's annual budget as a
document, and the CTO discovers that engineering
budgeting has three dimensions:

- **Headcount.** Number of hires by role by quarter.
  Derived from the hiring plan
  ([`mod-104` chapter 01](../mod-104-first-engineering-hires-and-team-topology/01-hiring-plan-against-roadmap-and-runway.md)).
- **Compensation.** Salary, equity, benefits, on-call
  stipend. Derived from the comp band
  ([`mod-104` chapter 06](../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md))
  and the headcount plan.
- **Non-headcount spend.** Cloud infrastructure, SaaS
  tools, contractor spend, training / conferences,
  hardware, professional services. Usually 15-30% of
  the total engineering budget at 15-50 engineers.

The 15-50 budget is a spreadsheet, quarterly-broken-out,
that the CFO can reconcile against the company financial
model. Two references worth having open:

- **Andreessen Horowitz — *The Business of Software***
  ([a16z.com/tech-topics](https://a16z.com/tech-topics/)),
  particularly the material on gross-margin structure
  and the shape of R&D as a percentage of revenue at
  seed / Series A / Series B — useful benchmarks for
  the "is our engineering spend defensible" question.
- **Bessemer Venture Partners — *State of the Cloud***
  ([bvp.com/atlas/state-of-the-cloud](https://www.bvp.com/atlas/state-of-the-cloud)),
  annual publication with SaaS benchmark data (R&D as
  % of revenue by stage, gross retention, etc.).

Two 15-50 anti-patterns to name:

- **The bottom-up budget.** Every team lead adds up
  their headcount asks; the total is presented to the
  CFO. The CFO cuts 20% off the top; the CTO passes
  the cut to the team leads; the team leads cut what
  they can least defend. The remedy is a *top-down
  target* from the CFO / CEO, translated by the CTO
  into per-team allocations against the roadmap.
- **The absence of non-headcount spend.** Cloud
  infrastructure gets budgeted at "whatever it was
  last year", and the CFO discovers a 40% cloud
  overrun mid-year. The remedy is a per-quarter
  cloud-spend forecast, updated against the actual
  monthly bill.

## Artifact 5 — The first offsite and the first departure

Two things happen for the first time at 15-50 engineers
that neither the 0-5 nor the 5-15 phase prepares you
for: the **first offsite** and the **first voluntary
departure**.

### The first offsite

At 5-15 engineers the whole team eats lunch together
and the "offsite" is a Friday afternoon at a pub. At
15-50 the team no longer fits at a single dinner table,
half the team joined after the founders' living-room
phase, and the shared context is entirely a work-time
artifact.

The first offsite is:

- **Two to three days**, off-site (a rented meeting
  space is fine, an actual "trip" is not required and
  can be a distraction).
- **Whole engineering team**, plus product /
  design / CEO for at least part of it.
- **A specific outcome.** Not "team building" as an
  end in itself. The 15-50 offsite outcomes commonly
  are: agree the next-quarter roadmap; agree the
  next-quarter platform / infra investment; agree the
  hiring plan for the next two quarters; work through
  a specific hard architectural question the team
  cannot resolve async.
- **A written output** by the end of the offsite. The
  offsite is not successful if there is nothing to
  point to on Monday.

The failure mode: the offsite is a two-day retreat with
trust-falls and no written output. The team returns
tired and no decisions were made. Do not run this
offsite.

### The first voluntary departure

The first voluntary departure — the first engineer who
joined in the 5-15 phase, hits their two-year vesting
cliff, and decides to leave for another opportunity —
is a distinct event with three consequences:

- **Tribal-knowledge loss.** The engineer holds context
  about the codebase and the customer base that isn't
  written down. The engineering handbook (chapter 02
  artifact 6) is the mitigation, and the departure is
  the first real test of whether the handbook is
  actually load-bearing.
- **Culture signal to the rest of the team.** The way
  the CTO responds to the departure sets a template
  for the next ten departures. Two questions
  everybody watches: *"did the CTO make an effort to
  understand why?"* and *"did the CTO speak well of
  the departed engineer on the last day?"* Answers of
  "no" and "no" produce a ripple in the retention
  numbers within a quarter.
- **The successor-question.** Who now owns the systems
  the departing engineer owned? If the answer is *"we
  will figure it out"*, the successor discovery is a
  distraction for months. The remedy is a written
  transition plan in the last two weeks of the
  engineer's tenure — code walkthroughs, runbook
  updates, escalation-path updates, formal handoff of
  every project.

The 15-50 discipline: the *first* voluntary departure
gets the *first* proper exit interview, the *first*
proper transition plan, and the *first* proper
retrospective on what the org could have done
differently. The mechanisms it produces are the ones
that carry through the next fifty departures.

Larson's *An Elegant Puzzle*
([lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/))
has a chapter on regrettable / non-regrettable attrition
that is the load-bearing read on the *"how do we
measure and respond"* side.

## The 15-50 DORA reading

Chapter 05 gives the full treatment; the 15-50 point:

- Deployment Frequency should be *many-times-daily* by
  the end of the transition. If it is not, the first
  platform team's charter (artifact 2) usually needs
  to include a deploy-infrastructure investment.
- Lead Time for Changes should stay under a day. If
  it is regressing, the code-review queue at team
  boundaries is usually the cause — RFC discipline
  (chapter 02 artifact 4) needs strengthening.
- Change Failure Rate should be under 15%. If it is
  higher, the first platform team's charter usually
  needs to include a test-infrastructure investment.
- MTTR should be under an hour. If it is not, the
  on-call rotation and incident-response playbook
  (chapter 07) need reinforcement.

## Where the boundary sits

The 15-50 transition is where the boundary to
[`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
(level 45) starts appearing in the CTO's day. Two
specific classes of decision that belong to the senior
architect rather than the CTO:

- **The multi-region / multi-tenancy architecture
  decision.** If the product is entering an enterprise
  market that requires data-residency or a private-
  deployment option, the *architecture* work belongs
  to a senior architect. The CTO can make the *build-
  or-buy / hire-a-consultant* call, but the CTO should
  not personally design the multi-region control
  plane.
- **The deep platform / kernel-level infra work.**
  If the platform team's charter includes a custom
  scheduler, a bespoke storage layer, or a serious
  networking layer, the *depth* belongs to a senior
  architect or a principal engineer, not to the CTO.

Chapter 06 covers the platform-investment sizing at
15-50 and names the deferrals.

## Summary

- 15-50 is the phase in which the CTO installs the
  management infrastructure — role, layer, document,
  calendar, ritual — that lets the org survive the
  loss of the small-team assumptions.
- **First EM** — the CTO's first *management*
  delegation. Owns 1:1s, hiring, performance for a
  team. Fournier's *The Manager's Path*
  ([oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/))
  and Zhuo's *The Making of a Manager*
  ([juliezhuo.com/book](https://www.juliezhuo.com/book))
  are the loads. Promote-vs-hire per
  [`mod-104` chapter 05](../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md).
- **First platform team** — *only if the earn-its-
  keep tests from [`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md)
  pass*. Named internal customer, sized cost-to-carry,
  explicit vs.-buy alternative, product-team-first
  alternative, time-boxed pilot. Team Topologies
  ([teamtopologies.com](https://teamtopologies.com/))
  is the vocabulary.
- **Career ladder v1** — three to five levels, two
  tracks (IC and management), one page per level, comp
  band attached. progression.fyi
  ([progression.fyi](https://www.progression.fyi/)) is
  the compendium of public ladders to read before
  writing your own.
- **First annual budget cycle** — headcount +
  compensation + non-headcount spend. Top-down target
  from the CFO, translated by the CTO. See
  [`mod-108`](../mod-108-cto-ceo-and-board-communication/README.md)
  for the CFO/CTO relationship shape.
- **First offsite** — two to three days, whole team,
  specific outcome, written output. Not team-building
  as an end in itself.
- **First voluntary departure** — the first real test
  of the engineering handbook. Sets the template for
  every subsequent departure; the CTO's response is
  watched by the whole team. Larson's *An Elegant
  Puzzle*
  ([lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/))
  is the load on regrettable attrition.
- DORA numbers at 15-50: Deployment Frequency
  many-times-daily, Lead Time under a day, Change
  Failure Rate under 15%, MTTR under an hour. Chapter
  05 gives the full treatment.
- The boundary to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) starts appearing at 15-50: multi-region
  / multi-tenancy architecture and deep platform work
  belong to a senior architect the CTO has hired, not
  to the CTO themselves.

The chapter's paired exercise —
[`exercise-03-fifteen-to-fifty-first-em-and-platform-team.md`](exercises/exercise-03-fifteen-to-fifty-first-em-and-platform-team.md)
— asks you to author the first-EM role charter, the
earn-its-keep test result for the first platform team,
the career ladder v1, and the first-annual-budget
outline.

Chapter 04 walks the 50→150 transition — the first VP
Eng, the first governance council, the first budget
re-forecast under investor pressure, the first
cross-team dependency crisis, and the honest reckoning
that the CTO's day job has stopped being individual
technical decisions and become cross-team coordination.
