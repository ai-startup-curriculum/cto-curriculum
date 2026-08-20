# Exercise 02 — Cost-to-Carry Sizing for Five Debt Items

**Module:** `mod-105-technical-debt-as-business-decision`
**Planned time:** ~3 hours
**Chapter this builds on:** [`03-cost-to-carry-and-depreciation-schedule.md`](../03-cost-to-carry-and-depreciation-schedule.md),
building on the categorised items from
[`exercise-01`](exercise-01-fowler-quadrant-categorisation-drill.md).

## Problem statement

For **five debt items** — drawn from your exercise-01
categorised list — size the **cost-to-carry (now)** and
the **depreciation schedule** so that each item becomes
a portfolio line you could defend to a CFO row by row.

The point of the drill is not to publish finance-grade
numbers. It is to convert *"a mess"* into *"~8
engineering-hours per week today, ~14 by end of Q3,
dominant compounder is team-size"* — the shape of
statement that lets the debt be compared against other
uses of engineering time on a like-for-like axis.

## Requirements

Author a Markdown document at `docs/tech-debt/cost-to-
carry.md` (or the equivalent in your working repo).

### The five sized items

For **each** of the five items:

- **The item header**: ID (from exercise 01 if you
  used numbering there), Title, Fowler quadrant,
  Family (with ISO/IEC 25010 characteristic or
  structural shape named — carry the labels forward
  from exercise 01).
- **The six-source sizing** (chapter 03). For
  **each** source, either give an hours-per-week
  number (rounded generously) or state explicitly
  that it does not apply and why:
  1. **Workaround tax** — hours/week the team spends
     on the workarounds (extra tests, extra QA,
     extra review comments, extra hand-offs, extra
     deploy safeguards). Cite the median-of-three
     estimate (below).
  2. **On-call tax** — incidents in the last two
     quarters that traced to this item; hours per
     incident on average; hours/week when
     annualised. Add a standby premium (chapter 03
     rule of thumb: +10-25%).
  3. **Onboarding tax** — extra days per new hire to
     become productive near this item; multiplied by
     new hires per quarter; divided by weeks per
     quarter.
  4. **Lead-time tax** — the DORA Lead Time /
     Change Failure Rate delta on debt-touching
     modules vs. the team baseline (see [dora.dev](https://dora.dev/)).
     If you have no DORA telemetry, state so and
     use an order-of-magnitude estimate; do not skip
     the row.
  5. **Feature-slip tax** — features you cannot
     ship at all until this debt is paid; quantified
     as "the two-week feature becomes a three-month
     project" or similar. Not hours/week directly;
     name the delta in shipping timeline.
  6. **Morale / attrition tax** — qualitative flag
     (yes / no / possibly) with a one-line
     evidence. Do not put a number here; it is a
     People / Governance number, not yours (see
     [startup-operations-governance-curriculum](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum)).
- **The aggregate cost-to-carry (now)** — sum of
  the numeric sources, rounded, expressed as
  engineering-hours per week. Add the qualitative
  flags below the number.
- **The depreciation schedule** — a 2-4 quarter
  projection. State the dominant compounder (team-
  size / codebase-size / turnover / adjacent-
  decision) and *why* it dominates for this item.
  Give the projected cost-to-carry at each of the
  next two quarter-ends.
- **The median-of-three note** — one line naming
  the three engineers who estimated (initials or
  roles are fine — *"CTO, tech lead A, backend
  engineer B"*) and any wide disagreement worth
  flagging (a 3× spread in estimates is data; write
  it down).

### The summary table

After the five items, produce a **summary table** with
one row per item and columns:

- ID.
- Title (short).
- Cost-to-carry (now).
- Cost-to-carry (projected, end of quarter +2).
- Dominant compounder.
- Portfolio band (chapter 03 convention: `< 2 h/wk` /
  `2-8` / `8-20` / `> 20`).

### The narrative paragraph

Below the summary table, write a **200-400 word
paragraph** answering:

- **Aggregate cost-to-carry (now)** for the five
  items, expressed as hours/week AND as percentage
  of team capacity (use ~65-75% of nominal team-
  size × 40 as your capacity denominator; state the
  denominator you used).
- **Aggregate projected cost-to-carry (quarter +2)**,
  same units.
- **The rise (percentage points)** the aggregate is
  projected to gain, and which items dominate the
  rise.
- **The two items** whose depreciation curve most
  demands a plan in the next quarter. Do not
  propose the plan (that is exercise 04); just name
  the two items and the reason.
- **The one qualitative flag** (morale / attrition
  / customer-perception) you would want the CEO to
  weigh in on. Name it.

## Starter guidance

- **Do not solo-estimate.** Chapter 03's median-of-
  three protocol is the *whole point* of the drill.
  The solo estimate under-counts every category and
  the CFO / board will spot it. Book two 30-minute
  conversations with engineers who work near the
  debt; get their independent hours-per-week
  estimates; take the median.
- **Do not skip DORA even if you don't have it.**
  If you have no telemetry for Lead Time / Change
  Failure Rate, state so — *"no DORA telemetry;
  estimating from PR-cycle-time samples over Q1"*
  — and put a number down. A missing row is
  invisible; an approximate row is a starting
  point. See mod-106 chapter 05 for the DORA
  baseline the org should be moving toward
  ([dora.dev](https://dora.dev/)).
- **Do not publish a dollar-per-year figure.** The
  drill's output is hours-per-week. If your CFO
  wants a dollar, they can multiply by the loaded
  cost from mod-104 chapter 01; do not do the
  multiplication yourself unless the CFO co-owns
  the multiplier. See the chapter-03 failure mode
  on this.
- **Do not publish a "fix ROI" figure either.** The
  fix costs are exercise-04 territory. Publishing
  ROI up front creates false precision and
  encourages the CEO to demand ROI on every future
  refactor at a level of accuracy the discipline
  cannot support.
- **Round generously.** These are order-of-
  magnitude numbers. *"~8 hours/week"* not *"7.6
  hours/week"*. Precision is a false-confidence
  signal; the CFO knows.
- **Name the dominant compounder per item.** The
  four options (team-size, codebase-size, turnover,
  adjacent-decision) are from chapter 03. Every
  item should have exactly one dominant driver
  named; if you cannot pick one, the projection is
  probably wrong.
- **Flat depreciation is a warning sign.** If
  every item's projected cost-to-carry equals the
  current cost-to-carry, you have not thought about
  the compounders. Chapter 03's failure mode list
  calls this out.
- **The morale / attrition flag is qualitative.**
  Do not attempt to size it in hours; a
  yes/possibly/no flag with a one-line evidence is
  the right output. Cite the People lead as the
  authoritative source for the dollar version.
- **Cite Cunningham 1992** for the interest-rate
  framing:
  [`c2.com/doc/oopsla92.html`](http://c2.com/doc/oopsla92.html).
  Cite chapter 03's four-compounder list when
  defending the projection.

## Acceptance criteria

The drill output is complete when:

- Five items have each been sized against the six
  sources, with the median-of-three protocol
  applied (and the three estimators named).
- Each item has an aggregate cost-to-carry (now),
  a projected cost-to-carry (quarter +2), and a
  named dominant compounder — no flat depreciation
  curves without a defence.
- The summary table has the five rows and the
  columns listed above; the portfolio-band label
  is applied per item.
- The narrative paragraph reports aggregate
  hours-per-week AND aggregate percentage of team
  capacity, with the capacity denominator stated
  explicitly.
- The two items most demanding a next-quarter plan
  are named; the one qualitative flag requiring
  CEO input is named.
- A CFO / fractional CFO reader can look at the
  summary and compute their own dollar figure if
  they wish; a reader without CFO context can
  understand the hours-per-week story on its own.

## What this feeds into

- **Exercise 03** — the refactor budget is derived
  from the aggregate cost-to-carry sized here.
- **Exercise 04** — the deprecate-vs-rewrite-vs-
  leave decision is per-item; the sizing here is
  input.
- **Exercise 05** — the full inventory's
  `Cost-to-carry` and `Depreciation` columns are
  populated from this drill.
- **Lab 01** — the portfolio decision log the lab
  publishes builds on the sized portfolio.
- **Capstones** — the debt-portfolio sections of
  [`project-102`](../../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package/)
  and
  [`project-103`](../../../projects/project-103-scaling-plan-from-five-to-fifty-engineers/)
  reuse the sized items.

The drill is *deliberately* five items rather than the
full portfolio because the discipline you are
practicing — the median-of-three protocol, the
six-source addition, the depreciation projection —
takes 30-45 minutes per item to do well. Five is
enough to build the muscle; the full portfolio (10-15
items) is exercise 05 / lab 01 territory.
