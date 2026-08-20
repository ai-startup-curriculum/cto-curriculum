# The Cunningham Metaphor and the Fowler Quadrants

> "Shipping first time code is like going into debt. A
> little debt speeds development so long as it is paid back
> promptly with a rewrite... The danger occurs when the debt
> is not repaid. Every minute spent on not-quite-right code
> counts as interest on that debt." — Ward Cunningham, 1992
> OOPSLA experience report
> ([c2.com/doc/oopsla92.html](http://c2.com/doc/oopsla92.html);
> video summary at
> [youtube.com/watch?v=pqeJFYwnkjE](https://www.youtube.com/watch?v=pqeJFYwnkjE)).

## Motivation

Every founder-CTO has been in the room for a version of
this conversation:

- **The senior engineer:** *"We really need to rewrite the
  billing service. It's a mess."*
- **The CEO:** *"Can we just add the enterprise SSO feature
  first? Sales has a demo Thursday."*
- **The CTO:** *"...how much of the enterprise SSO work is
  actually blocked by the billing mess?"*

Two answers to that last question are common and both are
wrong. The first — *"It isn't, we just want to rewrite it"*
— reveals a moral framing (bad code offends us; therefore
we must fix it). The second — *"All of it, we can't ship
anything until we rewrite"* — reveals a catastrophic framing
(the code is beyond redemption; therefore only the
rewrite counts). Neither answer belongs on the CEO's desk,
because neither answer is a **business** framing.

The business framing exists. Ward Cunningham published it
at OOPSLA in 1992 as the **debt metaphor**. Martin Fowler
extended it in 2009 into a **quadrant** that separates the
kind of debt worth taking from the kind that eats you.
Together they give the CTO a vocabulary that turns "we
need to rewrite the billing service" into a portfolio
line item with a principal, an interest rate, a
counterparty, and a repayment plan.

This chapter walks the two references, names the four
misreadings that turn the metaphor into a cudgel, and sets
up the sizing (chapter 03), budgeting (chapter 04), and
decision (chapter 05) chapters that follow.

## Cunningham's original metaphor — debt as a financial instrument

The 1992 report is short (one page) and worth reading in
full ([c2.com/doc/oopsla92.html](http://c2.com/doc/oopsla92.html)).
Cunningham had been writing a portfolio-management system
for a customer using WyCash — a Smalltalk framework — and
observed that shipping "first-time-through" code was
useful *if* the team then rewrote it as their
understanding of the domain grew. He named the pattern
after a financial-services concept his customer would
already recognise:

- **Principal** — the amount of "not-quite-right code"
  currently in the system.
- **Interest** — the ongoing cost of working *around*
  that code every time you touch it. Not paid at some
  future date. Paid continuously, as a tax on every
  change.
- **Repayment** — refactoring the not-quite-right code
  until the shape of the system matches the shape of
  the domain.
- **Default** — the state where the interest cost has
  grown so large that all engineering effort goes into
  servicing debt and none into new value. Cunningham's
  memorable phrase: *"entire engineering organisations
  can be brought to a stand-still under the debt load."*

The critical property of the original metaphor — and the
one the modern retelling most often loses — is that
Cunningham's debt is **deliberate**. It is a technique
for shipping learning code fast, on the *explicit
understanding* that you will refactor once the domain is
clearer. He is not describing sloppy work. He is
describing a **loan** used to accelerate delivery, priced
against the interest cost of servicing it.

Cunningham himself has been direct about the misreading —
see his 2009 clarification video
([youtube.com/watch?v=pqeJFYwnkjE](https://www.youtube.com/watch?v=pqeJFYwnkjE))
— where he distinguishes his intent (a *deliberate*
learning-and-refactor loop) from the modern default
usage (any code you don't like). The distinction matters
because the two things have completely different
treatments in a business conversation.

## Fowler's quadrant — the 2×2 that separates loans from bad debts

Martin Fowler picked the metaphor up in 2009 and added a
second axis, publishing the result as a bliki entry
titled *TechnicalDebtQuadrant*
([martinfowler.com/bliki/TechnicalDebtQuadrant.html](https://martinfowler.com/bliki/TechnicalDebtQuadrant.html)).
The two axes:

- **Deliberate vs. Inadvertent** — did the team *know*
  they were taking on debt at the time they did it?
- **Prudent vs. Reckless** — did the team make a
  considered trade-off, or a careless one?

The four cells are named in the bliki entry directly and
each cell has a canonical example:

```
                    | Reckless                     | Prudent
--------------------|------------------------------|------------------------------
Deliberate          | "We don't have time for      | "We must ship now and deal
                    |  design"                     |  with the consequences"
--------------------|------------------------------|------------------------------
Inadvertent         | "What's Layering?"           | "Now we know how we should
                    |                              |  have done it"
```

Read the cells the way a lender reads a loan file:

- **Deliberate + Prudent** — *"We must ship now and deal
  with the consequences."* This is Cunningham's original
  loan. The team named the debt, priced it against the
  urgency of shipping (a customer commitment, a
  compliance milestone, a competitive deadline), and
  will pay it back when the shipping pressure eases.
  This debt is a **feature** of a shipping org, not a
  bug. Most startup CTOs need *more* of this debt in
  their portfolio, not less.
- **Deliberate + Reckless** — *"We don't have time for
  design."* The team knows the design will not survive
  the next customer, and they take the shortcut anyway.
  This is the debt that compounds. It is the founder-CTO
  who says "we're pre-PMF, we don't have time for tests"
  — and then finds twelve months later that they can't
  ship without breaking three subsystems on every
  change. Almost always the wrong loan.
- **Inadvertent + Prudent** — *"Now we know how we should
  have done it."* The team designed carefully, shipped,
  and only *after* learning more about the domain did
  they realise the original abstraction was wrong. This
  is the debt that comes from Cunningham's original
  observation — early code is domain-learning code,
  and the domain teaches you things the initial design
  couldn't know. This debt is a **signal**, not a
  failure — its appearance means the team is learning.
- **Inadvertent + Reckless** — *"What's Layering?"* The
  team didn't know a better shape existed. This is the
  debt of an org that has hired people who cannot see
  the design pathologies they are producing. The fix
  is *not* refactoring — the fix is either training,
  hiring, or bringing in a technical advisor. See
  [`mod-104` chapter 03](../mod-104-first-engineering-hires-and-team-topology/03-founding-engineer-profile-and-first-project.md)
  on the founding-engineer profile that guards
  against this cell filling up.

The value of the quadrant is that it makes the debt
conversation *actionable*. A ten-item debt list becomes a
portfolio: three items are prudent deliberate loans that
just need repayment; two are inadvertent prudent
signals that the domain has shifted and the design needs
to catch up; four are reckless items you should either
stop-loss (deprecate the feature, buy the vendor) or
refuse to accumulate more of (hire differently); one is
somebody's pet rewrite that turns out not to be debt at
all when you dig in. The CTO's job is to run that
sorting.

## Debt is not a moral failing

Two failure modes come from treating debt as moral rather
than financial:

- **The purity-driven refactor.** An engineer with a
  strong aesthetic reaction to a piece of code declares
  it "unmaintainable" and starts a rewrite the roadmap
  does not have room for. The CTO who cannot separate
  "I dislike this code" from "the interest rate on this
  code is X hours per week" cannot arbitrate the
  conversation. See the deprecate-vs-rewrite-vs-leave
  decision drill in chapter 05.
- **The moral-hazard cover-up.** The team took on
  deliberate reckless debt to hit a shipping date,
  shipped, and now refuses to name the debt because
  naming it would be admitting a bad decision. The
  interest quietly compounds. The debt inventory
  (chapter 06) exists specifically to counter this — you
  name the debt on the record, and the naming *is* the
  first repayment.

The frame the CTO carries into the CEO / board
conversation is: **debt is a financial instrument the
engineering org uses to accelerate value delivery**. It
has a principal (what needs to change), an interest rate
(the cost-to-carry you will size in chapter 03), a
counterparty (the business owner who took the loan; see
chapter 04), and a repayment plan (deprecate, rewrite, or
leave — chapter 05). Framed that way, "we need to spend
20% of next quarter on debt" is a resource-allocation
conversation the board has already had thirty times about
other financial instruments — R&D vs. sales, capex vs.
opex, marketing spend against payback period. Framed as
"we need to rewrite because the code is bad" it is not.

## Where the metaphor stops being useful

The debt metaphor is a communication tool, not a
mathematical model. Two places it breaks down that the
CTO should signal in the room:

- **The interest rate is not fixed.** Financial interest
  is a contract; technical interest is a rate that
  *rises* as the codebase and team grow. Chapter 03 on
  cost-to-carry and the *depreciation schedule* handles
  this — the same piece of debt costs 2 hours per week
  at team-size 5 and can cost 30 hours per week at
  team-size 30, because more people touch it and each
  touch pays the tax.
- **There is no bankruptcy court.** The financial-debt
  metaphor implies that at some limit the org can
  restructure and walk away. In software the closest
  analogue is a full rewrite — and the rewrite has its
  own well-documented failure modes (Netscape 6, the
  Joel Spolsky essay
  *"Things You Should Never Do, Part I"* at
  [joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/)).
  Chapter 05 handles this with the Chesterton's Fence /
  StranglerFig discipline that separates the rewrite
  that might work from the one that has a 70% chance of
  killing the company.

The extended debt vocabulary — Steve McConnell's
*unintentional vs. intentional* framing, published on
his blog in 2007
([stevemcconnell.com/blog/managing-technical-debt](https://stevemcconnell.com/articles/technical-debt/)) —
predates and overlaps Fowler's quadrants. Fowler's is the
version the industry has converged on because the 2×2
gives you a diagnostic *and* a treatment plan, but
McConnell's version is worth knowing when a stakeholder
reaches for it.

## Summary

- **Ward Cunningham** introduced technical debt in a
  1992 OOPSLA experience report
  ([c2.com/doc/oopsla92.html](http://c2.com/doc/oopsla92.html))
  as a **deliberate** technique: ship learning code fast
  and refactor once the domain is clearer. The
  principal / interest / repayment / default vocabulary
  is his.
- **Martin Fowler** added the second axis in the 2009
  *TechnicalDebtQuadrant* bliki entry
  ([martinfowler.com/bliki/TechnicalDebtQuadrant.html](https://martinfowler.com/bliki/TechnicalDebtQuadrant.html))
  — **Deliberate vs. Inadvertent × Prudent vs.
  Reckless** — giving four cells with distinct treatments.
- The **Deliberate + Prudent** cell is Cunningham's
  original loan and is a **feature** of a shipping
  startup, not a failure. Most startup CTOs need more of
  this debt in their portfolio, not less.
- The **Deliberate + Reckless** cell is the debt that
  compounds and eats orgs. Refuse it.
- The **Inadvertent + Prudent** cell is the *signal that
  the team is learning*. Refactor with the new
  understanding, do not blame the past self who couldn't
  have known.
- The **Inadvertent + Reckless** cell is a *hiring /
  training* problem, not a refactor problem. See
  [`mod-104` chapter 03](../mod-104-first-engineering-hires-and-team-topology/03-founding-engineer-profile-and-first-project.md).
- Treat debt as a **financial instrument**, not a moral
  failing. This makes the CEO / board conversation about
  resource allocation, which the board has had many
  times before, rather than about rewriting, which
  frightens them.
- The metaphor is a communication tool, not a math
  model. Chapter 03 handles the rising-interest-rate
  case; chapter 05 handles the "no bankruptcy court"
  case with Chesterton's Fence / StranglerFig.

The chapter's paired exercise —
[`exercise-01-fowler-quadrant-categorisation-drill.md`](exercises/exercise-01-fowler-quadrant-categorisation-drill.md)
— walks you through categorising the ten most
recognisable debt items in your (or a real reference)
codebase into the four cells and separating the loans
you should keep from the bad debts you need a plan for.
Chapter 02 distinguishes **quality-attribute debt** from
**structural debt**, so that the portfolio-line labels
are precise enough to defend. Chapter 03 sizes the
interest rate that lets the debt be compared against
other engineering-time uses.
