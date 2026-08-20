# The Debt Inventory and the Portfolio Decision Log

> "The good architect writes down the decisions that
> matter. The great architect writes them down in a
> format the next person can read." — a paraphrase of
> the working discipline in Nygard's original *Documenting
> Architecture Decisions* essay
> ([cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)),
> applied to the debt-portfolio artifact.

## Motivation

The four preceding chapters give the CTO the pieces:
Fowler quadrant + Cunningham metaphor (chapter 01), the
family (chapter 02), the cost-to-carry and depreciation
schedule (chapter 03), the refactor budget and business
owner (chapter 04), and the deprecate-vs-rewrite-vs-
leave decision (chapter 05). This chapter walks the
authoring of the *artifact* — the debt inventory and the
portfolio decision log — that assembles those pieces into
a single document a board member, an incoming VP
Engineering, a technical-due-diligence reviewer, or an
incoming senior architect can read.

The test the artifact has to pass: **a competent
technical reader who has not been in your building can
read the inventory in under thirty minutes and come out
knowing (a) what debt the company has, (b) what it
costs, (c) what the plan is for each item, and (d) which
items are engineering-owned versus which are
CEO / board / customer-facing decisions that require them
to weigh in.**

This is the artifact that turns *"the engineers keep
asking for a rewrite"* into *"here's the six-item
portfolio, here's the aggregate carry cost, here's the
plan for each item, here's the two items that need your
sign-off, here's the four we're just handling."*

## The two documents

The artifact is two files, not one:

- **The debt inventory** — `docs/tech-debt/inventory.md`
  or equivalent — a rolling table of every debt item
  currently on the portfolio. One row per item;
  columns are defined below. The inventory is
  *current-state*: the row goes away when the item is
  paid down, deprecated, or superseded.
- **The portfolio decision log** — `docs/tech-debt/decisions/`
  — a directory of numbered decision records, one per
  significant decision about the portfolio. This is
  the *history* of the portfolio, in the same shape
  as an ADR log (see
  [`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md)
  — Nygard's format, `adr-tools`
  ([github.com/npryce/adr-tools](https://github.com/npryce/adr-tools))
  works fine here too).

The split matters because the inventory answers "what
is the state today?" and the decision log answers "why
did we make the choices that got us here?". Combining
them into one document either buries the current state
under history or loses the history entirely.

## The inventory row format

One row per debt item. Columns:

- **`ID`** — a stable identifier (`DEBT-0001`,
  `DEBT-0002`, ...). Never renumber; retired items
  keep their ID in the decision log.
- **`Title`** — a short descriptive noun. *"Billing
  service — Order aggregate spans three services"*,
  not *"billing mess"*.
- **`Fowler quadrant`** (chapter 01) — Deliberate-
  Prudent / Deliberate-Reckless / Inadvertent-Prudent /
  Inadvertent-Reckless.
- **`Family`** (chapter 02) — Quality-attribute or
  Structural. If quality-attribute, name the ISO/IEC
  25010 characteristic (Reliability / Performance
  Efficiency / Security / Maintainability / ...).
- **`Cost-to-carry (now)`** (chapter 03) — engineering-
  hours per week. Cite the sources you added up
  (workaround / on-call / onboarding / lead-time /
  feature-slip / attrition).
- **`Depreciation`** (chapter 03) — the two-quarter
  projection, plus the dominant compounder (team-size /
  codebase-size / turnover / adjacent-decision).
- **`Business owner`** (chapter 04) — the non-
  engineering person whose commitment is unblocked
  when this debt is paid. Empty-cell = candidate for
  deprecation, not for repayment.
- **`Response`** (chapter 05) — Deprecate / Rewrite /
  Leave, with a one-line justification anchored to the
  decision tree.
- **`Plan`** — the concrete near-term work, if any.
  For *Rewrite*: the StranglerFig migration plan or a
  pointer to a decision-log entry that holds it. For
  *Deprecate*: the sunset schedule. For *Leave*: the
  revisit date.
- **`Driver`** — the business fact that this debt is
  a downstream consequence of (per chapter 02's
  "structural debt that is actually a pivot" edge
  case).
- **`Boundary`** — one of `founder-scope`, `defer to
  ai-infra-senior-architect (level 45)`, `defer to
  ai-infra-principal-architect (level 55)` (per
  chapter 05's boundary section). Every row is
  labelled.
- **`Last reviewed`** and **`Next review`** — dates.
  Every row is reviewed at least quarterly; some
  rows more often.

A single row in practice:

```
ID           DEBT-0007
Title        Billing — Order aggregate spans three services (billing, notifications, invoicing)
Fowler       Inadvertent-Prudent (we didn't know how the domain would evolve)
Family       Structural (aggregate boundary is wrong; domain has three coupled write paths)
Cost-to-carry ~12 h/wk (workaround: 6 / on-call: 3 / onboarding: 2 / lead-time: 1)
Depreciation ~18 h/wk by end Q3 (dominant compounder: team-size — two hires onto billing in Q2)
Business owner Head of Sales (blocks usage-based-pricing commitment to design partner ACME Corp; contract signed 2026-06-10)
Response     Rewrite via StranglerFig (see DECISION-0004)
Plan         Q2 wk 1-3: dual-write to new aggregate; Q2 wk 4-8: shift reads; Q3 wk 1-2: cutover writes; Q3 wk 3: delete old
Driver       Usage-based-pricing commitment (ACME contract, 2026-06-10)
Boundary     founder-scope
Last reviewed 2026-08-01
Next review  2026-11-01
```

The row is longer than a typical spreadsheet row and
that is deliberate. A row that reads like a spreadsheet
row hides the reasoning that makes the row defensible; a
row that reads like an executive one-pager makes it
possible for the CEO to challenge the response without a
follow-up meeting.

## The decision-log record format

The portfolio decision log follows the Nygard ADR shape
([cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)),
with debt-portfolio-specific sections. One file per
decision:

```
# DECISION-0004 — Rewrite Billing Order Aggregate via StranglerFig

## Status
Accepted, 2026-08-15. Superseded by DECISION-0011 (2026-11-20) — no. Live.

## Context
- Inventory items affected: DEBT-0007, DEBT-0009.
- Aggregate cost-to-carry: ~15 h/wk today, projected ~22 h/wk by end Q3.
- Business trigger: ACME Corp usage-based-pricing commitment (2026-06-10 contract).
- Team-size trigger: two hires slated onto billing in Q2 (see mod-104 hiring plan HP-2026-Q2).

## Decision
Rewrite via StranglerFig over Q2-Q3. Old aggregate is retained
until final cutover in Q3 week 3. Dual-write pattern for weeks
1-3; parity checker for weeks 4-8; cutover of writes in Q3 week
1-2; deletion of old path in Q3 week 3.

## Chesterton's Fence check
- The three-service split originally existed because of a 2024
  compliance requirement (SOC 2 controls CC6.1 / CC7.2) that
  billing not co-locate with notifications. Requirement is now
  satisfied by the ISMS scoping change of DECISION-0002 (2026-
  05-10) — the aggregate boundary is no longer load-bearing on
  compliance.
- Retroactive ADR filed: `ADR-0037 — Billing / Notifications /
  Invoicing Split Rationale` documents the original
  constraint and its supersession.

## Consequences
- Positive: cost-to-carry drops to ~4 h/wk post-migration;
  usage-based-pricing feature becomes a two-week ship instead
  of a six-week coordination.
- Negative: refactor budget for Q2 rises from 20% to 26% (see
  BUDGET-2026-Q2). Two feature commitments move: X from Q2 to
  Q3; Y from Q3 to Q4.
- Deferred: multi-tenant isolation depth defers to ai-infra-
  senior-architect (level 45) — see the pool/silo/bridge
  vocabulary in the AWS SaaS Lens (docs.aws.amazon.com/
  wellarchitected/latest/saas-lens/saas-lens.html); we do not
  need it in this rewrite but we should not introduce a shape
  that forecloses it.

## Business owner sign-off
- CEO (as compliance lead per mod-107 chapter 01) — 2026-08-14
- Head of Sales (for ACME commitment) — 2026-08-14

## Review cadence
- Weekly stand-up during Q2; monthly during Q3 wrap.
- Next portfolio-level review: 2026-11-01.
```

Two properties of the record shape:

- **The Chesterton's Fence check is called out
  explicitly.** Chapter 05's discipline lives here in
  writing, and can be audited later. If the check
  turns out to have missed something, the decision
  log makes the miss explicit; that is how the org
  learns.
- **Business-owner sign-off is on the record.** The
  business owner (chapter 04) is not just named — they
  co-signed the decision. This is what makes the
  decision defensible in a subsequent quarter when
  someone asks "why did we spend a quarter on this?".

## The one-page portfolio summary (the board version)

The inventory and the decision log are the full-fidelity
artifact. The **board version** is a single page that
lives at the top of the inventory file (or in the board
pre-read, per [`mod-108` chapter 04](../mod-108-cto-ceo-and-board-communication/README.md)).

The summary contains:

- **Portfolio size.** Number of items on the current
  inventory (typically 5-15 at pre-Series-A; more
  than 20 is a warning sign that the CTO is either
  cataloguing at too fine a grain or has genuinely
  lost portfolio discipline).
- **Aggregate cost-to-carry.** Sum of the item-level
  numbers, expressed as engineering-hours per week
  AND as a percentage of team capacity. *"Currently
  ~55 h/wk (~14% of engineering capacity), projected
  ~74 h/wk (~19%) by end of next quarter."*
- **Response mix.** How many items are Deprecate, how
  many Rewrite, how many Leave. The board notices if
  the ratio is unusual — all-Rewrite is a warning
  sign, all-Leave is a warning sign, all-Deprecate is
  suspicious.
- **This quarter's principal repayment.** Which
  specific items are being paid down this quarter,
  and against which business commitments.
- **The two or three items that need CEO / board
  attention.** The items whose deprecation would
  require a customer-facing communication, whose
  rewrite requires a business trade-off the CEO
  should sign off on, or whose "leave" carry cost is
  material enough to name in the board pack.
- **The boundary items.** The two or three items
  where the founder-scope CTO is choosing to defer
  up to `ai-infra-senior-architect` or `ai-infra-
  principal-architect` rather than attempt in-house.
  Naming them at the board explicitly is the honest
  version of the boundary — the alternative is
  attempting them, failing, and having to explain
  the fail retroactively.

The one-page summary is what the CEO cites in the
Series-B fundraising deck as *"engineering health —
technical debt is a portfolio the CTO manages
explicitly."* It is what the Series-B lead investor's
technical-due-diligence reviewer reads first when they
ask for the debt inventory (they will ask; every
technical-DD checklist asks — see the a16z tech-DD
checklist at [a16z.com/tech-diligence-checklist](https://a16z.com/tech-diligence-checklist/)).
And it is what the incoming VP Engineering reads on
day one to understand what they have inherited.

## The boundary to `ai-infra-senior-architect`

Chapter 05 named the two responses that defer up
(multi-quarter, multi-team system extractions;
multi-region / multi-tenant re-architectures). The
inventory row's `Boundary` column labels this per row,
which is where the deferral lives operationally.

The rule for populating the column:

- **`founder-scope`** — everything a pre-Series-A CTO
  can legitimately StranglerFig themselves on a team of
  5-25 engineers running a single-region production
  system. This is most of the inventory at seed / early
  Series-A.
- **`defer to ai-infra-senior-architect (level 45)`** —
  the extraction / re-architecture jobs that are
  genuinely multi-quarter, multi-team, or cross a
  scale threshold the founder-CTO has not personally
  worked at. The role at level 45 owns *"the
  technical mechanics of large refactors and system
  extractions at post-Series-B scale"* per the
  ownership map in
  [`CURRICULUM.md`](../../CURRICULUM.md).
- **`defer to ai-infra-principal-architect (level 55)`** —
  the highest-altitude re-architecture work
  (distributed-consensus rewrites, multi-region /
  multi-cloud posture changes, multi-tenancy model
  changes at scale). Rare at pre-Series-A; label the
  row explicitly rather than pretending you would
  attempt it.

The peer-track owners for the technical craft — not the
business framing — are
[`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning),
[`ai-infra-principal-engineer`](../../../ai-infra-principal-engineer-learning),
and
[`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning);
they own the deep how, this module owns the debt-as-
business-portfolio framing at pre-Series-A scale.

## Cadence

The inventory and the decision log are *living* artifacts:

- **Weekly** — engineering leadership reviews the
  inventory in the weekly leadership sync. New items
  get added; items whose cost-to-carry has crossed a
  threshold get flagged; items being actively paid
  down get status updates.
- **Monthly** — the CTO reviews the inventory with the
  CEO. The one-page summary is the discussion
  document. Business-owner sign-offs happen here.
- **Quarterly** — the inventory is re-baselined
  against the roadmap and the hiring plan; the
  refactor budget for the next quarter is set (chapter
  04); the "leave" items whose revisit-date lands in
  this quarter get re-decided. A quarterly summary
  paragraph goes into the board pre-read.
- **Annually** — the whole portfolio is reviewed for
  patterns. Are all the recent additions in the same
  subsystem (suggesting a topology change per
  [`mod-104` chapter 04](../mod-104-first-engineering-hires-and-team-topology/04-team-topologies-at-startup-scale.md))?
  Is the Inadvertent-Reckless quadrant filling up
  (suggesting a hiring / training issue per
  [`mod-104` chapter 03](../mod-104-first-engineering-hires-and-team-topology/03-founding-engineer-profile-and-first-project.md))?
  Is the Deliberate-Reckless quadrant filling up
  (suggesting the shipping-pressure culture is
  compounding faster than the org can service)? The
  annual review is where these meta-patterns get
  surfaced.

## Failure modes

- **The write-once inventory.** A debt inventory that
  was authored in Q1 and never updated. New items
  don't appear; paid-down items are still on the
  list; the aggregate cost-to-carry is wildly wrong.
  Fix: the review cadence above; the inventory is a
  living artifact.
- **The prose-not-tabular inventory.** The inventory
  is a wall of paragraphs instead of a table. A
  reader cannot compare rows; the CTO cannot sort by
  cost-to-carry or by response; the summary numbers
  cannot be derived. Fix: use the columnar format.
- **The no-business-owner inventory.** Every row's
  business-owner column is either empty or *"CTO"*.
  The portfolio has no external advocacy; it loses
  every prioritisation vote. Fix: for each row,
  either name a real business owner or accept that
  the item is engineering-aesthetic and treat it as a
  deprecate candidate (chapter 05).
- **The no-decision-log portfolio.** The inventory
  exists but there is no history of why the current
  responses were chosen. A new VP Eng inherits the
  inventory and has to re-derive every choice. Fix:
  every material response change (Rewrite → Leave,
  Leave → Deprecate) files a decision-log entry.
- **The boundary-column-empty inventory.** No item is
  labelled with the boundary to `ai-infra-senior-
  architect` / `ai-infra-principal-architect`,
  because the CTO is uncomfortable admitting some
  items are out of their scope. The two rewrites
  outside founder scope get attempted anyway; they
  fail slowly. Fix: label every row; be honest
  about the two or three items that defer up.
- **The board summary that is only technical.** The
  one-page summary reads like an engineering
  document. The CEO / board can't parse it. Fix:
  lead with response mix, aggregate cost, and the
  two items that need CEO attention; put the ISO/IEC
  25010 taxonomy detail in the inventory file, not
  in the summary.

## Summary

- The artifact is **two documents**: the **debt
  inventory** (current state, tabular, one row per
  item) and the **portfolio decision log** (history,
  Nygard ADR shape, one file per material decision).
- The inventory **row schema** carries eleven columns:
  ID, Title, Fowler quadrant, Family, Cost-to-carry
  (now), Depreciation, Business owner, Response, Plan,
  Driver, Boundary, Last reviewed / Next review. The
  row is longer than a spreadsheet row on purpose —
  it holds the reasoning that makes the response
  defensible.
- The decision-log record uses the **Nygard ADR
  format**
  ([cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions))
  with debt-specific sections: **Chesterton's Fence
  check**, **business-owner sign-off**, **review
  cadence**.
- The **one-page portfolio summary** (portfolio size,
  aggregate cost-to-carry, response mix, this-quarter
  repayment, items needing CEO / board attention,
  boundary items) is what the CEO cites in the board
  pack and what the Series-B technical-DD reviewer
  reads first.
- The **boundary column** labels each item
  `founder-scope` / `defer to ai-infra-senior-
  architect (level 45)` / `defer to ai-infra-
  principal-architect (level 55)` so the two rewrites
  outside pre-Series-A scope are honest about
  deferring up.
- The **cadence** is weekly (engineering leadership),
  monthly (with CEO), quarterly (with the roadmap
  and hiring plan), annually (for meta-patterns —
  Inadvertent-Reckless filling up = hiring issue;
  Deliberate-Reckless filling up = shipping-culture
  issue).

The chapter's paired exercise —
[`exercise-05-technical-debt-inventory-authoring.md`](exercises/exercise-05-technical-debt-inventory-authoring.md)
— walks the authoring of the full inventory + one
sample decision-log entry + the one-page board summary
for your (or a real reference) startup. This is the
capstone-quality artifact of the whole module; it
becomes an input to the lab in this module
(`lab-01-publish-a-technical-debt-portfolio-decision-log`)
and to the capstone
[`project-102`](../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package/)
(the SOC 2 readiness + compliance-debt package) and
[`project-103`](../../projects/project-103-scaling-plan-from-five-to-fifty-engineers/)
(the 5 → 40 engineer scaling plan's debt-portfolio
section).
