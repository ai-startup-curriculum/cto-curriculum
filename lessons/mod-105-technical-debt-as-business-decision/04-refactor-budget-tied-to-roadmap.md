# The Refactor Budget Tied to the Roadmap

> "Engineers who work on features 100% of the time will
> eventually make the codebase impossible to work in.
> Engineers who work on refactoring 100% of the time will
> ship nothing. The org has to pick the split explicitly
> or the split gets picked implicitly, badly." — the
> operational version of Will Larson's *An Elegant
> Puzzle* framing on eng-time allocation
> ([lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/)).

## Motivation

Chapter 03 gave you the cost-to-carry number per debt
item. This chapter answers the follow-on question the
CEO will ask three seconds later: *"OK, so what
percentage of engineering time do you want to spend on
debt next quarter, and why that number and not a
different one?"*

The wrong answers:

- **"As much as we need to keep the codebase healthy."**
  Not a number; not defensible in a resource-allocation
  conversation.
- **"Google spends 20% on 20% projects, so we'll do
  that."** A cargo-culted number from a completely
  different context (Google's 20% is a *personal
  autonomy* time, not a debt-refactor budget); the
  CEO will notice.
- **"None until we ship the enterprise deal."** A
  political answer that trades a real interest bill
  for a fictional zero. Cost-to-carry does not become
  zero because you stop labelling it.

The right shape of answer:

- **"20% of engineering time next quarter, allocated
  against these three specific portfolio items whose
  cost-to-carry today already exceeds 24 hours/week
  in aggregate. Two of the three items are prerequisites
  for the enterprise SSO commitment; one is a stop-
  loss on the on-call load. Here's the trade-off — we
  drop these two feature commitments to make room, and
  here's why that trade is the right one."**

That answer is a *budget* — a percentage, a set of line
items it is allocated against, a set of feature trade-
offs it displaces, and a business owner who signs off. It
is the artifact this chapter walks the authoring of.

## Why a budget, not a project

Two shapes exist for debt work:

- **The one-shot project.** *"We're going to have a two-
  quarter refactor initiative and then we'll be done."*
  This shape almost never works. The refactor initiative
  competes head-to-head with feature work, loses the
  political fight the moment a customer commitment
  shifts, and ends inconclusively with the codebase in
  a *worse* state than before (half migrated to the new
  shape, half still on the old shape).
- **The recurring budget.** *"20% of engineering time,
  every quarter, allocated against a portfolio the CTO
  publishes."* This shape works because it is *always
  on*. It handles the depreciation curve (chapter 03)
  as it rises; it is not vulnerable to a single
  quarter's feature pressure; the portfolio evolves as
  items get paid down and new items get incurred.

The budget frame is also easier to sell to a board
because it maps to something they already understand: a
recurring OpEx line (like on-call cost, or SaaS spend, or
the observability bill), not a one-off capital project.
Boards approve recurring lines against a rate; they
scrutinise one-off projects against an outcome. The debt
work performs poorly under outcome scrutiny (you rarely
get to "done" — you get to "handled") and performs well
under rate scrutiny.

## The 20% rule — one shape, not the only shape

The 20% number appears in the field enough to be worth
naming; it also gets misused enough to need un-naming.

Where the number does *not* come from:

- **Google's 20% time** (announced in the S-1;
  discussed publicly for years) is time engineers can
  spend on projects of their own choosing. It is a
  *personal-autonomy* mechanism, not a debt-refactor
  budget. Do not conflate them; the CEO who has read
  the Google references will notice.

Where the number *does* come from:

- **Practitioner default.** Multiple engineering-
  leadership references converge on "a large minority
  of engineering time" — typically 15-25% — as the
  sustainable rate at which debt can be repaid without
  the org grinding to a halt. Will Larson's *An
  Elegant Puzzle*
  ([lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/))
  discusses systems for allocating engineering time
  against multiple categories (features, debt,
  operational load, on-call, meetings) and defends the
  discipline of *explicit* allocation. Michael Feathers's
  *Working Effectively with Legacy Code*
  ([informit.com — Feathers WELC](https://www.informit.com/store/working-effectively-with-legacy-code-9780131177055))
  documents the empirical reality that legacy
  refactoring proceeds at a fraction of feature-work
  velocity — the fraction that the 15-25% band
  approximates.

The number the CTO defends in the board room is
whichever percentage the portfolio's aggregate cost-to-
carry (chapter 03) actually justifies. **20% is a shape,
not a law.** Some quarters it is 30% (a compliance
deadline is forcing security-debt repayment; a load-
bearing subsystem's cost-to-carry has crossed a
threshold). Some quarters it is 10% (the portfolio is in
a maintenance state; the aggregate cost-to-carry has
been paid down; feature velocity is being spent for a
specific launch). What matters is that the number is
**pinned to the portfolio** and **defended against the
roadmap**.

## Deriving the budget from the portfolio

The mechanical version of the derivation, per quarter:

- Sum the top-N items' cost-to-carry from chapter 03
  (say, N = 6-10 items — the portfolio you actually
  want to move on).
- Compare the aggregate to the team's total
  engineering-hours available in the quarter.
- The ratio is a floor for the quarter's debt budget
  — spending less than that ratio means the debt is
  compounding faster than you are paying it.
- Add the *fix* effort for the highest-priority
  subset of items you plan to move on — the ones with
  a business owner (below) and a StranglerFig plan
  (chapter 05).
- The sum of "the interest you're paying anyway" plus
  "the principal repayment you plan to do this
  quarter" is the budget.

For a 10-engineer team with 400 available engineer-hours
per week (10 × 40, minus meetings / on-call / support —
roughly 65-75% of nominal is a realistic default;
Rands's *Rands In Repose* essays touch this
[randsinrepose.com](https://randsinrepose.com/)) and a
portfolio whose aggregate cost-to-carry is ~40
hours/week, you are already spending 10% *unbudgeted* on
carry. Adding 8-10% for principal repayment gets you to
~18-20% total, which is the shape the "20% rule" arrives
at from below.

That derivation is the paragraph the CFO wants
underneath the "20%" headline number in the plan. It
converts the number from "a rule I read about" to "a
calculation I can dispute row by row."

## Every line item needs a business owner

The single largest failure mode of debt work in startups
is that the debt has an *engineering* owner (the CTO or
a tech lead) but no *business* owner. The debt then
loses every prioritisation conversation, because
engineering owners are perceived to be arguing for their
own convenience.

The fix: each portfolio item's inventory row
(chapter 06) has a **business owner** column, and the
business owner is not the CTO. It is the person on
the business side whose commitment is unblocked when
the debt is paid:

- The **enterprise SSO commitment** to Sales — the
  owner is the Head of Sales (or the CEO acting as
  Sales at pre-Series-A).
- The **SOC 2 Type I readiness** commitment — the
  owner is whoever the CEO / board designated as
  compliance lead (typically the CEO at pre-Series-A;
  see [`mod-107` chapter 01](../mod-107-founder-scope-security-and-compliance/README.md)).
- The **onboarding-time reduction** that unblocks the
  hiring plan — the owner is the CTO acting in their
  *organisational-scaling* capacity (see
  [`mod-104` chapter 01](../mod-104-first-engineering-hires-and-team-topology/01-hiring-plan-against-roadmap-and-runway.md)),
  not the CTO acting in their engineering-lead
  capacity — those are two different hats.
- The **compliance audit gap** — the owner is the
  business function that will be blocked without the
  audit; sales into regulated segments is the
  archetypal case.

When the debt item has no plausible business owner —
nobody on the business side benefits from paying it
down — the item is *engineering-aesthetic* debt, not
business-relevant debt. The response is either to leave
it and pay the carry cost, or to formally deprecate the
feature it supports (chapter 05). Do not fight for
budget to repay it.

## The two things the budget is authored against

The refactor budget is authored against **two** external
artifacts:

- **The roadmap.** Every dollar of debt budget is a
  dollar not spent on a feature. The plan makes the
  trade explicit: *"this budget requires us to move
  feature X from Q3 to Q4; Y from Q4 to Q1"*.
  Concealing that trade is how debt work gets clawed
  back mid-quarter when a customer commitment shifts.
  See [`mod-102` chapter 01](../mod-102-architecture-under-uncertainty/01-monolith-first-and-evolutionary-architecture.md)
  on the evolutionary posture the roadmap is planned
  from.
- **The hiring plan.** Debt work absorbs the same
  engineering-hours the hiring plan (see
  [`mod-104` chapter 01](../mod-104-first-engineering-hires-and-team-topology/01-hiring-plan-against-roadmap-and-runway.md))
  is planning to grow. If the plan projects team-size
  compounding as the dominant depreciation driver
  (chapter 03), the hiring plan *needs* the debt work
  to succeed — every new hire onto a compounding-tax
  subsystem is a compounder itself. Say so in the
  narrative.

The board-ready framing that ties these together: *"The
refactor budget for next quarter is 22% of engineering-
hours. That is derived from the portfolio's aggregate
cost-to-carry (currently 55 hours/week — 14% of
capacity) plus the planned principal repayment on three
specific items (an additional 8% of capacity). The three
items have business owners X, Y, Z. The trade-offs on
the roadmap are these two feature moves; the hiring plan
is unchanged because two of the three items are
prerequisites for the two hires slated onto that
subsystem in month +2."*

## The Google eng-productivity framing

*Software Engineering at Google*
([abseil.io/resources/swe-book](https://abseil.io/resources/swe-book))
uses a slightly different vocabulary — engineering
productivity, sustainable software engineering — but
the underlying model is the same: engineering time is a
finite budget allocated across categories with different
half-lives, and the org that fails to allocate
explicitly ends up defaulting to a bad allocation. If
your organisation reads that book, cite it as the shared
vocabulary; if it doesn't, cite Will Larson's *An
Elegant Puzzle*
([lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/))
which is more compact and startup-scale-appropriate.

## Two things the budget is NOT

- **A punishment.** Some CTOs treat the debt budget as
  penance for having taken on the debt in the first
  place, and set the number high enough that feature
  velocity suffers as a form of moral atonement. The
  board reads this as unforced weakness. Set the
  number against the portfolio math and defend it that
  way; the past decision to take the debt was
  usually correct (Cunningham's original loan,
  chapter 01) and does not need atoning for.
- **A permanent floor.** Some CTOs, having negotiated
  the 20% number once, treat it as a floor they never
  revisit. The portfolio changes; the ratio should
  change. Publish the derivation every quarter; if
  the aggregate cost-to-carry has fallen because of
  repayment, the budget shrinks and that is a *win*
  to celebrate — a signal that the debt discipline is
  working.

## Failure modes

- **The debt-as-slack budget.** The budget is not
  allocated against specific portfolio items — it is
  a "20% slack" allocation the team can spend on
  whatever debt they feel like. The result is that
  everyone works on their own aesthetic preferences
  and the portfolio's high-cost-to-carry items get
  no attention. Fix: allocate against named items,
  each with a business owner and a plan.
- **The unaudited budget.** The CTO negotiated 20%
  three quarters ago and has not re-derived it since.
  Everyone assumes debt is being paid down; nobody
  is looking at the portfolio's cost-to-carry
  trend. Fix: publish the derivation every quarter;
  make it a rolling artifact, not a one-time
  negotiation.
- **The one-shot rewrite dressed up as a budget.**
  The "budget" is actually a single two-quarter
  refactor initiative. The moment a customer
  commitment shifts, the initiative gets pulled;
  the refactor half-lands; the codebase is worse
  than before. Fix: the budget is a *rate*, not a
  project; the portfolio changes as items land, but
  the rate persists.
- **The engineering-only-owner budget.** Every
  portfolio item's owner is the CTO or a tech lead.
  In the first roadmap conflict, every item loses
  the prioritisation vote. Fix: name a business
  owner per item; walk the item off the portfolio
  if none can be identified.
- **The cover-for-a-rewrite budget.** The 20% figure
  is negotiated to fund a rewrite the CTO has already
  committed to in their head. The portfolio is
  reverse-engineered from the desired rewrite. The
  board eventually notices. Fix: derive the number
  from the portfolio, not the portfolio from the
  number.

## Summary

- The refactor budget is a **recurring rate** of
  engineering time (typically 15-25% at pre-Series-A
  scale; **20% is a shape, not a law**) allocated
  against a **named portfolio** of debt items, each
  with a **business owner**.
- The rate is **derived** from the portfolio's
  aggregate cost-to-carry (chapter 03) plus the
  planned principal repayment on the highest-
  priority items; it is not a number imported from
  another company or borrowed from Google's 20%
  personal-autonomy time (which is a different
  mechanism).
- Every line item **must have a business owner**
  who benefits when the debt is paid down. Items
  without a business owner are engineering-aesthetic
  and lose every prioritisation vote — either
  deprecate the underlying feature (chapter 05) or
  pay the carry cost explicitly.
- The budget is authored **against the roadmap and
  the hiring plan**. The trade-offs (feature moves,
  hiring implications) are stated up front, not
  concealed.
- The budget is a **rate**, not a **project**.
  One-shot refactor initiatives lose the political
  fight and leave the codebase half-migrated.
- Failure modes: debt-as-slack, unaudited budget,
  one-shot rewrite dressed up as a budget,
  engineering-only-owner budget, cover-for-a-
  rewrite budget.

The chapter's paired exercise —
[`exercise-03-refactor-budget-tied-to-roadmap-drill.md`](exercises/exercise-03-refactor-budget-tied-to-roadmap-drill.md)
— walks the derivation of the budget for your (or a
real reference) startup, including the roadmap trade-
offs the budget forces and the business owner named
per item. Chapter 05 handles the *per-item* decision of
deprecate vs. rewrite vs. leave; chapter 06 formats the
whole thing as the portfolio + decision log a board
member can read.
