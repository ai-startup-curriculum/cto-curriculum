# Quality-Attribute Debt vs. Structural Debt

> "Not all debt is created equal. Refactoring a slow query
> and re-designing an aggregate boundary look similar on a
> whiteboard and cost completely different amounts to do."
> — a paraphrase widely used in the field; the underlying
> distinction is worked in Ford, Parsons and Kua,
> *Building Evolutionary Architectures*
> ([oreilly.com](https://www.oreilly.com/library/view/building-evolutionary-architectures/9781491986356/)).

## Motivation

Chapter 01 gave you the Fowler quadrant labels for
*classifying* debt items. This chapter gives you the
labels for *the debt itself* — the two families of debt
that pretty much every item in a startup codebase falls
into, and that have completely different sizing (chapter
03), budgeting (chapter 04), and treatment (chapter 05)
profiles.

If chapter 01 is the answer to *"was taking this debt on
a good decision or a bad one?"*, this chapter is the
answer to *"what kind of debt is it?"*. Confusing the two
kinds is the second most common failure mode in the
startup-debt conversation (the first is treating debt as
moral rather than financial, per chapter 01):

- Quality-attribute debt is often *cheap and mechanical*
  to fix — a slow query gets an index; a missing
  monitor gets a Datadog check; a missing input
  validation gets a middleware. It is priced against
  the ISO/IEC 25010 characteristic it regresses.
- Structural debt is often *expensive and load-bearing*
  to fix — the aggregate boundary is wrong; the
  billing state machine is spread across three
  services; the auth check is inlined at 47 call sites.
  It is priced against the *rate of future change* the
  wrong shape imposes a tax on.

Both are real debt. Both have a business case for
repayment. But the cost model, the risk profile, and the
choice of response (deprecate / rewrite / leave) all
diverge sharply depending on which family the item
belongs to.

## Quality-attribute debt

**Quality-attribute debt** is a regression in one of the
ISO/IEC 25010:2023 non-functional characteristics
([iso.org/standard/78176](https://www.iso.org/standard/78176.html);
walked in
[`mod-102` chapter 04](../mod-102-architecture-under-uncertainty/04-iso-25010-quality-attribute-trade-offs.md))
against the level the product actually needs at its
current stage.

Concretely, quality-attribute debt items look like:

- **Reliability debt** — the p99 API latency is 3.2
  seconds and the SLO the enterprise contract requires
  is 500ms. The retry logic has a known bug that
  amplifies transient upstream failures. The
  background-job queue silently drops jobs on worker
  restart.
- **Performance-efficiency debt** — the `/customers`
  endpoint runs an N+1 query that hits the DB 300
  times per page load. The batch job scales linearly
  with row count and is projected to exceed the
  nightly window in six months.
- **Security debt** — the CSRF middleware is missing on
  three admin routes. The password-reset flow uses
  URL-embedded tokens with no expiry. The dependency
  scanner flags 12 known CVEs on the current
  lockfile. See [`mod-107` chapter 02](../mod-107-founder-scope-security-and-compliance/README.md)
  for the founder-scope security playbook that
  prioritises these.
- **Maintainability debt** — no tests exist for the
  refund-processing module (test coverage is 0% and it
  is edited on every enterprise commit). Onboarding a
  new engineer takes 12 days because the local-dev
  setup involves seven undocumented steps.
- **Interaction-capability debt** — the admin console
  requires the CTO to hand-craft SQL updates because
  the UI never got past a spike.
- **Portability debt** — the deploy pipeline requires a
  specific engineer's laptop because a credential lives
  only in their keychain.
- **Compatibility debt** — the API version the mobile
  client depends on was deprecated three quarters ago
  and cannot be removed without breaking two dozen
  installs that never updated.
- **Functional-suitability debt** — the feature ships
  but only for the happy path; every edge case
  produces an ambiguous error that the support team
  has learned to translate.

Two useful properties of quality-attribute debt:

- **The fix is usually local.** The change is bounded
  to the module, the test file, the middleware, the
  query, the pipeline configuration, the dependency
  bump. The blast radius is small; the risk of the
  rewrite going sideways is small; the confidence in
  the estimate is relatively high.
- **The metric is legible.** Reliability debt has an
  SLO. Performance debt has a p95 number. Security
  debt has a CVE score and an OWASP ASVS reference
  ([owasp.org/www-project-application-security-verification-standard](https://owasp.org/www-project-application-security-verification-standard/)).
  Maintainability debt has a test-coverage number and
  an onboarding-time number. The board conversation is
  easier because the *before* and *after* are numbers.

The failure mode with quality-attribute debt is treating
it as *just* an engineering concern. It isn't — it maps
directly to customer commitments (an SLO in a contract),
to compliance milestones (an ASVS or SOC 2 control), or
to hiring throughput (an onboarding-time number). Chapter
04 handles the mapping so that the debt has a *business
owner*, not just an engineering owner.

## Structural debt

**Structural debt** is a mismatch between the *shape* of
the code and the *shape* of the domain. It is the debt
Cunningham was actually describing in 1992 — the
first-time-through code that shipped fast, taught the
team the domain, and now no longer matches what the team
has learned.

Concretely, structural debt items look like:

- **Wrong abstraction** — the `Order` object was
  designed for one-off retail sales; the product has
  since acquired subscriptions, hybrid subscription-plus-
  usage, gifted subscriptions, and marketplace
  transactions. Every new pricing model requires
  branching inside `Order.calculateTotal()`. Sandi
  Metz's essay
  *"The Wrong Abstraction"*
  ([sandimetz.com/blog/2016/1/20/the-wrong-abstraction](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction))
  is the canonical treatment: *duplication is far
  cheaper than the wrong abstraction*.
- **Coupling / feature envy** — the `PricingEngine` and
  the `NotificationService` know about each other's
  internal state; changes to one propagate to the
  other; the aggregate boundary between them is not
  actually enforced. Eric Evans's *Domain-Driven Design*
  ([domainlanguage.com/ddd](https://www.domainlanguage.com/ddd/))
  is the classical reference on aggregate boundaries.
- **Missing seams** — the auth check is inlined at 47
  call sites. Adding tenant-scoped auth requires
  changing all 47. There is no single place to
  intercept.
- **Architecture misfit** — the team chose microservices
  at seed and now runs eight services in production;
  every feature crosses three of them; there is no
  team topology that maps naturally to the split. See
  [`mod-102` chapter 05](../mod-102-architecture-under-uncertainty/05-monolith-modular-monolith-services-and-cap.md)
  on the modular-monolith default, and Sam Newman's
  *Monolith to Microservices*
  ([samnewman.io/books/monolith-to-microservices](https://samnewman.io/books/monolith-to-microservices/))
  on decomposition when it *does* pay off.
- **Un-modelled invariant** — the domain has an
  invariant nobody wrote down (e.g. "a refund can only
  be issued against a captured payment"); it is
  enforced by convention in three places and bypassed
  in one, and the bypass is where the bug is.
- **Ownership vacuum** — a system that nobody
  currently owns; every change is done by whoever last
  touched it. This is a topology / [Team Topologies](https://teamtopologies.com/book)
  debt as much as a code debt. See
  [`mod-104` chapter 04](../mod-104-first-engineering-hires-and-team-topology/04-team-topologies-at-startup-scale.md).

Two useful properties of structural debt:

- **The fix is usually global.** The change is not
  bounded to a module — the whole point is that the
  module boundary is wrong. The blast radius is large;
  the risk of the rewrite going sideways is high; the
  estimate variance is high. This is exactly the case
  Chesterton's Fence and StranglerFig were invented
  for (chapter 05).
- **The metric is not legible.** There is no p95 for
  "this aggregate boundary is in the wrong place";
  there is no CVE for "this abstraction is wrong". The
  interest rate is real (chapter 03 sizes it) but it
  is inferred from the *rate of change* the debt taxes,
  not read off a dashboard. Board conversations about
  structural debt are harder than board conversations
  about quality-attribute debt for exactly this reason.

## The two families require different responses

Chapter 05 handles the three responses (deprecate,
rewrite, leave) in detail; the fork happens here:

- **Quality-attribute debt** is almost always *leave-
  and-fix-in-place*. You add the missing index, you fix
  the middleware, you write the tests. The rewrite
  discipline (Chesterton's Fence, StranglerFig) is
  rarely necessary because the change is local. The
  refactor budget (chapter 04) covers it.
- **Structural debt** is where the deprecate-vs-rewrite-
  vs-leave decision actually bites. Because the fix
  is global, all three responses are live:
  - **Deprecate** the feature the mis-shaped code
    supports (if a business owner will sign off — see
    chapter 04); the debt goes away for free.
  - **Rewrite** using StranglerFig
    ([martinfowler.com/bliki/StranglerFigApplication.html](https://martinfowler.com/bliki/StranglerFigApplication.html))
    so the transition is incremental and the risk is
    bounded; this is the response for load-bearing
    structural debt.
  - **Leave** and pay the carry cost, explicitly, and
    revisit next quarter; this is the response when
    the structural debt is real but the business
    value of the fix is not yet worth the cost.

The framework the CTO carries into a technical-debt
review meeting looks like:

```
For each debt item:
  1. Fowler quadrant (chapter 01) — is this a loan we
     should keep or a bad debt we should stop?
  2. Family (this chapter) — quality-attribute or
     structural?
  3. Cost-to-carry (chapter 03) — engineering-hours
     per week, and the depreciation curve.
  4. Business owner (chapter 04) — which customer
     commitment, compliance milestone, or hiring
     throughput does this connect to?
  5. Response (chapter 05) — deprecate, rewrite, or
     leave, defended on the previous four columns.
  6. Portfolio row (chapter 06) — one row in the
     inventory / decision log an incoming VP Eng
     can read.
```

## Two mixed / edge cases worth naming

- **The "quality-attribute regression that is actually
  structural."** A slow query looks like performance
  debt, but the real cause is that the domain model
  requires a `JOIN` across two aggregates that should
  never have been split (or should never have been
  merged). Adding the index treats the symptom; the
  interest keeps compounding because the next feature
  will hit the same misalignment. The diagnostic is:
  after the local fix ships, does the same *shape* of
  bug recur within a quarter? If yes, it was structural.
- **The "structural debt that is actually a business
  pivot."** Sometimes the code doesn't match the domain
  because *the business has changed and nobody told
  engineering*. The `Order` model doesn't fit
  subscriptions because the product used to be
  transactional and pivoted to SaaS. Refactoring in
  isolation of that pivot is engineering solving the
  wrong problem; the debt inventory needs to name the
  pivot as the driver.

Both edge cases are why chapter 06's inventory format
carries a `driver` column — the business fact this debt
item is a downstream consequence of. Without it the debt
review turns into an architecture debate.

## The relationship to ISO/IEC 25010

Quality-attribute debt is priced *directly* against the
ISO/IEC 25010 characteristic it regresses. The list in
this chapter is one line per characteristic (reliability,
performance efficiency, security, maintainability,
interaction capability, portability, compatibility,
functional suitability) — the eight characteristics of
the 2023 revision
([iso.org/standard/78176](https://www.iso.org/standard/78176.html))
plus the ninth characteristic *flexibility* the 2023
revision adds.

Structural debt is *not* priced against a single ISO/IEC
25010 characteristic — the whole point is that the shape
is wrong, and the wrong shape usually taxes several
characteristics at once (a wrong aggregate boundary
usually hurts maintainability, performance efficiency,
and reliability simultaneously). This is why chapter 03's
cost-to-carry sizing has to be measured on *engineering-
hours per week paid to the debt*, not on a single ISO
number.

The chapter-04 quality-attribute ranking in mod-102 is a
useful cross-check: if you rank Maintainability at #1
for your stage (typical seed-stage default) and your
debt portfolio is 80% structural, then the portfolio is
reflecting your stated ranking correctly. If you rank
Maintainability at #1 and your portfolio is 80% security
debt, either the ranking is wrong or the portfolio
represents a genuine emergency you need to handle first.

## Failure modes

- **The "everything is a rewrite" portfolio.** Every
  item on the debt list is treated as structural, so
  every item is priced as a multi-quarter rewrite. This
  is expensive and usually wrong — most debt items are
  quality-attribute regressions with local fixes.
  Fix: sort the list into the two families first, and
  count how much of each you actually have.
- **The "everything is a middleware" portfolio.** The
  reverse: every item is treated as quality-attribute,
  so every fix is scoped as a two-day ticket. The
  structural items keep coming back with different
  faces (see the "regression that is actually
  structural" edge case). Fix: after each quality-
  attribute fix, ask if the same shape of bug is
  likely to recur; if yes, escalate to structural.
- **The un-labelled portfolio.** The debt list is a
  wall of prose with no family labels. The board
  reader cannot tell what kind of decisions they are
  about to be asked to fund. Fix: chapter 06's
  inventory format is columnar and labels every row.
- **The premature-abstraction structural debt.**
  Structural debt that comes from *over-abstracting
  too early* — a plugin architecture built for
  imagined future extensions that never materialised.
  This is the mirror of Sandi Metz's *"prefer
  duplication over the wrong abstraction"*. Fix: the
  same StranglerFig discipline chapter 05 walks — you
  can strangle a premature abstraction back down to
  the concrete cases just as you can strangle a
  legacy service.

## Summary

- **Quality-attribute debt** is a regression in one of
  the ISO/IEC 25010 non-functional characteristics
  (reliability, performance efficiency, security,
  maintainability, interaction capability, portability,
  compatibility, functional suitability). Fixes are
  usually local. Metrics are usually legible.
- **Structural debt** is a mismatch between the shape
  of the code and the shape of the domain — wrong
  abstraction, wrong aggregate boundary, missing seam,
  architecture misfit, un-modelled invariant, ownership
  vacuum. Fixes are usually global. Metrics are
  inferred from the *rate of change* the debt taxes.
- **Different responses.** Quality-attribute debt is
  almost always *leave-and-fix-in-place* within the
  refactor budget (chapter 04). Structural debt is
  where the deprecate-vs-rewrite-vs-leave decision
  (chapter 05) actually bites, because the fix is
  global.
- **Two edge cases** to watch for: the quality-
  attribute regression that is actually structural
  (fix ships, same shape of bug recurs), and the
  structural debt that is actually a downstream
  consequence of a business pivot nobody told
  engineering about.
- The **inventory row** for every debt item names the
  family, the ISO/IEC 25010 characteristic (if quality-
  attribute), and the business driver (chapter 06).

The chapter's paired exercise —
[`exercise-01-fowler-quadrant-categorisation-drill.md`](exercises/exercise-01-fowler-quadrant-categorisation-drill.md)
— asks you to label ten real debt items with both
Fowler quadrant *and* family; the two labels together are
the minimum a portfolio-line description needs.
Chapter 03 sizes the cost-to-carry for each item; chapter
04 ties it to a business owner; chapter 05 chooses the
response; chapter 06 formats the whole thing as a
portfolio a board member can read.
