# Exercise 03 — Refactor Budget Tied to Roadmap Drill

**Module:** `mod-105-technical-debt-as-business-decision`
**Planned time:** ~3 hours
**Chapter this builds on:** [`04-refactor-budget-tied-to-roadmap.md`](../04-refactor-budget-tied-to-roadmap.md),
building on [`exercise-02`](exercise-02-cost-to-carry-sizing-for-five-debt-items.md)
(which produced the sized portfolio) and referencing
[`mod-104` exercise 01](../../mod-104-first-engineering-hires-and-team-topology/exercises/exercise-01-hiring-plan-against-roadmap-and-runway.md)
(the hiring plan the budget interacts with).

## Problem statement

Derive a **defensible refactor budget** for the next
quarter for your (or a real reference) startup,
expressed as a **percentage of engineering time**,
allocated against **named portfolio items each with a
business owner**, and pinned to the **specific roadmap
trade-offs** it forces.

The point is to convert an implicit "we should spend
some time on refactoring" into an explicit rate that
(i) the CEO can defend to the board as a recurring
line, (ii) the engineering leads can defend to their
teams as a stable expectation, and (iii) a technical-
due-diligence reviewer can read as evidence of
portfolio discipline.

The 20% number is *not* the target. The **derivation
is the target** — the number falls out of the portfolio
math from exercise 02 plus the principal-repayment
plan for the highest-priority items. Some quarters
that will be 12%; some quarters 25%.

## Requirements

Author a Markdown document at `docs/tech-debt/refactor-
budget-Q<N>.md` (or the equivalent in your working
repo).

### The five sections

- **Section 1 — the portfolio input.** A short
  restatement (a table) of the sized items from
  exercise 02 that will be *considered* for this
  quarter's budget: ID, Title, cost-to-carry (now),
  cost-to-carry (projected end-of-quarter), business-
  owner candidate. Typically 5-8 items; the whole
  portfolio if you have <10, or the top-N by
  aggregate compounding rate if you have more.
- **Section 2 — the arithmetic derivation.** Show
  the math, per chapter 04's derivation:
  - Team-size and available engineering-hours per
    week (state the capacity multiplier — typically
    65-75% of nominal team-size × 40 — and cite the
    source; Will Larson's *An Elegant Puzzle*
    ([lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/))
    is one useful reference).
  - Aggregate cost-to-carry (now) as a percentage of
    capacity. This is your *floor* — the interest
    you are paying anyway.
  - Planned principal-repayment effort for the top-
    priority subset of items you want to move on this
    quarter — how many engineer-hours the fix
    (StranglerFig migration, security-debt sprint,
    onboarding-doc buildout, etc.) will consume.
  - Sum expressed as a percentage → **this
    quarter's proposed refactor budget**.
- **Section 3 — the per-item allocation.** A table
  showing which portfolio items get the budget:
  - ID + Title.
  - Business owner (per chapter 04; if empty, the
    item is a candidate for deprecation and does
    not get budget).
  - Allocated engineer-hours (or an FTE-equivalent
    over the quarter — e.g. *"0.5 FTE for 4
    weeks"*).
  - Expected cost-to-carry post-work.
  - Response type (Deprecate / Rewrite / Leave —
    even if exercise 04 hasn't been done formally
    yet, name the intended response).
- **Section 4 — the roadmap trade-offs.** State the
  trade explicitly:
  - **Feature moves.** Which roadmap items move to
    later quarters (or come off the plan) to make
    room for this budget? Two or three specific
    items; cite the roadmap version they came from.
  - **Hiring interactions.** Which hiring-plan rows
    (mod-104 exercise 01) *depend on* the refactor
    budget being spent? Which are potentially
    *displaced* if the budget grows further?
    Typically the depreciation-compounder items
    (chapter 03) show up here — a debt item whose
    dominant compounder is team-size is a debt
    the hiring plan needs paid down.
  - **Non-goals.** State what this budget explicitly
    is *not* buying: engineering-aesthetic
    rewrites, pet projects, "we might need it later"
    speculative work.
- **Section 5 — the board-facing paragraph.** A
  **150-300 word paragraph** the CEO can drop into
  the board pre-read. Must contain:
  - The proposed budget as a percentage of
    engineering time for the next quarter.
  - The derivation (aggregate cost-to-carry X% +
    principal repayment Y% = budget Z%).
  - The three named highest-priority items and
    their business owners.
  - The two-or-three roadmap trade-offs the budget
    forces.
  - The alternative you are *not* pursuing (the
    lower-budget scenario) and why.

## Starter guidance

- **Do NOT reach for 20% as the number first.**
  Chapter 04 explicitly warns against this — the
  20% figure is a *shape*, not a law, and starting
  from the number rather than deriving it produces
  a portfolio that is reverse-engineered to justify
  the number. Derive first, then compare.
- **Cite the derivation math**, do not gesture at
  it. The CEO / board / technical-DD reader will
  ask *"why 22% and not 17?"* — the answer is the
  arithmetic in Section 2, not "I think that
  feels right".
- **Every allocated item must have a business
  owner in Section 3.** Chapter 04's non-negotiable
  discipline. If a row's business owner is *"CTO"*,
  either identify a real non-engineering owner, or
  route the item to deprecation (chapter 05), or
  accept it is engineering-aesthetic and take it
  off the budget.
- **Do NOT bundle multiple items into a single
  slot.** *"20% for tech debt"* is not an
  allocation. *"5% for DEBT-0007 billing rewrite;
  8% for DEBT-0002 security debt (SOC 2 Type I
  path — mod-107); 4% for DEBT-0004 onboarding doc
  buildout; 3% reserve for unplanned"* is.
- **State the roadmap version.** *"Feature X moves
  from Q3 to Q4 per roadmap v2026-08"* — this
  makes the trade auditable when someone re-opens
  the conversation in three months.
- **Include the hiring-plan interaction.** Chapter
  04's most-under-cited link. If the hiring plan
  is loading three hires onto the billing subsystem
  in Q2 and the billing subsystem's dominant
  compounder is team-size, the two artifacts are
  fighting each other; the budget conversation
  should call this out.
- **Do NOT propose a project.** Chapter 04's
  emphasis: the budget is a *rate*, not a *project*.
  If Section 5 reads like a project charter (single
  outcome, single deadline, single big-bang
  deliverable), redraft as a recurring allocation
  that survives a customer commitment shift.
- **Cite the sources.** Chapter 04's Will Larson
  reference
  ([lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/)),
  the DORA baseline
  ([dora.dev](https://dora.dev/)) for the delivery-
  cadence context, and *Software Engineering at
  Google*'s "programming integrated over time"
  chapter
  ([abseil.io/resources/swe-book](https://abseil.io/resources/swe-book))
  are the three references worth including as
  citations.

## Acceptance criteria

The budget is complete when:

- Section 1 restates the sized portfolio (drawn
  from exercise 02) — no new items are introduced
  here without sizing.
- Section 2 shows the arithmetic derivation —
  capacity, aggregate-carry, planned repayment,
  total — and a defensible percentage falls out.
- Section 3 allocates the budget to named items,
  each with a real business owner (not "CTO").
- Section 4 states the specific feature moves and
  the hiring-plan interactions the budget forces.
- Section 5 is a 150-300 word paragraph the CEO
  can drop into a board pre-read verbatim — it
  contains the number, the derivation, the three
  priorities, and the trade-offs.
- A reader (CEO, CFO, board member, incoming VP
  Eng) can look at the document and *dispute row
  by row* — that is what "defensible" means. The
  budget is not "trust me"; it is a set of numbers
  and choices any of which is legitimately
  disputable.
- The document is dated and version-numbered; it is
  a rolling artifact rewritten each quarter, not a
  one-time deliverable.

## What this feeds into

- **Exercise 04** — the deprecate-vs-rewrite-vs-
  leave per-item decision uses the budget as
  input: items that get budget are candidates for
  Rewrite (Chesterton's Fence + StranglerFig);
  items with no business owner are candidates for
  Deprecate; items whose cost-to-carry is real but
  whose depreciation curve is flat are candidates
  for Leave.
- **Exercise 05** — the full inventory row's
  `Response`, `Plan`, and business-owner columns
  are populated from this budget's decisions.
- **Lab 01** — the published portfolio decision log
  includes this budget as its `BUDGET-<quarter>`
  decision record.
- **Capstones** — the debt-portfolio sections of
  [`project-102`](../../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package/)
  and
  [`project-103`](../../../projects/project-103-scaling-plan-from-five-to-fifty-engineers/)
  use this format for the recurring quarterly
  refactor budget.

The drill is one quarter; the discipline is recurring.
Every quarter you re-run the derivation, the portfolio
shifts as items get paid down or new ones get incurred,
and the number moves. That movement — up when the
compounders are winning, down when the discipline is
holding — is the healthiest signal a debt portfolio
can give.
