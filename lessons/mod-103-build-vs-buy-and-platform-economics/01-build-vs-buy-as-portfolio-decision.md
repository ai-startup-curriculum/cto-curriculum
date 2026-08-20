# Build vs. Buy as a Portfolio Decision

> "Do only what only you can do." — the maxim most often
> attributed, in this shape, to Jeff Bezos when explaining why
> Amazon buys rather than builds anything that is not its
> differentiator. The shape of the argument is the argument:
> build-vs-buy is a *portfolio* call about where finite team
> attention is deployed, not an aesthetic call about code
> ownership.

## Motivation

Every capability the startup depends on — auth, payments, the
data warehouse, the observability stack, the feature-flag
service, the foundation-model API — was either built by the
team or bought from a vendor. Each of those choices consumed
either team-time (the scarcest resource at pre-seed / seed) or
cash (also scarce, and paid on a schedule the vendor sets, not
one the team sets). The build-vs-buy decision is where those
two scarce budgets meet.

Two failure modes are common, and they are aesthetic mirror
images of each other.

- **Not-Invented-Here (NIH) as a virtue.** The team builds an
  in-house auth service, an in-house queue, an in-house
  observability pipeline, an in-house feature-flag system, on
  the theory that "we understand our needs better than any
  vendor does". Six quarters in, the team is running an
  infrastructure business as a side effect of running a
  product business, and every one of those in-house systems is
  a load-bearing dependency with a bus factor of one.
- **Vendor-everything as a virtue.** The team wires the
  product together from twenty SaaS vendors, each solving a
  slice of the stack. The monthly invoice climbs faster than
  revenue, the switching cost of any one vendor grows every
  month, and the "differentiator" — the thing the team could
  actually have built a moat around — is now a thin layer of
  glue between other people's APIs.

Both failure modes have the same root cause: **the
build-vs-buy call was made one component at a time, on
aesthetic grounds, without reference to the portfolio the
company was assembling**. This chapter names the portfolio
frame and the three axes — leverage, moat, team-time — that a
seed-stage CTO uses to make each call defensibly.

## The portfolio frame

Think of every capability the product depends on as an entry
in a portfolio. The portfolio has a fixed budget — engineer-
time this quarter, cash this month, and the total number of
load-bearing dependencies the team can meaningfully own — and
each entry is either **built by the team** (attention +
runway spent to gain moat and control) or **bought from a
vendor** (cash spent to buy leverage and delegate operational
risk).

The right question is not "should we build X?" in isolation.
It is "**of all the capabilities we depend on, which handful
do we build because they are the moat, and which do we buy
so that we can spend the team on the moat?**". That framing
is a portfolio call — the same shape the CFO makes when
allocating operating expense across a budget, and the shape
an investor recognises when reading the pitch deck.

Three axes govern each entry in the portfolio.

### Axis 1 — leverage

*How much throughput does buying this give the team, per
dollar and per week of avoided build?*

- A payments processor buys the team the throughput of
  never having to implement PCI-scope card handling, chargeback
  flows, or acquirer integrations — capabilities that would
  take multiple engineer-quarters to build minimally and
  multiple engineer-years to make robust. The leverage per
  dollar of vendor fee is extremely high.
- An in-repo, one-file build of a Slack webhook notifier
  is the opposite: buying a SaaS notifier service would cost
  more per month than the ten-line build ever will, and gives
  no leverage that the ten-line build does not already give.
- Between the extremes is where the interesting judgement
  lives — the observability stack, the queue, the
  feature-flag system, the auth vendor — and where the other
  two axes decide the call.

### Axis 2 — moat

*Is this capability part of what makes us defensible against
a competitor, or is it commodity infrastructure?*

- If the answer is *this is commodity* (identity, payments,
  transactional email, error reporting, log aggregation, cloud
  compute), the default is **buy** — nothing about the
  in-house version will ever be a moat, and the team-time
  spent building it is team-time not spent on the moat.
- If the answer is *this is the moat* (the domain model, the
  ranking algorithm, the proprietary dataset, the workflow
  the customer pays you for, the specific ML pipeline that is
  the product), the default is **build** — buying it means
  buying commodity where you needed proprietary, and the
  vendor's roadmap is not aligned to your competitive edge.
- **The default flips when the moat and the commodity are
  the same code.** If the vendor's product *is* your ranking
  algorithm, then buying it means the moat is the vendor's,
  not yours; you must build. Conversely, if what looks like
  "our special auth flow" is actually 95% the same OAuth
  dance as everyone else's, the moat is not there and you
  should buy.

The Bezos maxim — *do only what only you can do* — is the
short form of the moat test.

### Axis 3 — team-time economics

*What does building this cost in engineer-quarters this year,
in on-call weight, and in the opportunity cost of the
roadmap items we push?*

Team-time at pre-seed / seed is the scarcest resource in the
company. The classic hidden cost of *build* is not the initial
build — it is the years of maintenance, on-call, security
patches, and *upgrade the dependency because the CVE cannot
be ignored* work that never appears on the roadmap but
consumes the team every quarter after ship. Fred Brooks's
*Mythical Man-Month*
([wikipedia.org/wiki/The_Mythical_Man-Month](https://en.wikipedia.org/wiki/The_Mythical_Man-Month))
is the classic on why a build's ongoing cost tends to exceed
the naive up-front estimate by a large multiple.

The classic hidden cost of *buy* is not the invoice — it is
the drift the vendor introduces over years (pricing changes,
capability sunsets, terms-of-service updates, acquisition of
the vendor by someone the team never wanted to do business
with, the vendor pivoting away from your segment). See
chapter 06 on the vendor-selection scorecard for how to
account for that risk explicitly.

The seed-stage default, when the moat axis does not resolve
the call, is: **buy in order to conserve team-time; revisit
the call at the next stage transition** (per
[`mod-101`](../mod-101-cto-role-and-ownership-map/) — the
stage-by-stage plan). Every capability you build at seed is a
capability the team will be maintaining at Series A, at
Series B, and at scale. Choose the two or three you can
afford to maintain forever; buy the rest.

## The build-vs-buy matrix an investor can read

The output of this chapter's discipline is a single
**build-vs-buy matrix** — a one-page portfolio view that a
technical advisor, a lead investor, or a technical
due-diligence reviewer can read in five minutes. The matrix
lists each load-bearing capability the product depends on,
the current disposition (build / buy / hybrid), and the axis
that dominates the call.

A workable shape (used in this module's exercise 01):

```
| Capability            | Disposition | Vendor / Build | Moat? | Leverage of buying | Reopening trigger |
|-----------------------|-------------|----------------|-------|--------------------|-------------------|
| Identity / SSO        | Buy         | WorkOS         | No    | High (SAML/SCIM plumbing avoided) | Signed enterprise customer with in-house IdP the vendor does not federate |
| Payments              | Buy         | Stripe         | No    | Very high (PCI, tax, chargebacks) | Multi-currency + non-card rails become material to revenue |
| Foundation-model API  | Buy → Hybrid | OpenAI + Anthropic | Partial | High (inference infra avoided) | Per-token cost > 30% of gross margin, or unit economics require self-host |
| Domain ML pipeline    | Build       | in-house       | Yes   | N/A (this is the moat) | Never — buying breaks the moat |
| Feature flags         | Buy         | LaunchDarkly   | No    | Medium (SDK breadth) | Cost per MAU crosses in-house maintenance cost |
| Observability         | Buy         | Datadog        | No    | High (single-pane-of-glass) | Vendor bill trajectory forces re-plan (chapter 03) |
| Data warehouse        | Buy         | BigQuery       | No    | High (serverless, no ops) | Egress / query cost trajectory forces re-plan (chapter 02) |
```

Two things about the shape:

- **Every row has a *reopening trigger* column.** A
  disposition without a reopening trigger is a decision the
  team will forget it made. The trigger is what turns the
  matrix from a snapshot into a decision instrument the team
  actually re-reads at stage transitions.
- **The "Moat?" column is the tie-breaker, not the sort
  key.** Investors are looking for exactly two things from
  this matrix: (a) that the team has thought about where the
  moat is, and (b) that the team has not spent runway
  building things that are not the moat. Both are visible on
  the matrix.

Exercise 01 walks the authoring of this matrix for five real
choices at your (or a real reference) startup.

## Concrete example: the "we built our own auth" story

A common shape of the NIH failure mode is the in-house auth
service. The story typically runs:

- **Quarter 0.** Team decides to build a minimal
  email-and-password login "so we don't take on a vendor
  dependency". Two engineer-weeks. Ships.
- **Quarter 1.** Add password reset, session management,
  rate-limiting. Two more engineer-weeks. Ships. Nobody
  writes the ADR (see
  [`mod-102`](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md)).
- **Quarter 3.** First design partner asks for "sign in
  with Google". Two engineer-weeks to add OAuth. Ships.
- **Quarter 4.** First enterprise prospect asks for SAML SSO
  and SCIM provisioning. This is now an engineer-quarter of
  work — SAML and SCIM are not weekend projects — and the
  in-house code was not architected for it. The engineer who
  understands the auth code is on-call for it, blocked from
  other roadmap work, and increasingly the bottleneck.
- **Quarter 5.** A CVE is disclosed in a session-handling
  library the in-house code depends on. Everything else
  stops until it is patched.
- **Quarter 6.** The team ports off the in-house auth service
  to WorkOS or Auth0 as an emergency de-risk before the next
  enterprise deal, having spent the equivalent of two
  engineer-quarters over the year on identity — engineer-time
  the team did not have and did not spend on the moat.

The correct call at quarter 0, run through the portfolio
frame, would have been:

- **Leverage of buying:** very high (SAML, SCIM, MFA, session
  handling, CVE monitoring, audit logs — all delegated).
- **Moat:** identity is not the moat. If someone else's OAuth
  UI is 95% the same as ours, the moat is not there.
- **Team-time:** an in-house auth service is a maintenance
  commitment the team cannot afford to sustain against a
  moving compliance and threat landscape.

Portfolio verdict: **buy**. The reopening trigger — a
customer requirement the vendor genuinely cannot serve —
would then be the explicit condition under which the call is
revisited. Chapter 06 formalises that reopening-trigger
discipline in the vendor-selection scorecard.

## What the matrix is *not*

- **Not a static asset.** The matrix is versioned in the
  repo (same shape as the ADR index — see
  [`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md)),
  re-reviewed each quarter, and rows move as reopening
  triggers fire.
- **Not a beauty contest of vendors.** The matrix records
  the *disposition* (build / buy / hybrid) and the
  *reasoning*. The specific vendor choice within a "buy"
  row is chapter 06 material — the vendor-selection
  scorecard.
- **Not a substitute for the ADR.** Each meaningful row in
  the matrix should have a corresponding ADR that captures
  the *why* at the depth the ADR format is designed for.
  The matrix is the index; the ADRs are the depth.
- **Not a general-purpose enterprise architecture artifact.**
  It is a one-page portfolio view for a pre-seed / seed
  startup — legible to a founder, a first engineering hire,
  and an investor. If it grows past one page, it has
  drifted; edit it back.

## Common failure modes

- **The "hybrid because we couldn't decide" row.** A row
  marked `Build + Buy` because the team ships against both
  the vendor and an in-house prototype in parallel — with no
  agreed condition under which one wins. Fix: convert to a
  spike with a kill criterion (per
  [`mod-102` chapter 06](../mod-102-architecture-under-uncertainty/06-spikes-and-kill-criteria.md))
  or pick a disposition.
- **The moat-inflation row.** Every row is claimed to be
  part of the moat, because owning the code feels safer.
  Fix: pressure-test each moat claim against "would a
  competitor with the same vendor stack be materially
  behind?". If not, it is not the moat.
- **The vendor-lock-invisibility row.** The matrix records
  vendor choices but never surfaces the switching cost.
  Fix: add a switching-cost column (chapter 06), or link
  each buy row to the ADR that names the vendor-lock
  trade-off explicitly.
- **The stale-matrix.** The matrix ages, no one re-reads it,
  and at the next stage transition (Series A, hiring wave,
  new segment) the team is re-litigating from scratch. Fix:
  put the matrix re-review on the quarterly rhythm alongside
  the ADR-index review.

## Summary

- Build-vs-buy is a **portfolio decision** — a call about
  where finite team-time and cash are deployed across all
  the capabilities the product depends on — not an
  aesthetic call about code ownership.
- Three axes govern each entry: **leverage** (throughput per
  dollar), **moat** (defensibility), **team-time economics**
  (the multi-year cost of ownership, not the up-front
  build).
- The seed-stage default when the moat axis does not
  resolve the call is **buy**, in order to conserve team-
  time; the disposition is revisited at the next stage
  transition or when the reopening trigger fires.
- The output is a one-page **build-vs-buy matrix** an
  investor can read, with columns for capability,
  disposition, moat, leverage-of-buying, and reopening
  trigger.
- Each meaningful row is anchored to an ADR
  (see [`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md))
  so the reasoning is durable, and the whole matrix is
  re-read at stage transitions rather than left to age.

The chapter's paired exercise —
[`exercise-01-build-vs-buy-matrix-for-five-real-choices.md`](exercises/exercise-01-build-vs-buy-matrix-for-five-real-choices.md)
— walks the authoring of the matrix for five real choices at
your (or a real reference) startup. The subsequent chapters
in this module — cloud-provider economics (02), managed
vs. self-hosted across the classic categories (03), the AI-
native stack decisions (04), Radar / CNCF Landscape reading
(05), and the vendor-selection scorecard (06) — are the
per-cell depth that the matrix indexes.
