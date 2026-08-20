# The Cofounder-Dispute Mechanic — Vesting, Tie-Breaker, Relationship Agreement, Mediation

> "The best time to draft the cofounder-dispute
> mechanic is when both cofounders still like each
> other. The second best time is now. There is no
> third best time." — the framing this chapter is
> organised around.

## Motivation

Cofounder disputes are the most-cited *avoidable* cause of
startup failure in the Y Combinator, First Round, and
Startup Genome post-mortems that publish honest data on
why early-stage companies die. The typical failure
pattern is not a *bad* dispute; it is a *late* dispute —
one that surfaces in year two or three, with no vesting
schedule that can absorb a founder departure, no
decision-rights map to route the disagreement, no
mediation route agreed in advance, and no legal
instrument that lets either party leave without breaking
the cap table.

The mechanics that prevent that failure are unglamorous,
mostly legal, and must be installed *before* the dispute.
This chapter names the four pieces of that mechanic and,
critically, names the boundary at which the CTO stops
being the author and hands the instrument to counsel.

## The four pieces of the dispute mechanic

The mechanic has four load-bearing pieces. Each on its
own is insufficient; the four together give the founders
a defensible way to disagree, to escalate, and — in the
worst case — to separate without destroying the company.

- **Founding-team equity split with vesting.** How the
  equity was divided and, more importantly, on what
  schedule it vests and what triggers accelerate or
  reverse the vesting.
- **A decision-tie-breaker mechanism.** The mechanism
  from chapter 01 formalised into the operating
  agreement: for consensus-column decisions where the
  founders cannot reach agreement, what happens.
- **A cofounder-relationship agreement.** The non-legal
  companion to the operating agreement — values,
  roles, decision rights, working style, exit — that
  the founders write together in the first six
  months.
- **A mediation route.** The named neutral third party
  the founders will use if the tie-breaker mechanism
  itself fails to resolve a dispute.

## Piece 1 — Founding-team equity with vesting

Founding-team equity is the single most-consequential
instrument the founders sign in the first year. Two
patterns produce most of the observed failures: no
vesting at all (either founder can leave day one with
their full grant), or a vesting schedule with no
acceleration and no reverse-vesting.

The founder-scope standard the CTO should understand
well enough to route to counsel — but *not* to draft
without counsel — is roughly:

- **Four-year vesting with a one-year cliff.** The
  founder earns 25% of their grant at the one-year
  mark and the remaining 75% ratably (monthly, most
  commonly) over the next 36 months. Founders who
  leave before the cliff earn 0%; founders who leave
  after the cliff earn the vested portion and forfeit
  the unvested balance.
- **Double-trigger acceleration on change of control.**
  If the company is acquired *and* the founder is
  terminated without cause (or resigns for good reason)
  within a specified window post-acquisition, the
  vesting accelerates in full or in part. Single-
  trigger acceleration (acceleration on acquisition
  alone) is possible but is generally disliked by
  acquirers and can complicate a deal.
- **Reverse-vesting on founder shares granted at
  incorporation.** Founder shares granted at
  incorporation (i.e. issued rather than granted from
  the option pool) can be structured with a repurchase
  right that mirrors a vesting schedule: if the
  founder leaves before the schedule completes, the
  company (or the remaining founders) can repurchase
  the unvested portion at a nominal price. Reverse-
  vesting on founder shares is what makes it possible
  for a departing founder not to walk away with a
  cap-table-breaking stake.
- **An 83(b) election filed within 30 days of the
  grant** (for founders receiving restricted shares
  subject to vesting in the US) — Internal Revenue
  Code §83(b), see the IRS instructions at
  [irs.gov — About Form 15620 (Section 83(b) Election)](https://www.irs.gov/forms-pubs/about-form-15620).
  The 83(b) election is a *time-limited* filing that
  the founder must make personally; missing the
  window is one of the most-common early-stage tax
  mistakes and is not recoverable.

Every one of these items is a legal instrument. The
CTO's role is to understand the *shape* of the standard
approach — to notice when the shape is missing from a
draft or a bad-actor proposal — and to route the actual
drafting to a startup-experienced attorney. Templated
starting points from
[Y Combinator's Startup Documents](https://www.ycombinator.com/documents)
(the SAFE, the founder-agreement templates) and from
[Cooley GO](https://www.cooleygo.com/documents/)
(cofounder equity split, vesting schedules, IP
assignment) exist to *anchor* the conversation with
counsel; they are not a substitute for it.

## Piece 2 — The decision-tie-breaker mechanism (as a legal instrument)

Chapter 01 introduced the tie-breaker as an operating
mechanism inside the weekly 1:1. In the dispute-mechanic
context, the same mechanism must be reflected in the
company's *legal* structure — most commonly in the
operating agreement (for an LLC) or in the shareholders'
agreement / bylaws (for a C-corp) — so that a *governance*
dispute has a defensible resolution path.

The concrete places the tie-breaker mechanism shows up
as a legal instrument:

- **The board composition.** A two-founder board with
  no independent director produces a 1-1 deadlock on
  any consensus-column disagreement. Adding a *neutral
  third seat* — an independent director, or a board
  observer with agreed influence — creates a mechanism
  by which a governance-level deadlock can be broken
  without the founders needing to agree on the
  breaker. The seed-stage norm is to add the neutral
  seat at or before the first priced round; deferring
  it past Series-A is an anti-pattern.
- **Voting agreements.** Preferred-stock voting
  agreements (signed as part of any priced round) will
  typically name protective provisions — a specified
  list of decisions that require investor consent as
  well as founder consent. These *do* provide a
  deadlock-breaking mechanism for a subset of
  decisions, but they route the decision to *investors*
  rather than a neutral third party; the CTO should
  understand which decisions the current voting
  agreement routes to investor consent because those
  are decisions the founders cannot resolve alone even
  if they agree.
- **Statutory deadlock provisions.** Most jurisdictions
  offer statutory remedies for a genuine corporate
  deadlock — Delaware §226 dissolution / receivership
  being the most-cited in US startup practice
  (see [Delaware General Corporation Law §226](https://delcode.delaware.gov/title8/c001/sc07/index.html)).
  These are *last-resort* remedies; a well-drafted
  operating agreement or shareholders' agreement
  provides earlier and less-destructive resolution
  paths.

Every one of these is a legal instrument, again drafted
and reviewed by counsel. The CTO's role is to be able to
read the operating agreement, notice whether it has a
named tie-breaker mechanism for governance deadlocks,
and — if not — to raise it with the CEO and with
counsel as an item to address before the next round.

## Piece 3 — The cofounder-relationship agreement

The cofounder-relationship agreement is the non-legal
companion to the legal instruments above. It is a
document the founders write *together*, in the first
three-to-six months, that names:

- **Roles.** Who does what today. This is the input to
  the ownership map in
  [`mod-101`](../mod-101-cto-role-and-ownership-map/README.md)
  and to the decision-rights map in chapter 01. The
  discipline is to name the roles *narrowly enough*
  that ambiguity is surfaced. "Both handle strategy"
  is a failure mode; "CEO owns fundraising and
  positioning, CTO owns hiring bar and architecture,
  both own the roadmap" is a starting point.
- **Values.** The three-to-five values the founders
  have agreed the company will hire, evaluate, and
  make decisions against. Values written under
  founder disagreement two years in are values that
  serve one founder over the other; values written in
  the honeymoon period are the ones both founders
  will honour when it costs them.
- **Working style.** How the founders will
  communicate; the cadence of the 1:1 (chapter 01);
  the norms for disagreement (in-1:1 is fine, in-
  front-of-team is not); the norms for delivering
  hard feedback to each other.
- **Decision rights.** A prose version of the four-
  column map from chapter 01. The founders should be
  able to point to the relationship agreement and
  say *"here's how we decide"* without having to
  reason from first principles each time.
- **Exit conditions.** The hardest section to write
  and the most-important. Under what conditions
  would either founder leave? Under what conditions
  would the founders replace one of themselves? What
  is the process — mediation first, then a specified
  time window, then a named separation posture. This
  section is *not* a legal exit process (that lives
  in the operating agreement and the vesting
  instruments) — it is the founders' agreement about
  when and how the legal process gets triggered.

The most-cited source on the *shape* of a cofounder-
relationship agreement is Jason Fried and David
Heinemeier Hansson's *It Doesn't Have To Be Crazy at
Work* and Reid Hoffman's *The Alliance*; the Founder
Institute publishes a
[founder-collaboration agreement template](https://fi.co/insight/founder-agreements)
that names the sections without imposing a specific
values statement. Either is a valid starting point.

The load-bearing property: the cofounder-relationship
agreement is not enforceable in court, and the point is
not enforcement. The point is that the founders have
written down, in the honeymoon period, the answers to
the questions a dispute would otherwise force them to
answer under duress with adversarial counsel in the
room.

## Piece 4 — The mediation route

If the tie-breaker mechanism inside the 1:1 fails, and
the escalation to the board or lead director fails, the
next step is mediation — and mediation only works if the
mediator has been *identified in advance*, ideally
introduced to both founders, and agreed as the person
either founder can invoke.

Three practical mediation routes at seed / Series-A:

- **A named independent director or board observer.**
  The person named in the decision-rights map as the
  first-call for founder disputes (chapter 01) is
  frequently the first mediation route. This is
  informal mediation and it works well for
  disagreements that are still operational rather than
  relational.
- **An outside CTO or founder-coach.** For
  disagreements that are relational rather than
  operational — where the cofounders have started to
  distrust each other's judgment rather than
  disagreeing on a specific decision — a founder-
  coach or an experienced-founder mentor is often the
  right mediator. The name should be identified in
  advance, ideally by both founders together.
- **A formal mediator retained through counsel.** For
  disputes that have reached the *"one of us may need
  to leave"* stage, a formal mediator retained through
  counsel is typically the correct route. This is
  expensive, adversarial-adjacent, and worth avoiding
  where possible — but it is the correct step when
  the informal routes have failed. Waiting until
  litigation is the failure mode.

The escalation ladder — informal advisor → board /
lead director → formal mediator → counsel-led
separation — should be *named in the cofounder-
relationship agreement*, with the specific people (or
process for finding them) identified for the first two
rungs.

## What a well-drafted cofounder agreement covers — the checklist

A cofounder agreement drafted by startup-experienced
counsel will typically cover, in some form, all of the
following. The CTO's job is not to draft them; it is to
be able to read the draft, notice missing items, and
route the gap to counsel.

- **Equity split** — the initial percentage split
  between founders and the rationale for the split.
- **Vesting schedule** — the four-year / one-year-
  cliff standard, or the deviation and rationale.
- **Acceleration provisions** — single-trigger or
  double-trigger, with the definition of *cause* and
  *good reason*.
- **Reverse-vesting on founder shares** — the
  repurchase right and the price mechanism.
- **IP assignment** — every founder assigns any and
  all IP they created before or during the company's
  formation that relates to the company's business to
  the company. This is a load-bearing item at every
  DD (chapter 04).
- **Confidentiality and non-solicit** — standard
  post-separation obligations.
- **Roles and titles** — the initial designation of
  CEO, CTO, and any other C-level role and the
  process to change it.
- **Decision rights** — the tie-breaker mechanism for
  governance decisions, referencing the operating
  agreement or the shareholders' agreement.
- **Non-compete** — post-separation, jurisdiction-
  dependent. California, for example, largely does
  not enforce post-employment non-competes
  ([California Business and Professions Code §16600](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=7.&chapter=1.&part=2.&lawCode=BPC&article=)),
  which is one of the reasons the cofounder-
  relationship agreement matters more in California
  than elsewhere.
- **Founder exit process** — voluntary exit,
  involuntary exit (with cause / without cause /
  disability / death), and the mechanics of each
  (share repurchase, transition period, ongoing
  vesting or forfeiture).
- **Mediation and dispute-resolution clause** —
  reference to the mediation route agreed in the
  cofounder-relationship agreement, and the fallback
  to arbitration or litigation.

Missing items are not a *disqualifier* — the CTO
should not refuse to sign because a clause is missing —
but every missing item is a question for counsel and,
depending on the answer, a request for the draft to be
extended.

## The strict boundary to counsel

The single most-abused sentence in cofounder-agreement
work is *"my CTO drafted this, we're good"*. The CTO
does not draft cofounder legal instruments. Counsel
does. The reverse is equally true: counsel does not
choose the values that go into the cofounder-
relationship agreement; the founders do.

The founder-scope discipline is that:

- **The CTO owns the specification of *what the
  instrument must do*.** Equity split, vesting shape,
  tie-breaker mechanism, exit process — the CTO
  articulates the intent.
- **Counsel owns the drafting of the instrument that
  achieves the intent, in the jurisdiction, under
  the tax code, and in a form that will survive a
  future dispute.**
- **The CTO owns the reading of the returned draft
  against the specification** — asking "does this
  clause achieve what I asked for?" and, where the
  answer is unclear, asking counsel to explain in
  writing.
- **The CTO does not draft or edit the legal
  instrument directly.** Every edit routed through
  counsel; every question that could produce a legal
  opinion goes to counsel with a written response.
- **Neither the CTO nor the CEO shares the
  attorney-client privileged draft with third
  parties** without counsel's approval — sharing
  destroys the privilege and can weaken the
  instrument in a future dispute.

A pragmatic sizing: a full cofounder-agreement package
drafted from scratch at Series-Seed pricing typically
costs $5-15k of legal fees and takes two-to-four weeks;
using templated starting points from Y Combinator or
Cooley GO with counsel review typically costs $2-5k
and takes one-to-two weeks. Both are cheap compared to
the cost of a mid-stage founder dispute without the
package installed.

## Signals that the mechanic needs a refresh

Three signals that the dispute mechanic installed in
the honeymoon period needs a re-visit:

- **A new founder-level role has been added** (a
  Chief Product Officer, a second technical
  co-founder, a President or COO). The decision-
  rights map from chapter 01 needs a re-column-ing
  and the operating agreement may need a voting
  update.
- **The company has raised a priced round**, adding
  investor protective provisions and (usually) a
  board seat. The operating agreement is being
  amended anyway; the dispute-mechanic pieces should
  be reviewed against the new instruments.
- **The founders have had a real disagreement they
  had to work through.** After every genuine dispute
  the founders have resolved (or the tie-breaker
  fired), the mechanic gets a retro in the next 1:1
  — is the decision-rights map still right, is the
  tie-breaker mechanism still calibrated, is the
  mediation route still valid?

## Summary

- The cofounder-dispute mechanic has **four pieces**:
  founding-team equity with vesting, a decision-tie-
  breaker mechanism (operationally in the 1:1,
  legally in the operating agreement), a cofounder-
  relationship agreement, and a named mediation
  route.
- **Vesting shape** — four-year / one-year-cliff,
  double-trigger acceleration, reverse-vesting on
  founder shares, and (US) a timely 83(b) election —
  is the founder-scope standard whose *shape* the
  CTO understands and whose *drafting* is routed to
  counsel.
- The **cofounder-relationship agreement** — roles,
  values, working style, decision rights, exit
  conditions — is the non-legal companion the
  founders write together in the honeymoon period.
  It is not enforceable in court; that is not the
  point.
- The **mediation route** must be named in advance,
  with the specific people identified for the first
  two rungs of the escalation ladder (informal
  advisor → board / lead director → formal mediator
  → counsel-led separation).
- The **strict boundary to counsel**: the CTO owns
  the specification of what each instrument must do
  and the reading of the draft against that
  specification; counsel owns the drafting itself.
  Direct CTO edits to legal instruments are an
  anti-pattern.

The exercise for this chapter —
`exercise-02-cofounder-dispute-mechanic-drill.md` —
walks the audit of the four pieces you have installed
today against the checklist in this chapter and
produces the gap list routed to counsel.
