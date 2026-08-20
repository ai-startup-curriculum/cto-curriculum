# The Hiring Plan Against the Roadmap and the Runway

> "Every hire is a bet against runway." — a line variously
> attributed inside the seed-stage founder community, but
> the shape is universal: at pre-seed and seed, cash out is
> the clock every hiring conversation is timed against, and
> every offer letter you sign shortens it.

## Motivation

Ask a first-time CTO "what does your hiring plan look like
for the next twelve months?" and one of three answers is
likely:

- *"We're hiring two senior back-end engineers as soon as
  we can find them."* — a role and a seniority, but no
  timing, no cost, and no link to the roadmap.
- *"We'll hire when we need to."* — no plan at all; the
  team will grow reactively as the pain of *not* hiring
  becomes acute, which is the point at which the hire is
  already six months late.
- *"Here's a spreadsheet."* — twenty rows, twelve months,
  fully-loaded costs, hiring-manager assignments, and a
  named trigger for each — the answer a Series-A board
  chair expects, and the artifact this chapter teaches you
  to author.

The problem the first two answers have in common is that
they are *not* pinned to two other artifacts a competent
board reviewer will ask about in the same meeting: the
**technical roadmap** (why do we need these specific hires
and not others?) and the **runway** (can we actually
afford them, and what happens to the fundraising path if
we do?).

This chapter names the shape of a hiring plan that a
first-round-investor board member can read in five minutes
and defend to their partnership — and, more importantly,
that the CTO can defend to the CEO when the cash-out date
starts moving.

## The three artifacts hiring plans are authored against

A hiring plan is a *derived* artifact. It is derived from
three inputs that must exist first, or the plan is
guessing.

### Input 1 — the technical roadmap

The roadmap says what the team must ship over the next
12-18 months. Every hire in the plan should be traceable
to a specific commitment on the roadmap: a customer
segment the product must serve, a compliance milestone
the enterprise deal requires (see
[`mod-107`](../mod-107-founder-scope-security-and-compliance/README.md)),
a platform capability the build-vs-buy matrix (see
[`mod-103` chapter 01](../mod-103-build-vs-buy-and-platform-economics/01-build-vs-buy-as-portfolio-decision.md))
resolved to *build*, or a scale threshold the current
team cannot meet.

The failure mode this rules out: **hiring the archetype
you find comfortable to work with**, rather than the
archetype the roadmap requires. A CTO who is a distributed-
systems specialist will over-hire distributed-systems
engineers even when the roadmap calls for a front-end lead
and a data engineer.

### Input 2 — the runway

The runway is the current cash balance divided by monthly
net burn — the number of months the company can operate
before it runs out of money. It is owned by the CEO / CFO,
not the CTO, but the CTO must understand it precisely
enough to reason about the hiring pace it can support.

The relevant numbers:

- **Current cash balance** — actual bank balance.
- **Current monthly net burn** — cash out minus cash in.
- **Months of runway** — cash / burn.
- **Fundraising cadence** — when is the next raise
  targeted, at what stage, at what expected proceeds?
  Every hiring plan is either *bridge-to-next-raise* (the
  hires must be productive and their impact visible in the
  next fundraising narrative) or *post-raise* (the plan is
  contingent on the raise closing, and must be flagged as
  such).
- **Non-headcount OpEx** — cloud bill, vendor invoices,
  legal, rent, salaries already committed. Grows on a
  schedule the CTO does not control, but eats runway too.

A hiring plan that adds N engineers over the next twelve
months at $X fully-loaded per engineer shortens runway by
N × X per year. If that shortening is not tolerable given
the target next-raise date, the plan is wrong regardless
of the roadmap.

### Input 3 — the funding-stage-appropriate compensation band

Compensation is not one number. It is (i) a base salary,
(ii) an equity grant (typically ISOs with a four-year vest
and a one-year cliff at seed / Series-A stage in US-shape
startups), (iii) any signing bonus, and (iv) benefits and
employer-side payroll taxes. All four are stage-sensitive:
a seed-stage startup pays a founding engineer more equity
and less cash than a Series-B startup does, because the
seed-stage startup does not have the cash to compete on
base and the equity has more expected value to a candidate
who joins early.

The public references the CTO consults to calibrate the
band — and cites in the plan — are:

- **Levels.fyi** — [levels.fyi](https://www.levels.fyi/).
  Crowdsourced comp data by level and location; the seed
  / Series-A columns are thinner than the FAANG columns
  but the trajectory shape is calibrated well.
- **Option Impact / Pave / Radford surveys** — the paid
  compensation surveys People / HR teams subscribe to.
  The CTO does not need to run the survey — this is the
  hand-off to the People / Governance track
  ([`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum)
  People pillar) — but must understand what the People
  lead is pricing against.
- **Carta State of Startup Compensation** — Carta's
  published aggregate cap-table and equity data —
  [carta.com/blog](https://carta.com/blog/) — for the
  equity-grant band by stage.
- **Y Combinator startup pay guidance** — the founder-
  facing rules-of-thumb YC publishes for founding-engineer
  equity ranges (typically communicated inside the current
  YC startup school library —
  [startupschool.org/library](https://www.startupschool.org/library)).

Chapter 06 of this module is where the comp band is
formalised as an artifact; this chapter uses it as an
input. Do not invent numbers if you cannot verify them
against a public reference — annotate the row with
`<comp: check Levels.fyi / Pave for current band>` and
move on.

## The fully-loaded per-engineer cost model

The single most common error in first-time hiring plans is
using **base salary** as the per-engineer cost. Base is a
minority of the actual cost. The rows a defensible plan
budgets for, per engineer, per year:

- **Base salary** — the offered number.
- **Employer-side payroll taxes** — US: FICA (Social
  Security + Medicare), FUTA, state unemployment. Rule of
  thumb: **7-10% of base** in the US; higher in Europe.
- **Benefits** — health, dental, vision, 401(k) match,
  short/long-term disability, life. Rule of thumb: **10-
  20% of base** for a startup-tier benefits plan.
- **Equity expense (non-cash but real)** — the fair value
  of the ISO grant, expensed over the vest period. Does
  not consume cash but does dilute the cap table; track it
  separately as a *dilution budget*, not a cash number.
- **One-off ramp costs** — laptop and peripherals,
  onboarding cost (the productive time of the team
  members onboarding the new hire), signing bonus if
  offered, immigration / relocation if applicable.
- **Recruiting cost** — agency fee if used (typically
  15-25% of first-year base), or the loaded cost of
  in-house recruiter time and the founder / CTO interview
  hours.
- **Vendor / seat cost** — the SaaS seats the new engineer
  consumes (GitHub, Linear / Jira, Datadog, cloud IDE,
  Notion, 1Password, laptop-management, VPN, etc.) — often
  $200-500 per engineer per month at seed / Series-A
  scale.

For a US-based, Bay Area / NYC seed-stage back-end
engineer with a $180k base, a defensible fully-loaded
number is often in the $230k-260k per year range — a **1.3
to 1.5x multiplier** on base. The specific multiplier is
what your CFO / fractional-CFO would compute against your
actual benefits plan and jurisdiction. If you cannot get
that number, annotate the plan with `<loaded-multiplier:
CFO to confirm; using 1.4x placeholder>` and use the
placeholder — but do the arithmetic against a full-loaded
number, not against base.

## The one-page hiring plan

The output of this chapter's discipline is a **single-page
hiring plan** the CTO walks the CEO and the board
through. Columns:

```
| # | Role | Seniority | Team | Trigger (roadmap item / signal) | Target start | Fully-loaded cost/yr | Comp band source | Contingent on |
|---|------|-----------|------|---------------------------------|--------------|----------------------|------------------|---------------|
| 1 | Founding backend engineer | Senior / Staff | Product | MVP shipped to first paid design partner; CTO capacity < 40% IC | Month +1 | $260k | Levels.fyi seed row + YC founding-eng equity band | Cash-in-bank |
| 2 | Founding full-stack engineer | Senior | Product | Design-partner #2 signed; parallel front-end work needed | Month +3 | $240k | Levels.fyi seed row | Cash-in-bank |
| 3 | Founding ML engineer | Staff | Product | ML pipeline (mod-103 exercise 01 "build" row) crosses "one person can maintain" threshold | Month +5 | $280k | Levels.fyi ML row + AI-native premium | Cash-in-bank |
| 4 | First platform / SRE engineer | Senior | Platform | On-call rotation reaches 5 engineers; incident MTTR crosses target | Month +8 | $240k | Levels.fyi SRE row | Series-A close |
| 5 | First engineering manager | EM | Product | Team reaches 6-8 ICs (mod-104 chapter 05 trigger) | Month +12 | $260k | Levels.fyi EM I row | Series-A close |
```

Two things about the shape:

- **Every row has a trigger.** The trigger is *the
  specific observable condition that makes this hire the
  right next hire*. "We need more engineers" is not a
  trigger. "The CTO's IC time dropped below 40% and code
  review is blocking merges by more than one business
  day" is.
- **Every row has a "contingent on" column.** The plan
  distinguishes hires the company can afford out of
  current cash from hires that only exist if the next
  raise closes. The board conversation is different for
  each, and blurring them is how founders end up making
  offers they cannot fund.

The plan also carries a **summary paragraph**:

- Total headcount added over the plan horizon.
- Total added annual burn (sum of fully-loaded costs).
- Resulting months-of-runway shift, assuming no revenue
  change and no raise close.
- The two or three sensitivity scenarios: what happens if
  the raise slips by a quarter, what happens if the two
  most expensive hires cannot be found in the target
  window, what happens if a specific customer commitment
  slips.

## Board-conversation shape

A board-defensible hiring plan survives at least four
questions from a competent board member. Rehearse them
before the meeting:

- **"Why this order?"** — the plan sequences the roadmap
  triggers, not the CTO's preferences. Point at the
  triggers and the roadmap linkage.
- **"What if you can't find the staff-level hire in that
  window?"** — the plan has a fallback. Either you hire
  two senior engineers instead of one staff engineer (with
  a named trade-off in code review and mentoring load), or
  the roadmap item that hire was for slips, and that slip
  is acknowledged rather than pretended away.
- **"What's the runway impact if the raise slips one
  quarter?"** — the plan tells you. The contingent hires
  either delay or come off the plan; the CTO knows in
  advance which ones.
- **"Who is doing the hiring?"** — the plan names the
  hiring manager per row. At seed this is the CTO for
  every row; at Series-A it may be the CTO for platform
  and the first EM for product. If the answer is "TBD",
  the plan is not ready.

The board member will not ask "have you thought about
diversity" as a fifth question the CTO surprises them with
in the meeting — the plan should reflect the sourcing
strategy that makes a diverse pipeline possible, and the
CTO should already have named the referral-network bias
this rules out (see chapter 02 on interview loop design;
narrow sourcing narrows the funnel and defaults the
pipeline to whoever the CTO's network already looks like).

## Failure modes

- **The base-only cost model.** The plan uses base salary
  as the per-engineer number. Actual burn is 1.3-1.5x
  higher, and the plan runs the company out of cash
  faster than the CEO thinks. Fix: use the fully-loaded
  multiplier, and get the CFO / fractional-CFO to confirm.
- **The unnamed-trigger plan.** Every row has a target
  start date but no trigger. The plan slides forward or
  backward as calendar time changes, but the *decision*
  about whether to hire never gets re-made. Fix: every
  row is trigger + date, and the trigger dominates when
  the calendar and the trigger disagree.
- **The one-archetype plan.** All five hires are the same
  archetype the CTO is comfortable working with. The
  roadmap requires three archetypes; the plan is not
  serving the roadmap. Fix: run the plan against the
  build-vs-buy matrix (see
  [`mod-103` chapter 01](../mod-103-build-vs-buy-and-platform-economics/01-build-vs-buy-as-portfolio-decision.md))
  and confirm each "build" row has an owner in the plan.
- **The hire-someone-who-can-do-everything plan.** The
  plan hires generalists at the point where the roadmap
  requires specialists (a security engineer, a data
  engineer, an ML platform engineer). Generalists at
  founding-engineer scale are correct (chapter 03); at
  Series-A scale a full generalist team fails to serve
  workstreams that require depth.
- **The plan-that-outruns-the-manager.** The plan grows
  the team past 6-8 ICs reporting to the CTO without
  hiring the first EM (chapter 05). The CTO becomes the
  bottleneck; morale and delivery both degrade. Fix: the
  first-EM row belongs in the plan, and its trigger is
  team-size + calendar-load, not "the CTO is tired".

## Summary

- A hiring plan is a **derived** artifact — derived from
  the technical roadmap (why these hires), the runway
  (can we afford them), and a funding-stage-appropriate
  comp band (at what price).
- The **fully-loaded per-engineer cost** — base plus
  employer taxes plus benefits plus equity expense plus
  ramp plus recruiting plus per-seat vendor cost — is
  typically **1.3-1.5x** base in the US. Use it, not
  base, in the plan's arithmetic.
- The output is a **one-page plan** with columns for
  role, seniority, team, trigger, target start, fully-
  loaded cost, comp-band source, and contingency; every
  row has an observable trigger and a named hiring
  manager.
- A defensible plan survives at least four board
  questions: why this order, what if we can't find the
  staff hire, what's the runway impact if the raise
  slips, and who is doing the hiring.
- The plan is a living artifact. Re-review at every
  monthly board update, and re-baseline at every stage
  transition per [`mod-101` chapter 04](../mod-101-cto-role-and-ownership-map/04-personal-stage-by-stage-self-development-plan.md)
  and [`mod-106`](../mod-106-scaling-org-and-stack/README.md)
  (the stage-transition playbooks).

The chapter's paired exercise —
[`exercise-01-hiring-plan-against-roadmap-and-runway.md`](exercises/exercise-01-hiring-plan-against-roadmap-and-runway.md)
— walks the authoring of the plan for your (or a real
reference) startup, including the fully-loaded number and
the two sensitivity scenarios the board will ask about.
The interview loop that fills each row is chapter 02; the
founding-engineer profile that the first three rows draw
against is chapter 03.
