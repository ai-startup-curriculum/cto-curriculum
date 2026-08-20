# Exercise 04 — Deprecate vs. Rewrite vs. Leave Decision Drill

**Module:** `mod-105-technical-debt-as-business-decision`
**Planned time:** ~3 hours
**Chapter this builds on:** [`05-deprecate-rewrite-or-leave.md`](../05-deprecate-rewrite-or-leave.md),
building on the sized items from
[`exercise-02`](exercise-02-cost-to-carry-sizing-for-five-debt-items.md)
and the allocated budget from
[`exercise-03`](exercise-03-refactor-budget-tied-to-roadmap-drill.md).

## Problem statement

For **five debt items** (typically the same five you
sized in exercise 02), walk the chapter-05 **decision
tree** end-to-end. For each item, produce a **per-item
memo** that:

- runs the five decision-tree questions in order,
- arrives at one of the three responses (Deprecate /
  Rewrite / Leave),
- and defends the choice on the four columns you now
  have from the previous exercises (Fowler quadrant,
  family, cost-to-carry, business owner).

For any item where the response is **Rewrite**, the
memo must include a **Chesterton's Fence check** (why
does the current code exist in its current form? —
with source citations) and a **StranglerFig migration
sketch** (the incremental, reversible steps).

For any item where the response is **Leave**, the memo
must include the **explicit carry cost** the org is
accepting and a **revisit date**.

For any item where the response is **Deprecate**, the
memo must include the **sunset schedule** and the
**customer / product interactions** the deprecation
requires.

The point of the drill is to make the responses
defensible — chapter 05's failure modes (skipped
Chesterton's Fence, big-bang rewrite, rewrite that
should have been a deprecate, engineering-aesthetic
rewrite, unrevisited "leave") are exactly the failures
this drill guards against.

## Requirements

Author a Markdown document at `docs/tech-debt/response-
decisions.md` (or the equivalent in your working repo).

### For each of the five items

#### The item header

- ID, Title, Fowler quadrant, Family (carry forward
  from exercise 01 / 02).
- Cost-to-carry (now) + projected end-of-quarter-+2
  (carry forward from exercise 02).
- Business owner (carry forward from exercise 03).

#### The decision-tree walk

Walk **all five** questions from chapter 05 in order.
Do not skip any; the discipline is the walk itself.

- **Q1: Does the underlying feature still have a
  business owner?** If no → Deprecate. Justify with
  the business-owner-search evidence.
- **Q2: Is the debt quality-attribute or
  structural?** Quality-attribute → leave-and-fix-
  in-place via the refactor budget; the deprecate-
  vs-rewrite question does not apply. Structural →
  continue.
- **Q3: Does the depreciation curve project to
  exceed the fix cost within 4-6 quarters?** No →
  Leave. Yes → continue.
- **Q4: Does the Chesterton's Fence check pass?**
  No → Pause and do archaeology first. Yes →
  continue.
- **Q5: Do you have the team, runway, and political
  room for a StranglerFig-shape migration?** No →
  Leave. Yes → Rewrite.

For each question, write one to two sentences: the
answer and the evidence. *"Q1: Yes. Head of Sales owns
the ACME contract that this subsystem's slowness is
blocking; the business-owner column is filled."*

#### The response block

Depending on where the item lands:

- **If DEPRECATE:**
  - Sunset schedule: two-week feature-flag off in
    staging → one-month feature-flag off in
    production (behind a quiet-hours window) → code
    removal in next release → documentation-only
    presence for one more quarter → deletion.
  - Customer / product interactions required:
    Product / Marketing communication window,
    Customer Success outreach to affected
    accounts, docs update. Name the counterpart
    role (per Marty Cagan's product-decision
    framing in *Inspired* / *Empowered* —
    [svpg.com/books](https://www.svpg.com/books/)).
  - Business-owner sign-off required from
    (person / role).
- **If REWRITE:**
  - **Chesterton's Fence check.** For each non-
    obvious piece of the current code, note **why
    it exists**, citing archival source: an ADR
    (see [`mod-102` chapter 02](../../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md)),
    an incident post-mortem, a customer
    requirement, or a named conversation with a
    still-employed original author. If any piece
    fails the check, note the *archaeology* work
    (typically retroactive ADRs) that must
    complete before the rewrite begins.
  - **StranglerFig migration sketch.** A 5-9 step
    plan following Martin Fowler's pattern
    ([martinfowler.com/bliki/StranglerFigApplication.html](https://martinfowler.com/bliki/StranglerFigApplication.html)):
    put the new system alongside; route a subset
    of traffic; verify parity; migrate more;
    repeat; delete the old only when the last
    traffic is off. Each step is named,
    reversible, and estimatable.
  - **Feature-work compatibility.** Which feature
    work can proceed *during* the migration
    (against the old system) and which must wait?
    Chapter 05's discipline: the strangler
    pattern lets most feature work continue; a
    big-bang cutover forbids feature work. Name
    what your plan actually allows.
  - **Business-owner sign-off** required from
    (person / role).
- **If LEAVE:**
  - **Explicit carry cost** — restate the current
    cost-to-carry AND the projected cost-to-carry
    at revisit date. This is what the org is
    accepting.
  - **Revisit date** — a specific date one to two
    quarters out. Chapter 05's *"leave"* is
    time-boxed.
  - **The trigger that would flip this to
    Rewrite** — the observable condition (cost-
    to-carry exceeds X hours/week, an incident
    class recurs, a specific customer signs a
    specific contract, a specific hire lands)
    that would re-open the decision earlier than
    the revisit date.

#### The boundary label

For each item, label the boundary per chapter 05 /
chapter 06:

- `founder-scope` — you can StranglerFig it
  in-house.
- `defer to ai-infra-senior-architect (level 45)` —
  multi-quarter / multi-team / multi-region.
- `defer to ai-infra-principal-architect (level
  55)` — distributed-consensus / multi-region /
  multi-tenancy-model scope.

An item labelled `defer to ai-infra-senior-architect`
should still get a response memo — the response is
usually **Leave with named advisor / hire trigger** —
but the memo makes the deferral honest rather than
implicit.

### The five-item roll-up

After the five per-item memos, write a **short roll-up
paragraph (150-300 words)** that answers:

- **Response mix.** Of the five items: how many
  Deprecate, how many Rewrite, how many Leave?
  Chapter 05's warning-sign check: all-Rewrite,
  all-Leave, or all-Deprecate is unusual and merits
  a sanity check.
- **The single item you are least sure about**, and
  the specific piece of evidence that would flip your
  decision. This is the item you would take to a
  technical advisor for a second opinion.
- **The one item that requires CEO sign-off** —
  typically a deprecation with customer impact, or a
  rewrite with a material feature-work trade-off, or
  a leave whose carry cost is material enough to
  name in the board pack.

## Starter guidance

- **Do not skip Q1.** Deprecation is chapter 05's
  cheapest-and-most-underused response. Every drill
  where zero items go to Deprecate should trigger a
  sanity check — is there really no feature in the
  five items whose usage is <1% and whose owner
  cannot be identified?
- **Chesterton's Fence is not optional.** For any
  Rewrite item, if you cannot find an archival
  source for at least the load-bearing pieces of
  the current code, the response is *not* Rewrite —
  it is *Pause and do archaeology*, followed by
  Rewrite once the archaeology completes. Chapter
  05's failure-mode list is explicit on this.
- **StranglerFig, not big-bang.** Any Rewrite plan
  that describes a single quarter-long branch with
  a "flip over at the end" is chapter 05's *big-
  bang rewrite* failure mode. Redraft into named,
  reversible, incremental steps. The Fowler bliki
  ([martinfowler.com/bliki/StranglerFigApplication.html](https://martinfowler.com/bliki/StranglerFigApplication.html))
  and Newman's *Monolith to Microservices*
  ([samnewman.io/books/monolith-to-microservices](https://samnewman.io/books/monolith-to-microservices/))
  are the primary references.
- **Read Joel Spolsky's *"Things You Should Never
  Do, Part I"*** before finalising any Rewrite
  memo:
  [`joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/`](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/).
  It is 20 years old, three pages long, and every
  paragraph still applies.
- **"Leave" is a legitimate response.** Do not treat
  a Leave decision as failure. Chapter 05's
  emphasis: it is a *deliberate* choice to pay
  cost-to-carry in exchange for freed budget for
  higher-priority work. The discipline is that it
  is *explicit* (with carry cost stated) and *time-
  boxed* (with a revisit date), not that it is
  avoided.
- **Boundary honesty.** If an item is genuinely
  outside your scope — a multi-region cutover, a
  multi-tenant model change, a multi-quarter cross-
  team extraction — label it and choose *Leave with
  named advisor / hire trigger*. Chapter 05's
  boundary-honesty framing: attempting the
  out-of-scope rewrite in-house is worse than
  admitting the boundary.
- **The business-owner sign-off is a real
  signature, not a name in a column.** Before the
  memo lands in the inventory (exercise 05), the
  business owner has read the response block and
  agreed. If they haven't, the memo is a draft;
  chase the sign-off before finalising.

## Acceptance criteria

The drill output is complete when:

- Each of the five items has a memo that walks all
  five decision-tree questions in order.
- Each memo lands on Deprecate, Rewrite, or Leave
  with a response block that has the required
  fields (sunset schedule / Chesterton + StranglerFig
  / carry cost + revisit date).
- Each Rewrite memo has a Chesterton's Fence check
  with at least one archival citation per non-
  obvious piece; if any piece fails, the memo notes
  the archaeology work required before the
  StranglerFig begins.
- Each Rewrite memo has a StranglerFig plan with
  5-9 named, reversible, incremental steps — no
  big-bang cutovers.
- Each Leave memo has an explicit carry cost, a
  revisit date, and the trigger that would flip it
  to Rewrite.
- Each Deprecate memo has a sunset schedule and
  names the Product / Marketing / Customer Success
  counterparts.
- Every item has a boundary label; items outside
  founder scope are named as such rather than
  attempted.
- The roll-up paragraph answers response-mix,
  least-sure-item, and CEO-sign-off-item.
- A technical advisor who reads the document can
  challenge any single decision on evidence; that
  is the definition of "defensible."

## What this feeds into

- **Exercise 05** — the decisions here populate the
  `Response`, `Plan`, `Boundary`, and `Next
  review` columns of the inventory, and become
  decision-log entries.
- **Lab 01** — the portfolio decision log the lab
  publishes uses these memos verbatim (with light
  polish) as its decision records.
- **Capstones** — the debt-portfolio sections of
  [`project-102`](../../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package/)
  (security / compliance debt) and
  [`project-103`](../../../projects/project-103-scaling-plan-from-five-to-fifty-engineers/)
  (scaling-plan debt) reuse the decision-tree
  discipline for their debt items.

The drill is one round of decisions; the artifact is
recurring. Every quarter, the leave-with-revisit items
whose revisit date lands get re-decided; new items
arrive and get their first decision; the response mix
shifts as the portfolio changes shape.
