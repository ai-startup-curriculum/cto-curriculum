# Exercise 05 — Technical Debt Inventory Authoring

**Module:** `mod-105-technical-debt-as-business-decision`
**Planned time:** ~3 hours
**Chapter this builds on:** [`06-debt-inventory-and-portfolio-decision-log.md`](../06-debt-inventory-and-portfolio-decision-log.md),
consolidating the outputs of
[`exercise-01`](exercise-01-fowler-quadrant-categorisation-drill.md)
(categorisation),
[`exercise-02`](exercise-02-cost-to-carry-sizing-for-five-debt-items.md)
(sizing),
[`exercise-03`](exercise-03-refactor-budget-tied-to-roadmap-drill.md)
(budget), and
[`exercise-04`](exercise-04-deprecate-vs-rewrite-vs-leave-decision-drill.md)
(decisions).

## Problem statement

Author the **complete debt inventory** and **one sample
portfolio-decision-log entry** for your (or a real
reference) startup, using the eleven-column row format
from chapter 06. Then compose the **one-page portfolio
summary** the CEO can drop into a board pre-read.

This is the capstone-quality artifact of the whole
module. It is the document that turns *"the engineers
keep asking for a rewrite"* into *"here's the six-item
portfolio, here's the aggregate carry cost, here's the
plan for each item, here's the two items that need
your sign-off, here's the four we're just handling."*
It is the artifact that a Series-B lead investor's
technical-due-diligence reviewer will ask for by name
(see the a16z tech-DD checklist at
[`a16z.com/tech-diligence-checklist`](https://a16z.com/tech-diligence-checklist/)),
that an incoming VP Engineering will read on day one,
and that the CEO will cite in the Series-B fundraising
narrative as *"engineering health — technical debt is
a portfolio the CTO manages explicitly."*

## Requirements

Author **three files** in a `docs/tech-debt/` directory
(or the equivalent in your working repo):

- `docs/tech-debt/inventory.md` — the complete
  inventory (typically 6-12 rows).
- `docs/tech-debt/decisions/DECISION-0001-<slug>.md`
  — one sample decision-log entry, using the Nygard
  ADR shape (chapter 06 walks the format; see
  [`cognitect.com/blog/2011/11/15/documenting-architecture-decisions`](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)).
- `docs/tech-debt/README.md` — a short index /
  overview file that links to the inventory and the
  decision log and states the review cadence.

### `inventory.md` — the debt inventory

At the top of the file: the **one-page portfolio
summary** (see below).

Below it: the **row-per-item table** in the eleven-
column format from chapter 06.

The inventory contains **6-12 rows**:

- Fewer than 6 → you are under-cataloguing (or your
  codebase is genuinely brand-new; if so, say so at
  the top).
- More than 12 → you are cataloguing at too fine a
  grain; consolidate items that share a subsystem
  and a business owner into portfolio-level rows.
  Chapter 06's guidance: >20 rows is a warning sign
  of lost portfolio discipline.

**Columns per row** (from chapter 06 — verbatim):

- `ID` — `DEBT-0001`, `DEBT-0002`, ... — stable,
  never renumber.
- `Title` — a descriptive noun.
- `Fowler quadrant` — Deliberate-Prudent /
  Deliberate-Reckless / Inadvertent-Prudent /
  Inadvertent-Reckless. Cite
  [`martinfowler.com/bliki/TechnicalDebtQuadrant.html`](https://martinfowler.com/bliki/TechnicalDebtQuadrant.html)
  in the file preamble.
- `Family` — Quality-attribute (with ISO/IEC 25010
  characteristic named) or Structural (with shape
  named). Cite
  [`iso.org/standard/78176.html`](https://www.iso.org/standard/78176.html).
- `Cost-to-carry (now)` — engineering-hours per
  week; cite the sources you added up per
  chapter 03.
- `Depreciation` — 2-quarter projection; name the
  dominant compounder.
- `Business owner` — the non-engineering person
  whose commitment is unblocked when this debt is
  paid. Empty = deprecation candidate.
- `Response` — Deprecate / Rewrite / Leave, with a
  one-line justification.
- `Plan` — the concrete near-term work. For
  Rewrite, the StranglerFig migration steps or a
  pointer to a decision-log entry that holds it.
  For Deprecate, the sunset schedule. For Leave,
  the revisit date.
- `Driver` — the business fact this debt is a
  downstream consequence of. Especially important
  for the *"structural debt that is actually a
  pivot"* edge case from chapter 02.
- `Boundary` — one of `founder-scope`, `defer to
  ai-infra-senior-architect (level 45)`, `defer to
  ai-infra-principal-architect (level 55)`.
- `Last reviewed` / `Next review` — dates.

At least **three rows** should be populated from the
categorisation, sizing, and decisions of exercises
01-04 (i.e. this file is not from scratch — it
consolidates prior work).

### The one-page portfolio summary (top of `inventory.md`)

A section at the top of the inventory file titled
`## Portfolio summary — <date>` that contains:

- **Portfolio size** — number of items on the
  current inventory.
- **Aggregate cost-to-carry** — sum of all rows'
  cost-to-carry (now), expressed as engineering-
  hours per week AND as percentage of team capacity.
  Compare against projected end-of-quarter-+2 (the
  compounding line).
- **Response mix** — count of Deprecate / Rewrite /
  Leave items. Chapter 06's sanity check: if the
  mix is all-Rewrite, all-Leave, or all-Deprecate,
  call it out.
- **This quarter's principal repayment** — the
  specific items being paid down (typically 2-4
  items) and the business commitments each
  unblocks.
- **Items needing CEO / board attention** — the
  two or three items whose response requires the
  CEO to weigh in (customer-visible deprecation,
  material feature-work trade-off for a rewrite,
  Leave-decision whose carry cost is material).
- **Boundary items** — the items labelled `defer
  to ai-infra-senior-architect` or `defer to
  ai-infra-principal-architect`, named at the
  board so the deferral is explicit rather than
  implicit.

The summary should be readable in **under three
minutes** — this is the paragraph the CEO reads
before the board meeting. Detail lives in the
inventory rows below.

### `decisions/DECISION-0001-<slug>.md` — the sample decision-log entry

**One** decision-log entry, for the most defensible
Rewrite decision from exercise 04 (or, if you have no
Rewrite decision, the most defensible Deprecate). Use
the chapter 06 shape:

- `## Status` — Accepted / Superseded, with date.
- `## Context` — inventory items affected, aggregate
  cost-to-carry, business trigger, team-size trigger
  (with cross-references to the hiring plan from
  mod-104 exercise 01 where relevant).
- `## Decision` — the response chosen, with the
  StranglerFig / sunset / revisit specifics.
- `## Chesterton's Fence check` — retroactive ADR
  citations for the load-bearing pieces of the
  current code. Cite the archival sources (ADR
  numbers, post-mortem dates, customer requirement
  IDs).
- `## Consequences` — Positive / Negative / Deferred,
  with the roadmap and hiring-plan interactions
  called out explicitly. This is the Nygard shape;
  see [`mod-102` chapter 02](../../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md)
  and Nygard's original essay
  ([`cognitect.com/blog/2011/11/15/documenting-architecture-decisions`](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)).
- `## Business owner sign-off` — the named person
  and the date they signed.
- `## Review cadence` — the weekly / monthly /
  quarterly cadence during and after execution.

### `docs/tech-debt/README.md` — the index

A short (100-200 word) file that:

- Explains what lives in the directory (inventory,
  decisions).
- States the review cadence — weekly (engineering
  leadership sync), monthly (with CEO), quarterly
  (with roadmap and hiring plan), annually (for
  meta-patterns per chapter 06).
- Points to the module chapters as reference.
- Names the boundary owner peers for out-of-scope
  items:
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45),
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55).

## Starter guidance

- **Consolidate rather than re-invent.** This
  exercise assembles the outputs of exercises 01-04.
  If a row's Fowler quadrant / family / cost-to-
  carry / response was determined in a prior
  exercise, use *that*. Do not re-decide.
- **The one-page summary is the highest-leverage
  artifact.** A board member will read it and
  nothing else. Write it *last* (once the inventory
  is populated) and rewrite it three times.
- **Prose in the row is a feature, not a bug.**
  Chapter 06's row format is longer than a
  spreadsheet row on purpose. A row that reads like
  a spreadsheet row hides the reasoning; a row
  that reads like an executive one-pager makes it
  possible for the CEO to challenge the response
  without a follow-up meeting.
- **Fill the `Driver` column for every row.**
  Chapter 02's *"structural debt that is actually a
  pivot"* and chapter 06's row schema both make this
  non-optional. A row without a driver is a row
  whose business rationale you have not identified;
  that is either a deprecation candidate or an
  engineering-aesthetic item, per chapter 04.
- **Fill the `Boundary` column for every row.**
  Chapter 05 and chapter 06 both emphasise this.
  Do not leave rows with implicit boundary — the
  deferrals must be visible to the board and to an
  incoming VP Eng.
- **Do not include items with no evidence.** Every
  row's cost-to-carry needs the six-source sum
  (chapter 03; from exercise 02). If you have not
  sized the item, it does not belong in the
  inventory yet — take it back to exercise 02
  first.
- **Cross-link generously.** The inventory row
  should link to the decision-log entry that
  captured its response; the decision-log entry
  should link back to the inventory row(s) it
  affects. This is the same discipline as Nygard
  ADRs (mod-102 chapter 02) — the artifacts are
  a graph, not a flat list.
- **Cite the sources.** Cunningham 1992
  ([`c2.com/doc/oopsla92.html`](http://c2.com/doc/oopsla92.html))
  in the preamble; Fowler's *TechnicalDebtQuadrant*
  ([`martinfowler.com/bliki/TechnicalDebtQuadrant.html`](https://martinfowler.com/bliki/TechnicalDebtQuadrant.html))
  in the Fowler-quadrant column header; ISO/IEC
  25010:2023
  ([`iso.org/standard/78176.html`](https://www.iso.org/standard/78176.html))
  in the Family column header; Fowler's
  *StranglerFigApplication*
  ([`martinfowler.com/bliki/StranglerFigApplication.html`](https://martinfowler.com/bliki/StranglerFigApplication.html))
  in any Rewrite response block.
- **Boundary honesty is not weakness.** Rows
  labelled `defer to ai-infra-senior-architect
  (level 45)` are chapter 06's chosen shape for
  admitting scope limits. Attempting the out-of-
  scope rewrite in-house is a worse outcome than
  naming the deferral in the inventory.
- **The document is a living artifact.** Add a
  `Version:` and today's date at the top; add a
  `Next portfolio-level review:` date one quarter
  out.

## Acceptance criteria

The inventory is complete when:

- `inventory.md` opens with a one-page portfolio
  summary containing portfolio size, aggregate
  cost-to-carry (now + projected), response mix,
  this-quarter's principal repayment, items
  needing CEO attention, and boundary items.
- The inventory table has 6-12 rows, each with all
  eleven columns populated (rows with empty
  business-owner columns are flagged as
  deprecation candidates in the Response column).
- At least three rows are consolidated from the
  exercises 01-04 outputs (so the exercise is a
  synthesis, not a from-scratch restart).
- Response-mix contains at least one Deprecate,
  at least one Rewrite, and at least one Leave —
  if your portfolio does not naturally produce
  this mix, add a paragraph in the README
  explaining why.
- Every row has `Driver` and `Boundary` populated.
- `decisions/DECISION-0001-<slug>.md` uses the
  Nygard ADR shape with the debt-specific
  sections (Chesterton's Fence check, business-
  owner sign-off, review cadence).
- The Chesterton's Fence check cites at least one
  archival source (ADR, post-mortem, customer
  requirement, or named conversation).
- `docs/tech-debt/README.md` states the review
  cadence and names the boundary peer tracks.
- A test reader — a co-founder, a technical
  advisor, an incoming VP Eng, or a Series-B
  technical-DD reviewer — can read the three files
  in **under 30 minutes** and come out knowing what
  debt the company has, what it costs, what the
  plan is per item, and which items require CEO
  input.

## What this feeds into

- **Lab 01** —
  `lab-01-publish-a-technical-debt-portfolio-decision-log`
  publishes this artifact as a durable, versioned,
  quarterly-reviewed document.
- **Capstone [`project-102`](../../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package/)** —
  the SOC 2 Type I readiness package's compliance-
  debt inventory reuses this format for the
  compliance / security debt slice.
- **Capstone [`project-103`](../../../projects/project-103-scaling-plan-from-five-to-fifty-engineers/)** —
  the 5-to-40-engineer scaling plan's debt
  portfolio uses this format as its debt-portfolio
  section across the four planned stages.
- **Board pre-reads** — the one-page portfolio
  summary is a monthly board pre-read section
  (see [`mod-108` chapter 04](../../mod-108-cto-ceo-and-board-communication/README.md)).
- **Technical-due-diligence** — the full inventory
  + decision log is the artifact a Series-B lead
  investor's DD reviewer reads first when asking
  about engineering health (see the a16z tech-DD
  checklist at
  [`a16z.com/tech-diligence-checklist`](https://a16z.com/tech-diligence-checklist/)).

The exercise is *one* round of authoring; the
artifact is a **living document reviewed on the
cadence stated in the README**. Every quarter's
review moves items along, adds new items, and
generates new decision-log entries. Over 18-24
months the decision log becomes the *history* of
your engineering-strategy portfolio — the artifact
an incoming VP Eng reads before their first debt-
review meeting so they arrive with context, not with
questions.
