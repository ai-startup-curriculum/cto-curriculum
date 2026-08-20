# The CTO↔CEO Decision Cadence — Weekly 1:1, Decision-Rights Map, Tie-Breaker, Escalation

> "The single most-common cause of a founder blow-up
> in the first three years is not a bad decision —
> it's a decision one founder thought was theirs and
> the other thought was shared." — the framing this
> chapter is organised around.

## Motivation

Every co-founding pair operates on an *implicit* decision-
rights map for the first six to twelve months. It works
because there are ten decisions a day and both founders
are in the same room for eight of them. It stops working
between roughly the third hire and the seed close, when
the pace outstrips the "we're in the same room" backstop:
the CEO signs a term sheet the CTO first hears about on
the call; the CTO makes a hiring commitment the CEO first
hears about at the offer; a customer contract commits to a
data-residency posture engineering cannot deliver by the
promised date. None of these are bad decisions in
isolation. All of them are *unsynchronised* decisions —
and unsynchronised decisions compound into a founder-
trust deficit that a mediation session cannot recover
faster than an explicit decision-rights map installed at
month two would have prevented.

This chapter is about installing that map, and the weekly
cadence and escalation path that keep it honest, *before*
the pace forces you to do it under duress.

## The weekly CTO↔CEO 1:1 — a stable agenda beats a "let's catch up"

The weekly 1:1 is the single most-load-bearing meeting on
the CTO's calendar and the single most-often-degraded one:
degraded from an hour to thirty minutes, degraded from
in-person to a phone call between other meetings,
degraded from a stable agenda to a "let's catch up".
Each degradation feels reasonable in the moment; the
compound effect is that the two founders stop synchronising
on decisions until the disagreement is already public.

The 1:1 is not a status meeting — status lives in the
weekly written update (see chapter 03 on board pre-reads,
where the same discipline scales up). The 1:1 is the
place where **shared decisions are surfaced, tie-broken,
and logged**. A durable agenda for a 60-minute weekly
slot:

- **15 min — Decisions since last week.** Each founder
  briefs the decisions they made unilaterally in their
  own column of the decision-rights map since the last
  1:1. This is not review-and-approve; the point is
  *awareness*. If the CEO signed a customer contract
  with a technical commitment, the CTO learns about it
  here, not at customer implementation.
- **20 min — Decisions this week.** Each founder walks
  the *shared-decision* items on the agenda. These are
  the items that live in the "consensus" or "with
  input" columns and need a joint decision or a joint
  brief before the next 1:1.
- **10 min — Risks and blockers.** Existential
  vulnerabilities, key-person risk, customer / investor
  escalations, cash runway triggers that would move
  the roadmap. This is the item that most often
  degrades into "we're fine" — the discipline is to
  name at least one risk each, even when honestly
  nothing is on fire, so the muscle stays warm.
- **10 min — Hiring / people.** Open roles, offer
  status, performance concerns, org changes. Every
  hire above IC2 is a joint decision even if only one
  founder ran the loop.
- **5 min — Log and next-1:1 pre-read.** Update the
  running decision log (the same format the board
  decision log uses, chapter 03); confirm the pre-read
  items for next week.

The load-bearing property is *stability*: same day, same
time, same agenda, weekly, protected. The moment one of
the two founders starts moving or skipping the slot, the
decision-synchronisation function starts drifting, and
every subsequent decision has to be renegotiated under
higher pressure than would have been needed to protect
the slot.

## The decision-rights map — four columns, every recurring decision named

The core artifact is a **four-column decision-rights map**
that names, for every recurring class of decision at your
current stage, which of the four rights columns it lives
in. The four columns:

- **CEO unilateral.** The CEO decides. The CTO is
  informed after, may disagree, but does not have veto.
  Examples at seed / Series-A: term-sheet acceptance;
  pricing decisions inside the CEO's authority; hiring
  above VP; positioning and messaging; investor
  relations; board-communication cadence.
- **CTO unilateral.** The CTO decides. The CEO is
  informed after, may disagree, but does not have veto.
  Examples at seed / Series-A: choice of programming
  language and framework; cloud provider selection
  within the approved budget envelope; hiring below
  IC2 within the approved headcount plan; on-call
  rotation design; engineering process (sprint length,
  standup format).
- **Consensus (both must agree).** Neither founder
  proceeds without the other. Examples: hiring at IC3
  and above; equity grants above the standard offer
  ladder; any customer contract with a technical
  commitment materially beyond the current roadmap;
  any capital expenditure above a stated threshold
  (typical range at seed: $10-25k, at Series-A:
  $50-100k); any change to the founding-agreement
  vesting, cofounder split, or IP-assignment posture;
  the annual technical strategy and roadmap; the
  hiring plan against runway.
- **Board (or lead director) escalation.** Neither
  founder can decide alone; either escalates. Examples:
  cofounder equity re-split; cofounder departure; CEO
  or CTO compensation change; fundraising round terms
  materially different from the last approved
  guidance; acquisition offers; any material breach
  or incident that would trigger a customer or
  regulator notification.

A worked example — a first-page snapshot at ~15 rows for
a Series-A stage startup, seven engineers, one product,
one enterprise design partner in-flight:

| Decision class | CEO unilateral | CTO unilateral | Consensus | Board escalation |
|---|---|---|---|---|
| Engineering hiring — IC1 / IC2 | | ✓ | | |
| Engineering hiring — IC3 / staff / EM | | | ✓ | |
| VP Eng / Head of Product hire | | | ✓ | ✓ (offer) |
| Cloud vendor & spend ≤ $50k / mo | | ✓ | | |
| Cloud vendor & spend > $50k / mo | | | ✓ | |
| Enterprise contract, standard SLA | ✓ | | | |
| Enterprise contract, custom SLA / DPA / BAA | | | ✓ | |
| Term-sheet acceptance | ✓ (with CTO informed 48 h prior) | | | ✓ (board approves) |
| Founding-team equity re-split | | | | ✓ |
| Cofounder / exec departure | | | | ✓ |
| Roadmap re-baseline (annual) | | | ✓ | ✓ (board sees) |
| Roadmap re-baseline (in-quarter) | | | ✓ | |
| Incident with customer / regulator notification | | | ✓ | ✓ (post-hoc) |
| Security-posture change (SOC 2 scope, ISO, HIPAA scope) | | | ✓ | |
| Engineering process (sprint, standup, on-call design) | | ✓ | | |

Two properties that make the map useful:

- **Every row is a live decision class**, not a
  hypothetical. If your startup does not do enterprise
  contracts, the enterprise-contract row is not on the
  map yet. Adding rows as the business acquires the
  decision class is part of the annual re-baseline.
- **The map is a *joint* artifact**, signed by both
  founders and reviewed at least quarterly. A
  unilateral edit by either founder is itself a
  consensus-column violation.

An illustrative structured version to check in with git:

```yaml
# docs/founder-comms/decision-rights-map.yaml
# Reviewed quarterly; unilateral edit by either founder is a
# consensus-column violation.
version: 2026-08-Q3
signed_by:
  ceo: <name>, <date>
  cto: <name>, <date>
rows:
  - decision: "Engineering hiring — IC3 and above"
    column: consensus
    notes: "Standard offer ladder; either founder can veto"
  - decision: "Enterprise contract with custom SLA / DPA / BAA"
    column: consensus
    notes: "Technical-commitment review required before signature"
  - decision: "Term-sheet acceptance"
    column: ceo_unilateral
    notes: "CTO briefed 48 h prior; board approves"
    escalation: board
  # ... additional rows
```

## The tie-breaker mechanism — explicit before it is needed

For every consensus-column row, the map must also name
**what happens when consensus cannot be reached in the
1:1**. This is the single most-under-installed piece of
the cofounder relationship and the one that most
predictably causes founder blow-ups.

Three tie-breaker mechanisms that actually work in
practice at seed / Series-A:

- **Domain veto.** For a subset of consensus-column
  decisions the map explicitly names one founder as
  the tie-break holder. Example: if the CEO and CTO
  disagree on the hiring bar for an IC3 engineer, the
  CTO's judgment wins; if they disagree on the pricing
  posture for a design-partner contract, the CEO's
  judgment wins. The domain-veto column is not a
  hierarchy — it is a pre-agreed *who has the final
  word inside their craft*.
- **Deferred with a deadline.** For decisions where
  domain veto does not clearly apply, the map names a
  timeout after which the decision defaults to a
  specified outcome. Typical formulation: *"if
  consensus is not reached within two 1:1 cycles, the
  status quo holds and the decision is escalated to a
  lead director or board observer"*.
- **Third-party tie-breaker.** For a small named list
  of highest-stakes decisions (usually: an IP-assignment
  or vesting change, a cofounder role-change, a
  material litigation posture, a fundraise-terms
  disagreement), the map names a specific board
  member, board observer, or trusted independent
  advisor as tie-breaker. The named person must have
  agreed to the role in advance and must have been
  introduced to both founders.

The rule the map must enforce: **there is no consensus-
column row without a named tie-breaker mechanism**. A
consensus-column row with an unspecified tie-break is
worse than no map at all — it looks like a decision
process, feels like a decision process, and produces the
worst version of *whoever leaves the meeting first
declaring victory wins*.

## The escalation path to the board (or a board observer)

The board is not a substitute for founder consensus, and
using it that way corrodes both the founder relationship
and the board's willingness to be useful. The board is
the correct destination for a specific and short list of
escalations:

- Any decision the decision-rights map explicitly names
  as board-escalation (row 4 in the four-column map).
- Any consensus-column decision that has failed both
  cycles of *deferred-with-deadline* tie-breaker
  without resolution.
- Any founder-relationship rupture where the tie-
  breaker mechanism itself is contested (i.e. one
  founder rejects the tie-break outcome). At that
  point the cofounder-dispute mechanic (chapter 02)
  and mediation route become primary.
- Any *material* technical risk that neither founder
  can bound without external input — a class of
  incident (Series-B-scale outage on the horizon), a
  compliance obligation that has become un-scoped
  (chapter 06), or an architectural bet whose cost has
  moved beyond the founders' risk appetite.

The mechanics that make board escalation actually work:

- **Named lead director or board observer.** Even a
  small seed-stage board should have one director or
  observer who has agreed to be the *first call* on a
  founder dispute. The name lives in the decision-
  rights map. Between board meetings, that person is
  reachable.
- **Written escalation memo.** Every board escalation
  is preceded by a one-page memo — the decision at
  issue, the two founders' positions, the tie-breaker
  path attempted, the decision requested. Escalating
  verbally in the next board meeting without a memo
  destroys the board's ability to help.
- **Post-escalation retro.** After every board
  escalation, the founders retro in the next 1:1 —
  what led to the escalation, whether the decision-
  rights map needs a row change, whether the tie-
  breaker mechanism itself needs revision. The
  discipline is *learn from the escalation, do not
  make it the new normal*.

## A worked scenario — a customer contract with an out-of-roadmap commitment

The pattern shows up in every seed → Series-A CTO's
first year and is the single most-diagnostic test of the
decision-rights map. The scenario:

- A design-partner customer asks for **SAML SSO with
  their identity provider** as a contract prerequisite.
- The CEO wants to close the deal this quarter (it's a
  named account in the fundraising narrative).
- Engineering has SAML on the roadmap for next quarter
  as part of the enterprise-ready posture but has not
  built it yet.
- The customer's target close date is three weeks out.

With no decision-rights map installed, the pattern is
predictable: the CEO commits to the timeline in the sales
call, the CTO hears about it at the redline stage, the
engineering team is force-marched through a two-week
sprint, quality is compromised, and either the customer
churns in the first three months or the engineering team
loses two engineers to burnout. The founder trust
deficit shows up two quarters later as an unrelated
argument about hiring bar.

With the map installed, the same scenario plays as:

- The *enterprise-contract-with-custom-SLA/DPA/BAA* row
  is in the consensus column. The CEO cannot commit to
  the timeline unilaterally. The commitment is deferred
  to the next 1:1.
- In the 1:1, the CTO produces a *cost-of-carry
  estimate*: two engineer-weeks pulled from the current
  roadmap, one week of design work, ~30% delivery-risk
  on the current sprint. The CEO produces the *cost-
  of-not-carrying* estimate: contract slips one
  quarter, ~$X ARR delayed, narrative impact on the
  next investor update.
- The founders reach a joint decision — either the
  timeline is agreed with an explicit roadmap
  concession (the deferred item is named and slotted),
  or the timeline is renegotiated with the customer
  (the CEO owns the customer conversation, the CTO
  owns the engineering answer to *"when instead?"*).
- The decision is logged in the running decision log.
  If a subsequent customer asks for the same
  commitment on the same timeline, the founders reach
  for the log rather than re-litigating.

The load-bearing property: the map does not choose the
answer for the founders. The map ensures the answer is
*a joint one* and lives in a decision log that turns
future occurrences into a look-up rather than a fresh
argument.

## Signals that the cadence has drifted

Three tell-tale signals that the 1:1 / decision-rights
map / escalation cadence has drifted and needs to be
re-installed:

- **The CTO learns about a customer commitment at
  implementation time**, or the CEO learns about a
  hiring decision at offer-signing time. Either
  direction is a symptom of the same failure: a
  decision that was on the map has moved to unilateral
  action without a re-column-ing.
- **A board meeting produces a decision the founders
  had not aligned on beforehand.** The board should
  never be watching the founders negotiate live; the
  1:1 is where alignment happens, the board sees the
  aligned recommendation. A board that sees a live
  founder disagreement in-meeting is a board that
  starts losing confidence in *both* founders, not just
  the losing one.
- **The 1:1 has become a status meeting.** Status is
  cheap — a written weekly update takes ten minutes to
  produce and thirty seconds to read. If the 1:1 is
  filling with status, the decision surface is being
  starved. Re-install the four-item agenda.

## Summary

- The **weekly CTO↔CEO 1:1** with a stable four-item
  agenda (decisions since last week / decisions this
  week / risks and blockers / hiring and people) is
  the single most-load-bearing decision-synchronisation
  meeting on the CTO's calendar.
- The **four-column decision-rights map** — CEO
  unilateral, CTO unilateral, consensus, board
  escalation — is the joint artifact that names, per
  live decision class, who has the final word. Every
  consensus-column row must name its tie-breaker
  mechanism.
- The **tie-breaker mechanism** is one of *domain veto*,
  *deferred-with-deadline*, or a *named third-party
  tie-breaker* — pre-agreed and named in the map. A
  consensus row with no named tie-break is worse than
  no map at all.
- The **escalation path to the board** — a named lead
  director or board observer, a one-page written
  escalation memo, and a post-escalation retro — is
  reserved for map-designated escalations, failed tie-
  breakers, and founder-relationship ruptures. Not for
  routine decisions the founders should have made.
- The **running decision log** — the same format the
  board decision log uses (chapter 03) — turns every
  resolved consensus decision into a look-up rather
  than a re-argument.

The exercise for this chapter —
`exercise-01-cto-ceo-decision-rights-map.md` — walks
the construction of the map for your own founder pair.
