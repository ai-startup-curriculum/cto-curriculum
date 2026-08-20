# Cost-to-Carry and the Depreciation Schedule

> "Interest, in the financial-debt metaphor, is the
> ongoing cost of working around a piece of not-quite-
> right code. It is paid continuously." — the operational
> reading of Cunningham 1992
> ([c2.com/doc/oopsla92.html](http://c2.com/doc/oopsla92.html)),
> made explicit for the CTO.

## Motivation

A debt inventory (chapter 06) that says *"the billing
service is a mess"* is not defensible in a resource-
allocation conversation. It is defensible only when the
line reads *"the billing service currently costs the team
~8 engineering-hours per week in workarounds, and that
number is projected to grow to ~14 hours/week over the
next two quarters as we onboard three more people to it."*

That transformation — *"a mess"* → *"8 hours/week rising
to 14"* — is what this chapter walks. It is the sizing
that lets the debt item be compared against every other
use of engineering time (shipping the next feature,
hiring, on-call load, meetings) on a **like-for-like**
axis. Without it, the debt is a rhetorical claim; with
it, the debt is a portfolio line.

## The two numbers

For every debt item you plan to put in the inventory,
you size **two** numbers:

- **Cost-to-carry (now)** — engineering-hours per week
  the team currently spends because of this debt. This
  is the *interest* in Cunningham's metaphor. It is a
  *rate*, not a stock.
- **Depreciation schedule (projected)** — how the
  cost-to-carry is expected to change over the next
  two to four quarters, as the codebase grows and the
  team grows.

The pair matters because a debt item costing 2 hours/week
today but projected to reach 20 hours/week in two
quarters is a *different* portfolio item from one that
costs 5 hours/week today and will still cost 5 hours/week
in two quarters. The board conversation about the two is
different.

## Sizing the cost-to-carry (now)

Cost-to-carry is measured in engineering-hours per week.
Not lines of code, not dollars, not "story points" —
engineering-hours, because that is the currency the
refactor budget (chapter 04) and the hiring plan (see
[`mod-104` chapter 01](../mod-104-first-engineering-hires-and-team-topology/01-hiring-plan-against-roadmap-and-runway.md))
are both denominated in.

Six practical sources you can add up. None of them is
precise; all of them are more disciplined than "a mess."

### Source 1 — the workaround tax

For a given debt item, list the workarounds the team
routinely applies when working near it:

- Extra tests written to guard against the debt's
  brittleness.
- Extra manual QA cycles because automated tests
  can't cover the case.
- Extra code-review comments the same reviewers write
  every week.
- Extra hand-off conversations between engineers who
  each own part of the mess.
- Extra deploy-safeguards (staged rollouts, feature
  flags, manual runbooks) that would not be needed if
  the debt were fixed.

Estimate the hours-per-week the workarounds cost. A
useful discipline: **ask three engineers who work near
the debt to independently estimate**, then take the
median. Solo estimates by the CTO tend to under-count
because the CTO is not the one paying the tax.

### Source 2 — the on-call tax

Debt that produces incidents is priced against the
on-call rotation. For a given item, count:

- Incidents in the last two quarters that traced back
  to this debt (post-mortems / retros are the primary
  source).
- Hours per incident on average — detect, triage,
  mitigate, root-cause, post-mortem.
- Multiplied out, hours-per-quarter → hours-per-week.

Add a **standby cost** too: engineers on-call spend a
non-trivial fraction of their attention worrying about
whether the debt-related subsystem will page them, which
degrades focused work even between incidents. This is
harder to size but real; a conservative rule of thumb is
+10-25% of the paged-incident hours as a standby
premium.

### Source 3 — the onboarding tax

Every new engineer who has to work near the debt has to
learn its workarounds. Measure:

- Days to first meaningful PR near the debt.
- Days to on-call readiness for the debt-touching
  services.

For a given item, the onboarding tax = (extra onboarding
days per new hire) × (new hires per quarter) ÷ (weeks per
quarter). At team-size 5 with one hire every two
quarters this is negligible; at team-size 25 with two
hires per quarter it can dominate every other source.

### Source 4 — the change lead-time tax

The DORA four-key metrics (see
[dora.dev](https://dora.dev/) and Forsgren, Humble, Kim,
*Accelerate*) name **Lead Time for Changes** and
**Change Failure Rate** as first-class delivery
measurements. Debt regresses both:

- Changes near the debt take longer to merge (more
  review cycles, more test flakiness, more
  reverts).
- Changes near the debt fail more often (revert rate,
  post-deploy hotfix rate).

For a given item, compare the lead-time and failure-rate
on the debt-touching modules against the team's baseline;
the delta translates to hours-per-week of "moving through
tar" that a fixed system would recover.

### Source 5 — the feature-slip tax

Some debt items do not add friction to *ongoing* work —
they *forbid* certain features from being built at all
until the debt is repaid. Examples:

- The auth check is at 47 call sites; adding
  tenant-scoped auth is not a two-week feature but a
  three-month refactor.
- The billing state machine is spread across three
  services; adding usage-based pricing requires
  changes in all three, coordinated.

For these items, cost-to-carry is measured by *the
feature you cannot ship*. This is not hours-per-week
directly; it is the delta between "this feature ships in
X" and "this feature ships in X + Y after the debt is
paid." Chapter 04 handles the business framing of that
delta.

### Source 6 — the morale / attrition tax

The hardest source to size and the one CTOs most often
skip. Engineers who spend a lot of time in bad code
disengage; some leave. The full attrition-cost model
(recruiter time, ramp cost, opportunity cost) lives
in People / Governance ([`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum)).
For the debt inventory, you flag which items are known
to correlate with retention risk (typically the
structural debt from chapter 02) and note it as a
qualitative row rather than sizing it in hours; the
People lead is the authoritative source for the dollar
number.

### Adding them up

For a given debt item, the cost-to-carry (now) is the
sum of the applicable sources, expressed as **engineering-
hours per week**. Round generously — this is not a
finance-team number, it is an order-of-magnitude number
that lets you compare debt items against each other and
against feature work. A useful convention:

- **< 2 hours/week** — negligible; deprioritise
  unless the depreciation curve is steep.
- **2-8 hours/week** — real but tolerable at current
  team size; include in the portfolio but not urgent.
- **8-20 hours/week** — a first-class portfolio item;
  needs a business owner and a plan.
- **> 20 hours/week** — a stop-the-world item; block
  new feature work in the affected area until either
  a plan is in place or the item is formally accepted
  as a permanent tax.

## The depreciation schedule (why the interest rate rises)

Cunningham's original metaphor implicitly treated the
interest rate as constant. In practice it rises, for four
distinct reasons — and understanding *which* reason is
what lets you extrapolate the curve.

- **Team-size compounding.** The same piece of debt
  taxing 2 people at team-size 5 taxes 20 people at
  team-size 50. If cost-to-carry per person is
  roughly constant, total cost-to-carry scales
  linearly with team size. This is why deferring
  structural debt through a hiring wave is expensive
  — you multiplied the tax without noticing.
- **Codebase-size compounding.** As the codebase
  grows, more code lives adjacent to the debt. More
  adjacency = more places every change is at risk of
  entangling the debt. This scales roughly with the
  number of modules that call into the debt-touching
  code, not with total LOC.
- **Turnover compounding.** As engineers who
  understood the original context leave, the
  workaround-tax rises for the engineers who
  inherited the code without the context (Chesterton's
  Fence effect — see chapter 05). New hires spend
  hours reconstructing "why is it like this?" that
  the original authors would not have spent.
- **Adjacent-decision compounding.** Every new
  architectural decision that has to accommodate the
  wrong shape *entrenches* the wrong shape. A wrong
  aggregate boundary, once four downstream services
  have been designed against it, is much more
  expensive to fix than when only one service assumed
  it. This is the specific compounding
  *Building Evolutionary Architectures* (Ford, Parsons,
  Kua —
  [oreilly.com](https://www.oreilly.com/library/view/building-evolutionary-architectures/9781491986356/))
  is written against.

The depreciation schedule for a given item is your
projection over the next 2-4 quarters of how these four
compounders will move the cost-to-carry number. Be
concrete: *"cost-to-carry rises from ~8 to ~14 hours/week
by end of next quarter, driven primarily by team-size
compounding (three new hires onto the billing
subsystem)"*. That is the sentence the CFO wants next
to the portfolio line, because it turns *"the billing
service is a mess"* into *"the billing service is
compounding faster than the hiring plan can absorb, and
here is the specific hiring milestone that makes the
math flip."*

## The Google Software Engineering perspective

*Software Engineering at Google* (Winters, Manshreck,
Wright — [abseil.io/resources/swe-book](https://abseil.io/resources/swe-book))
has a chapter titled *"Software Engineering is
Programming Integrated Over Time"* whose central point
is exactly the compounding above: the cost of a decision
scales with the number of people, systems, and later
decisions that consume it. That framing is a useful
citation when explaining depreciation to a stakeholder
who has not thought about interest rates on code before.

Also useful — SPACE (Forsgren et al.,
[queue.acm.org/detail.cfm?id=3454124](https://queue.acm.org/detail.cfm?id=3454124))
and DORA ([dora.dev](https://dora.dev/)) — for the
system-level *symptoms* of aggregated debt (lead time
rising, change-failure rate rising, developer-survey
friction rising). See [`mod-106` chapter 05](../mod-106-scaling-org-and-stack/README.md)
on DORA as the delivery-cadence signal for the whole
org. If those trend lines are rising and no team can
point at a single new-feature cause, aggregated cost-to-
carry is the usual explanation.

## Two things to *not* try to size

- **A dollar value on the debt.** Some finance-adjacent
  frameworks (Nugroho et al.'s SIG *"backlog-based
  quantification"* of maintainability
  is one example) put a dollar cost on debt. This is
  legitimate research but is fragile in a startup
  context and easily gamed. The engineering-hours-per-
  week number is more honest because your CFO already
  has the loaded engineer cost from
  [`mod-104` chapter 01](../mod-104-first-engineering-hires-and-team-topology/01-hiring-plan-against-roadmap-and-runway.md);
  they can multiply if they want a dollar. Do not
  publish the multiplication yourself unless the CFO
  co-owns the number.
- **A precise ROI on the fix.** *"Fixing this debt
  saves 8 hours/week"* is a plausible top-line. But
  "the fix costs 200 engineering-hours over 6 weeks"
  and "the fix will save 8 hours/week from week 7
  forward" is not an ROI you should publish, because
  the *saving* is almost never realised in full — the
  team fills the recovered time with new work, and
  the counterfactual is unmeasurable. Publish the
  cost-to-carry and the depreciation curve; let the
  business owner (chapter 04) decide the fix is worth
  it without pretending the ROI number is finance-
  grade.

## Failure modes

- **The zero-time-per-week estimate.** The CTO thinks
  the debt costs nothing because *they personally* do
  not touch it much. Meanwhile the two engineers who
  do are losing a day a week to it. Fix: use the
  median-of-three-independent-estimates protocol from
  Source 1.
- **The single-source estimate.** The estimate uses
  only the workaround tax and skips the on-call
  tax, the onboarding tax, and the lead-time tax.
  The number ends up 3-5× too low. Fix: walk each of
  the six sources for each item, even if some come
  out to zero.
- **The flat depreciation schedule.** Every item's
  projected cost-to-carry equals its current cost-to-
  carry. This means the CTO has not thought about
  team-size / codebase-size / turnover compounding.
  Fix: for each item, name the *dominant compounder*
  (which of the four listed above) and its two-
  quarter projection.
- **The "we'll measure it precisely" delay.** The team
  waits to publish the inventory until it can attach
  a Datadog dashboard to every line. It never ships.
  Fix: publish the order-of-magnitude version now;
  refine when you have live telemetry.
- **The dollar-cost publication.** The CTO publishes
  a debt inventory with a "cost per year in USD"
  column that finance did not sign off on. Finance
  disputes the multiplier; the whole inventory loses
  credibility. Fix: publish hours; let finance
  multiply when they want to.

## Summary

- Every debt item's sizing has **two numbers**:
  **cost-to-carry (now)** in engineering-hours per
  week, and the **depreciation schedule** — how that
  cost is projected to change over the next two to
  four quarters.
- Cost-to-carry sums **six practical sources**: the
  workaround tax, the on-call tax, the onboarding
  tax, the lead-time tax (Lead Time / Change Failure
  Rate delta per DORA — [dora.dev](https://dora.dev/)),
  the feature-slip tax, and (qualitatively) the
  morale / attrition tax.
- The interest rate **rises** because of four
  compounders: team-size, codebase-size, turnover,
  and adjacent-decision. Name which one dominates
  for each item; it is what makes the projection
  defensible.
- Do **not** publish a dollar-per-year debt figure
  unless the CFO co-owns the multiplier; do **not**
  publish a precise ROI on the fix. Publish hours per
  week, let the business owner (chapter 04) decide.
- The whole sizing is order-of-magnitude by design.
  Precision comes from tie-breaking with real DORA
  telemetry (Deployment Frequency, Lead Time, Change
  Failure Rate, MTTR) once you have it.

The chapter's paired exercise —
[`exercise-02-cost-to-carry-sizing-for-five-debt-items.md`](exercises/exercise-02-cost-to-carry-sizing-for-five-debt-items.md)
— walks the sizing of five items from your own inventory,
including the median-of-three protocol, the six sources,
and the depreciation projection. Chapter 04 ties each
sized item to a business owner; chapter 05 picks the
response; chapter 06 formats the whole thing as a
portfolio a board member can read.
