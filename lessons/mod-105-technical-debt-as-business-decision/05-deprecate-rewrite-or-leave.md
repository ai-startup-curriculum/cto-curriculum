# Deprecate, Rewrite, or Leave — The Three Responses

> "In the matter of reforming things, as distinct from
> deforming them, there is one plain and simple principle;
> a principle which will probably be called a paradox.
> There exists in such a case a certain institution or law;
> let us say, for the sake of simplicity, a fence or gate
> erected across a road. The more modern type of reformer
> goes gaily up to it and says, 'I don't see the use of
> this; let us clear it away.' To which the more intelligent
> type of reformer will do well to answer: 'If you don't
> see the use of it, I certainly won't let you clear it
> away. Go away and think. Then, when you can come back
> and tell me that you do see the use of it, I may allow
> you to destroy it.'" — G. K. Chesterton, *The Thing*
> (1929)
> ([gutenberg.ca — Chesterton, *The Thing*](https://gutenberg.ca/ebooks/chestertongk-thething/chestertongk-thething-00-h.html)).

## Motivation

For each debt item in the portfolio (chapters 01-03),
sized against a business owner (chapter 04), there are
only three genuinely available responses:

- **Deprecate** — remove the feature the debt
  supports. The debt goes away for free.
- **Rewrite** — replace the mis-shaped code with a
  new shape. Do it *incrementally* using the
  StranglerFig pattern
  ([martinfowler.com/bliki/StranglerFigApplication.html](https://martinfowler.com/bliki/StranglerFigApplication.html)),
  and *only* after passing the Chesterton's Fence
  check.
- **Leave** — do nothing to the code; pay the
  cost-to-carry (chapter 03) explicitly, and
  revisit the decision next quarter.

Startups reflexively pick "rewrite" because it feels
like decisive action. The two most common failures in
debt management are (i) rewriting things that should
have been deprecated (you paid the migration cost for a
feature nobody was going to use), and (ii) rewriting
things that should have been left alone (you paid the
migration cost and introduced new bugs to replace old
ones the team had already routed around).

This chapter walks the decision. The output is a per-item
choice — one of the three — defended on the four columns
you already have (Fowler quadrant, family, cost-to-
carry, business owner). Chapter 06 is where the choices
land in the inventory / decision log; this chapter is
where the choices are *made*.

## Deprecate — the cheapest response

Deprecation is almost always the best option that is
almost never seriously considered. Debt that supports a
feature nobody uses is debt whose principal is *zero* —
the fix is "delete the code" and the migration cost is
"remove one route from the marketing site". This is
"do less" as the primary refactor tool.

Signals a debt item is a deprecation candidate:

- **Usage data says the feature is dead** — analytics
  show <1% of active users touch it, or the last
  invocation was six months ago.
- **The feature has no business owner** (per chapter
  04). No one on the business side benefits from
  keeping it, and no one will defend it in a
  deprecation review.
- **The feature was built for a customer who churned,
  or a market segment the company pivoted away from**
  — the *"structural debt that is actually a
  business pivot"* edge case from chapter 02.
- **The feature is one of several alternatives to the
  same job** and one of the others has clearly won —
  the CSV export the CTO built as a spike is still
  live even though a first-class integrations platform
  now serves the same use case, generating a decade
  of maintenance obligations for zero incremental
  value.

The deprecation *process* — the customer-communication
piece, the notice window, the sunset date — is a joint
piece of work with Product / Marketing (the customer
notice) and Customer Success (the outreach to affected
accounts). Marty Cagan's writing on product decisions —
*Inspired* / *Empowered* — is the reference on the
product-side discipline
([svpg.com/books](https://www.svpg.com/books/)); the
CTO's contribution is the sunset engineering plan
(feature-flag off in staging; feature-flag off in
production behind a quiet-hours window; code removal in
the next release; final documentation-only presence for
one more quarter, then gone).

Two things the CTO must resist:

- **The "we might need it later" argument.** You will
  not. And if you do, the code is still in git
  history. The maintenance cost of keeping unused
  code around exceeds the cost of resurrecting it
  from history when the need re-appears.
- **The "one customer still uses it" argument.** One
  customer means the deprecation is a targeted
  customer conversation, not a broadcast one. It does
  *not* mean the feature stays live for everyone
  else. See Customer Success's playbook for the
  target-account version.

## Rewrite — the response with the biggest downside

Rewrites are *load-bearing*: the cost is large, the
downside is catastrophic, and the industry has enough
scars from failed rewrites that a specific discipline
has grown up around when to do them and how.

Two guardrails before a rewrite is on the table.

### Guardrail 1 — Chesterton's Fence

The G. K. Chesterton quote at the top of the chapter is
the discipline. The rule: **before removing or replacing
any piece of code you don't understand the purpose of,
you must first be able to explain why it exists in its
current form**. Not from git-blame guesswork — from
either (i) archival records (ADRs — see
[`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md)),
(ii) an incident post-mortem that motivated it, (iii) a
customer requirement it satisfies, or (iv) a
conversation with someone who was in the room.

The failure mode Chesterton's Fence prevents: the
rewrite that removes what looks like a redundant check
and re-introduces the exact bug that check was added to
fix, three years after the incident. Every experienced
CTO can name at least one of these; the fence is what
prevents the next one.

Operationally in a rewrite plan:

- For every non-obvious piece of the code being
  replaced, note *why it exists*. If you cannot
  answer, either find someone who can or leave that
  piece in place until you can.
- If the rewrite is being done *specifically because
  the current code is un-explainable*, the rewrite
  team's first three weeks are archaeology, not
  coding. Archaeology outputs are ADRs written
  retroactively (yes, even for the old system) so
  that the *new* system can honour the constraints
  the old system encoded.

### Guardrail 2 — the StranglerFig pattern

Martin Fowler's *StranglerFigApplication*
([martinfowler.com/bliki/StranglerFigApplication.html](https://martinfowler.com/bliki/StranglerFigApplication.html))
is the incremental-migration pattern that turns a
rewrite from an all-or-nothing risk into a series of
small, reversible risks. The name comes from the
strangler-fig tree that gradually envelops its host
until the host dies without the tree ever having to fell
it explicitly. Applied to software:

- Put the new system *alongside* the old system.
- Route *some subset* of traffic (one endpoint, one
  customer segment, one feature flag, one entity
  type) through the new system.
- Verify parity against the old.
- Migrate another subset.
- Repeat until the last traffic is off the old system.
- Only *then* delete the old.

The properties this gives you:

- **Every migration step is reversible.** If the new
  path breaks, you flip the flag back and the old
  path takes over. The blast radius per step is
  bounded.
- **The team can absorb feature work during the
  migration.** A big-bang rewrite forbids feature
  work in the migrated area until the migration
  ships; the strangler pattern lets feature work
  continue against the old system while the new
  system is being built.
- **The estimate is honest.** Big-bang rewrites are
  famously bad estimates because the *"we'll flip
  over at the end"* step compresses six categories
  of risk into one deadline. The strangler pattern
  distributes the risk across many small steps you
  can estimate individually.

The counter-example that made the pattern famous —
Netscape's rewrite of Netscape 4 into Netscape 6, which
lost the market to Internet Explorer — is Joel Spolsky's
*"Things You Should Never Do, Part I"*
([joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/)).
Read the essay before you start a rewrite; it is 20
years old and every sentence still applies. Sam
Newman's *Monolith to Microservices*
([samnewman.io/books/monolith-to-microservices](https://samnewman.io/books/monolith-to-microservices/))
is the more recent book-length treatment specifically
for the service-extraction case.

The rewrite response is the right one when:

- The debt is **structural** (chapter 02) and the
  fix genuinely requires re-shaping (not just fixing
  in place).
- The **cost-to-carry** (chapter 03) is high enough
  that a StranglerFig-scale investment is defensible
  against feature work.
- A **business owner** exists (chapter 04) who wants
  the debt paid down because a specific commitment is
  blocked by it.
- The **Chesterton's Fence check** passes — the team
  can articulate why the current code is the shape it
  is, and knows which constraints the new code must
  honour.
- The team has the **StranglerFig discipline** —
  incremental migration with reversible steps, not a
  big-bang cutover.

## Leave — the response CTOs under-use

"Leave" is not "ignore." It is a *deliberate* decision
to pay the ongoing cost-to-carry (chapter 03) because
either (i) the fix is more expensive than the carry, or
(ii) the fix would displace higher-priority work whose
value exceeds the debt's compounding rate, or (iii) the
item is expected to be **superseded** by a larger
change (a pivot, an acquisition, a customer segment
change) whose arrival makes the fix moot.

Signals a debt item is a *leave* candidate:

- **Low cost-to-carry** in absolute terms — under 2
  hours/week — and a flat depreciation curve. The
  interest is cheap; paying principal is a poor use of
  the refactor budget.
- **High cost-to-fix relative to carry.** Some
  structural debt is genuinely eye-wateringly
  expensive to fix (a fundamental data-model change
  requires a two-quarter migration with every
  customer). If the carry is 4 hours/week for two
  more quarters until superseded, the honest math
  says leave.
- **Expected supersession.** An enterprise contract
  under negotiation would triple the traffic and
  force a re-architecture anyway; the current shape
  is going to have to change for a *different* reason
  in six months; local fixes now are wasted.
- **The mostly-fine legacy.** A subsystem that hasn't
  been touched in two years, has no incidents, has
  no upcoming feature requirements, and is
  well-encapsulated. The right move is often "leave
  it and defend the encapsulation".

"Leave" requires the same discipline as the other two
responses:

- The decision is **explicit in the inventory** —
  the row's *response* column reads "Leave / revisit
  Q2" or similar, not "no action taken."
- The **carry cost is named** — the decision
  acknowledges you are choosing to pay X hours/week
  in exchange for freeing that budget for higher-
  priority work.
- The **revisit date is set** — chapter 06's decision
  log includes a next-review date. "Leave" is a
  time-boxed decision, not a permanent one.

## The decision tree

The tree the CTO carries into the debt-portfolio review:

```
For each debt item:
  1. Does the underlying feature still have a business
     owner (chapter 04)?
       No  → DEPRECATE (chapter 06 tracks the sunset
              plan).
       Yes → continue.

  2. Is the debt QUALITY-ATTRIBUTE or STRUCTURAL
     (chapter 02)?
       Quality-attribute
         → LEAVE-AND-FIX-IN-PLACE via the refactor
           budget (chapter 04); this is not the
           deprecate-vs-rewrite question. Move on.
       Structural
         → continue.

  3. Is the cost-to-carry (chapter 03) high enough,
     and is the depreciation curve steep enough, that
     the compounding will exceed the fix cost within
     4-6 quarters?
       No  → LEAVE (set explicit revisit date; chapter
              06 records).
       Yes → continue.

  4. Does the Chesterton's Fence check pass? Can
     someone explain WHY the current code is the shape
     it is, from ADRs / post-mortems / customer
     requirements / archival conversations?
       No  → PAUSE. Do archaeology first (write
              retroactive ADRs). Do not start the
              rewrite until the fence is understood.
       Yes → continue.

  5. Do you have the team, the runway, and the
     political room for a StranglerFig-shape
     migration — incremental, reversible, feature-work-
     compatible?
       No  → LEAVE (revisit when you do; you are not
              being cowardly, you are being sane).
       Yes → REWRITE via StranglerFig.
```

The tree is not fancy. Its value is that it forbids
skipping any of the five decisions.

## Boundary — where this CTO ends and the senior architect begins

Two rewrites are out of scope for the pre-Series-A CTO
and defer up to
[`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
(level 45) or
[`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
(level 55):

- **The multi-quarter, multi-team system extraction**
  — carving a payments system out of a 500K-LOC
  monolith serving 50 million users; splitting a
  monorepo across three business units. The tactical
  choreography (per-endpoint traffic shifting, dual-
  write patterns, schema-migration playbooks,
  organisational-topology alignment) is deeper than
  StranglerFig's headline pattern and is the senior-
  architect's / principal-architect's craft. The
  pre-Series-A CTO calls out that this is where the
  scope defers upward and does not attempt to own
  the choreography themselves.
- **The multi-region / multi-tenant re-architecture
  under active production traffic.** Any rewrite
  that requires coordinated cutovers across regions,
  or that changes the tenancy model (silo ↔ pool ↔
  bridge — see the AWS SaaS Lens at
  [docs.aws.amazon.com/wellarchitected/latest/saas-lens](https://docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html))
  is a senior-architect-scope engagement.

The pre-Series-A CTO's job on these is to (i) recognise
them, (ii) not attempt them alone, (iii) either bring
in a technical advisor or defer the decision until a
principal-scope hire can own it, and (iv) size the
carry-cost of leaving them until then, so the "leave"
is explicit and the CFO / board have the math.

The **founder-scope** version of this — anything the
pre-Series-A CTO *can* legitimately StranglerFig
themselves — is a single subsystem, a single service, a
single well-bounded module, running on a team of 5-25
engineers, with a single production region. Everything
inside that box is what this chapter covers; everything
outside it defers up.

## Failure modes

- **The rewrite that skipped the Chesterton's Fence
  check.** The team gutted the old code, shipped the
  new, and re-introduced the bug the old code was
  there to prevent. Fix: retroactive ADRs before any
  rewrite; treat archaeology as the first three
  weeks.
- **The big-bang rewrite.** A rewrite done as a
  single quarter-long branch that "will flip over at
  the end." The estimate is famously bad; feature
  work is frozen in the affected area; when the
  cutover slips, the team is stuck on two systems.
  Fix: strangler-figs and reversible steps; the
  cutover is the *removal* of the old system after
  the last traffic has moved, not a flip.
- **The rewrite that was actually a deprecate.** The
  team spent two quarters rewriting a feature nobody
  was going to use. The debt paid down had zero
  business value. Fix: deprecate is question 1 in
  the decision tree; do not skip it.
- **The "leave" that never gets revisited.** An item
  marked "Leave / revisit Q2" is still on the
  inventory in Q7 with no updates. Fix: chapter 06's
  decision log carries the revisit-date column; add
  the review to the quarterly board pre-read.
- **The engineering-aesthetic rewrite.** A rewrite
  motivated by a CTO's or a senior engineer's
  aesthetic reaction to the code, with no cost-to-
  carry backing it and no business owner. Fix: the
  decision tree requires a business owner (question
  1) and a compounding cost-to-carry (question 3).
  If neither is present, the rewrite has failed the
  tree.

## Summary

- Three responses per debt item: **Deprecate**,
  **Rewrite**, **Leave**. Not two; not one.
- **Deprecate** is the cheapest and most-underused
  response. If the feature has no business owner,
  the debt principal is zero — delete the feature.
- **Rewrite** requires the **Chesterton's Fence** check
  (Chesterton, *The Thing* — 1929
  [gutenberg.ca — *The Thing*](https://gutenberg.ca/ebooks/chestertongk-thething/chestertongk-thething-00-h.html))
  *before* starting, so that the new code honours
  the constraints the old code encoded. Then it uses
  the **StranglerFig** pattern (Fowler —
  [martinfowler.com/bliki/StranglerFigApplication.html](https://martinfowler.com/bliki/StranglerFigApplication.html))
  for incremental, reversible migration — never a
  big-bang cutover.
- **Leave** is a deliberate decision to pay the
  carry cost (chapter 03) in exchange for freed
  refactor budget. It requires explicit carry-cost
  disclosure and a revisit date; it is time-boxed,
  not permanent.
- The **decision tree** walks five questions:
  business owner? family? cost-to-carry compounds
  fast enough? Chesterton's Fence passes?
  StranglerFig-compatible? Only "yes" on all five
  authorises a rewrite.
- **Multi-quarter, multi-team, or multi-region
  extractions defer up** to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) and
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55). The pre-Series-A CTO's job is to
  recognise them and not attempt them alone.
- Failure modes: skipped Chesterton's Fence, big-
  bang cutover, rewrite that should have been a
  deprecate, unrevisited "leave", engineering-
  aesthetic rewrite.

The chapter's paired exercise —
[`exercise-04-deprecate-vs-rewrite-vs-leave-decision-drill.md`](exercises/exercise-04-deprecate-vs-rewrite-vs-leave-decision-drill.md)
— walks the decision tree over the top-5 items in your
portfolio and writes the defence for each choice.
Chapter 06 formats the whole thing as the inventory +
decision log an incoming VP Eng can read on day one.
