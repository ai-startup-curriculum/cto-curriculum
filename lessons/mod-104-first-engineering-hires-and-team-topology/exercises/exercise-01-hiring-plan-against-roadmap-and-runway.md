# Exercise 01 — Hiring Plan Against Roadmap and Runway

**Module:** `mod-104-first-engineering-hires-and-team-topology`
**Planned time:** ~3 hours
**Chapter this builds on:** [`01-hiring-plan-against-roadmap-and-runway.md`](../01-hiring-plan-against-roadmap-and-runway.md)

## Problem statement

Author a **one-page hiring plan** for the next twelve
months of your (or a real reference) startup that
would survive a board conversation about **runway** and
**hiring pace**. The plan must be pinned to the
technical roadmap (why *these* hires and not others),
to the current runway (can we afford them), and to a
funding-stage-appropriate compensation band (at what
price), and must use a **fully-loaded per-engineer
cost** — not base salary — in its arithmetic.

The point of the drill is not to fill in a template. It
is to convert an implicit "we should hire soon" into an
explicit, defensible sequence that names the trigger for
each role, the cost per year, and the contingency if the
next raise slips a quarter.

## Requirements

Produce a **one-page hiring plan** (roughly one screen
when rendered), plus a **short summary paragraph** on
the runway impact and the two sensitivity scenarios the
board is likely to press on.

### The plan itself

- **Between 4 and 8 rows.** Each row is one role. Fewer
  than 4 is under-planning at seed / Series-A; more
  than 8 in twelve months is either an unusually well-
  funded startup (in which case say so) or an
  unrealistic pace.
- **Every row must include** all of the following
  columns; do not drop any:
  - `#` — the target hire order.
  - `Role` — the noun; be specific ("senior back-end
    engineer with distributed-systems depth", not
    "engineer").
  - `Seniority` — a level on your (or a plausible
    placeholder) career ladder — see chapter 06.
  - `Team` — the team this hire joins, per the topology
    of the target stage (see [`chapter 04`](../04-team-topologies-at-startup-scale.md)).
  - `Trigger (roadmap item / signal)` — the specific,
    observable condition that makes this hire the right
    next hire. "We need more capacity" is not a trigger.
    "CTO IC time drops below 40% for two consecutive
    weeks and code-review lead time exceeds one business
    day" is.
  - `Target start` — a month offset from today (e.g.
    "month +5"), not a calendar date; the plan is
    trigger-driven, not calendar-driven.
  - `Fully-loaded cost / year` — using the fully-loaded
    multiplier from chapter 01 (typically 1.3-1.5x base
    in the US); note the multiplier you used and the
    source you got it from.
  - `Comp band source` — the public reference the base
    and equity are pulled from — e.g. Levels.fyi,
    Pave, Carta, Index Ventures Option Plan.
  - `Contingent on` — cash-in-bank, next-raise close,
    a specific customer commitment, or a specific
    other hire being made first.
  - `Hiring manager` — the person who owns the loop
    for this role. If it is "TBD", the row is not
    ready.

### The summary paragraph

After the table, write **200-500 words** that answer:

- **Total added burn per year** — the sum of the
  fully-loaded costs.
- **Resulting months-of-runway shift** — assuming no
  revenue change and no raise, how many months of
  runway does this plan consume?
- **Sensitivity scenario A — raise slips one quarter.**
  Which rows come off the plan? Which move to a later
  target start? What happens to the roadmap items
  those rows were the answer to?
- **Sensitivity scenario B — you cannot find the two
  most senior hires inside the target window.** What
  is the fallback? (Two mid-senior hires? Roadmap
  slip? Delayed platform investment?)
- **The specific board question you are most nervous
  about.** Name it, and note the answer you would give
  today.

### Format and location

Author the plan as a Markdown table in a real repo, in
a `docs/hiring/hiring-plan.md` or equivalent path. The
summary paragraph belongs in the same file, below the
table.

The plan is a *living* artifact. Add a `Version: v0`
and today's date at the top; add a `Next review:`
date one month out. The plan is intended to be re-read
at every monthly board update.

## Starter guidance

- **Base is not the cost.** If your plan's per-row
  cost is the base salary, redo the arithmetic. The
  fully-loaded multiplier (typically 1.3-1.5x in the
  US) must be applied and cited.
- **Do not invent numbers you cannot verify.** If you
  do not know your current burn, write `<burn: CFO to
  confirm; using $X placeholder>`; do not guess. If
  you do not know the current comp band from a public
  reference, write `<comp: Levels.fyi / Pave lookup
  pending>` and use a placeholder.
- **Anchor each hire to the roadmap.** The trigger
  column should reference a specific roadmap item
  (customer commitment, compliance milestone, scale
  threshold, build-vs-buy row from [`mod-103`
  exercise 01](../../mod-103-build-vs-buy-and-platform-economics/exercises/exercise-01-build-vs-buy-matrix-for-five-real-choices.md))
  or a specific engineering-operations signal (CTO
  calendar composition, code-review lead time, on-call
  load).
- **Distinguish cash-in-bank hires from raise-
  contingent hires.** Every row's `Contingent on`
  column should be explicit. Blurring the two is how
  offer letters go out that cannot be funded.
- **Name the hiring manager.** At founding-team scale
  it is the CTO for every row; that is fine, but write
  it down. At Series-A the first EM (chapter 05) will
  own some rows; note the split.
- **Do not put all founding-engineer archetypes in
  the plan.** By hire #4 or #5 the roadmap requires
  specialists — a data engineer, a security engineer,
  a first platform / SRE — not five more T-shaped
  generalists. Use chapter 04's topology to steer the
  specialism mix.
- **Include the first-EM row** (chapter 05) if the
  team crosses 6-8 direct reports to the CTO inside
  the plan horizon. Skipping it is the most common
  omission at the seed → Series-A transition.
- The exercise composes with — but does not require —
  the [`mod-102` exercise 02 ADR set](../../mod-102-architecture-under-uncertainty/exercises/exercise-02-adr-authoring-for-three-real-decisions.md)
  and the [`mod-103` exercise 01 matrix](../../mod-103-build-vs-buy-and-platform-economics/exercises/exercise-01-build-vs-buy-matrix-for-five-real-choices.md).
  If either is authored, use it as the source for
  which "build" rows have hiring consequences.

## Acceptance criteria

Your plan is complete when a reader (co-founder,
first EM, technical advisor, or first-round investor)
can:

- Read the table and understand the twelve-month
  sequence of hires, why each is next, and what
  triggers each — without asking a follow-up
  question.
- Identify at a glance which rows the company can
  afford out of current cash and which are contingent
  on the next raise closing.
- Sum the fully-loaded costs and reproduce your
  runway-shift number.
- Read the two sensitivity paragraphs and see that
  the plan has thought about what happens when the
  world doesn't cooperate.
- Cross-reference the plan to at least one roadmap
  item (customer commitment, compliance milestone,
  build-vs-buy row) per hire — no orphan rows.
- Identify the hiring manager for each row; no "TBD"
  entries in that column.

The output of this exercise feeds directly into every
subsequent exercise in this module:

- Exercise 02 authors the interview loop that fills
  the earliest role in the plan.
- Exercise 03 authors the founding-engineer profile
  that the first three rows draw against.
- Exercise 04 draws the topology the plan populates.
- Exercise 05 runs the promote-vs-hire drill for the
  first-EM row.
- Exercise 06 authors the ladder and comp band the
  plan's `Seniority` and `Fully-loaded cost` columns
  reference.

The plan also becomes an artifact in the capstone
[`project-101`](../../../projects/project-101-first-year-technical-strategy-for-one-seed-startup)
first-year technical-strategy package.
