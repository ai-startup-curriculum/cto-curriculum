# Exercise 01 — Fowler Quadrant Categorisation Drill

**Module:** `mod-105-technical-debt-as-business-decision`
**Planned time:** ~2 hours
**Chapter this builds on:** [`01-cunningham-metaphor-and-fowler-quadrants.md`](../01-cunningham-metaphor-and-fowler-quadrants.md),
supported by [`02-quality-attribute-vs-structural-debt.md`](../02-quality-attribute-vs-structural-debt.md)

## Problem statement

Pick **ten real debt items** — from your own codebase if
you are running a startup, or from a reference codebase
(an open-source project you know well, a system a
previous employer ran, a well-documented
retrospective / post-mortem writeup you can cite). For
each item, produce a **short row** that assigns:

- the **Fowler quadrant** (chapter 01) — Deliberate-
  Prudent / Deliberate-Reckless / Inadvertent-Prudent /
  Inadvertent-Reckless,
- the **family** (chapter 02) — Quality-attribute
  (with the ISO/IEC 25010 characteristic named) or
  Structural (with the shape of misfit named),
- a **one-line evidence** for the quadrant call — what
  did you observe or hear that put the item in that
  cell?

The point of the drill is not to catalogue every debt
item you know about. It is to force yourself to *stop
guessing* about the character of each item — to make
the distinction between "a loan we should keep" and "a
bad debt we need a plan for" concrete, per-item, before
you get to sizing (exercise 02) or budgeting (exercise
03) or deciding (exercise 04).

## Requirements

Author a Markdown table at `docs/tech-debt/quadrant-
drill.md` (or the equivalent in your working repo).

### The table

- Exactly **ten rows**. Fewer means you did not stretch;
  more means you did not filter (start with a longer
  list and cull to the ten most defensible for the
  drill).
- The rows must span **at least three of the four
  Fowler quadrants**. If every row lands in
  Deliberate-Reckless, you have a hiring or a
  shipping-culture problem the drill is exposing; keep
  going — the four-cell distribution is diagnostic on
  its own.
- The rows must include **at least two Quality-
  attribute** and **at least two Structural** items.
  This forces you to think in both families and to
  notice which one dominates your codebase.

### Columns per row

- `#` — row number.
- `Title` — a short descriptive noun (see chapter 06
  row-format guidance; do not write *"billing mess"*).
- `Fowler quadrant` — one of D-P, D-R, I-P, I-R.
- `Family` — Quality-attribute (name the ISO/IEC
  25010 characteristic — Reliability / Performance
  Efficiency / Security / Maintainability /
  Interaction Capability / Portability /
  Compatibility / Functional Suitability) or
  Structural (name the shape — wrong abstraction,
  wrong aggregate boundary, missing seam,
  architecture misfit, un-modelled invariant,
  ownership vacuum).
- `Evidence` — one line, factual. *"Post-mortem
  2026-04-11 traced 3 incidents in Q1 to this."*
  *"Onboarding for the last two hires took 4 extra
  days because of this."* *"The design partner
  contract mentions 500ms p95; current is 3.2s."*
- `Business-owner candidate` — one line: who on
  the business side is affected? Empty is a valid
  answer and *itself is data* — an item with no
  business-owner candidate is a deprecation
  candidate (chapter 05).

### The four short paragraphs after the table

Below the table, write four paragraphs (100-200 words
each):

- **Paragraph 1 — the quadrant distribution.** How
  many items landed in each of the four cells? What
  does the distribution suggest? *"Six of ten items
  are Deliberate-Reckless — we have been paying the
  loan-vs-lack-of-planning tax; this quarter's
  budget conversation needs to name the culture
  driver, not just the item list."*
- **Paragraph 2 — the family split.** How many
  Quality-attribute vs. Structural? Cross-tabulate
  against the quadrant if useful. If your portfolio
  is 80% structural and your team ranks
  Maintainability at #1 on the ISO/IEC 25010 ranking
  (mod-102 chapter 04), that is a coherent signal;
  if the ranking says Reliability at #1 and the
  portfolio is 80% Maintainability-related structural
  debt, the ranking and the portfolio are inconsistent
  and one of the two is wrong.
- **Paragraph 3 — the surprises.** Which categorisations
  did you originally get wrong? *"I categorised the
  billing rewrite as Inadvertent-Prudent because the
  original design 'couldn't have known', but the
  post-mortem shows the original team *did* know and
  shipped anyway to hit the demo — this is Deliberate-
  Reckless."* Naming this openly is the point of the
  drill.
- **Paragraph 4 — the diagnostic call-out.** Which
  cell is *filling up*? Chapter 01's guidance:
  Inadvertent-Reckless filling up is a hiring /
  training issue; Deliberate-Reckless filling up is a
  shipping-culture issue; Deliberate-Prudent items
  accumulating with no repayment is a refactor-
  budget issue (which exercise 03 handles); Inadvertent-
  Prudent items accumulating is a *good* signal —
  the team is learning the domain.

## Starter guidance

- **Start with a longer list, then cull to ten.**
  Brainstorm 20-30 items first; then filter for the
  ten with the most defensible categorisation. The
  cull itself teaches you which items you understand
  well and which you don't.
- **Sit next to two engineers who work in each
  affected subsystem before you finalise.** Solo
  categorisation by the CTO under-counts almost
  every category; the two engineers who actually
  touch the code have the evidence you need for the
  `Evidence` column.
- **The `Evidence` column has to be evidence, not
  intuition.** *"This feels wrong"* is not
  evidence. *"Two post-mortems in Q1"*, *"the
  design partner contract clause 4.2"*, *"three
  hires flagged this in their onboarding retros"*
  are.
- **Do not skip Deliberate-Prudent.** This is
  Cunningham's original loan (chapter 01). A
  portfolio with zero Deliberate-Prudent items is a
  portfolio in which the team is not shipping fast
  enough to be taking on any productive learning
  debt. Name at least one.
- **Do not conflate `Family` with `Fowler quadrant`.**
  A structural debt item can be Deliberate-Prudent
  (the team shipped a monolith with an intentionally
  loose aggregate boundary because the domain wasn't
  yet known — chapter 02 + chapter 01 = a totally
  coherent row). Do not force the two axes to
  correlate.
- **Cite the Fowler source.** The bliki entry is
  [`martinfowler.com/bliki/TechnicalDebtQuadrant.html`](https://martinfowler.com/bliki/TechnicalDebtQuadrant.html).
  If a reviewer or a future you disputes a
  categorisation, the reference decides.
- **Cite the ISO/IEC 25010 characteristic
  precisely.** *"Reliability"* is fine at this drill
  scale; the sub-characteristic (*"availability"*,
  *"fault tolerance"*, *"recoverability"*) is
  useful if you can identify it. See the taxonomy at
  [`iso25000.com/iso-25010`](https://iso25000.com/index.php/en/iso-25000-standards/iso-25010)
  when the top-level name is ambiguous.
- **The empty `Business-owner candidate` is
  diagnostic.** Items with no plausible business
  owner are deprecation candidates (chapter 05,
  question 1 of the decision tree). Do not force a
  business owner in where none exists — the empty
  cell is more useful than a false name.

## Acceptance criteria

Your drill output is complete when:

- The table has exactly ten rows spanning at least
  three quadrants and at least two of each family.
- Every row has a Title, quadrant, family (with the
  ISO/IEC 25010 characteristic or structural-shape
  named), a factual Evidence line, and a business-
  owner candidate (which may be blank).
- The four paragraphs each answer the corresponding
  question (distribution, family split, surprises,
  diagnostic).
- At least one row was originally categorised in one
  cell and moved after the two-engineer walkthrough —
  and the move is called out in Paragraph 3.
- The drill can be handed to a technical advisor or
  a co-founder who does not know your codebase,
  and they can read it and understand what kinds of
  debt you have without asking a follow-up.

## What this feeds into

- **Exercise 02** — the five items you take forward
  to cost-to-carry sizing should come from *this*
  ten-row list (typically the highest-Evidence rows,
  or the rows whose quadrant / family most demanded
  a plan).
- **Exercise 03** — the refactor budget is derived
  from the sized items' aggregate cost-to-carry.
- **Exercise 04** — the deprecate-vs-rewrite-vs-leave
  decision is per-item; the quadrant and the family
  from this drill are inputs.
- **Exercise 05** — the full inventory + decision log
  builds on the enriched rows.

The drill is intentionally light on prescriptive output
format; the discipline is the *categorisation itself*,
not the artifact polish. Exercise 05 is where the polish
happens.
