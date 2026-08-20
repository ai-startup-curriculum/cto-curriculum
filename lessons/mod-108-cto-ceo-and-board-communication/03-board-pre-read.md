# Briefing the Board on Technical Progress — Pre-Read, Decision Log, Roadmap Ties

> "A board meeting is a *ratification* meeting, not a
> *discovery* meeting. If a board member is learning
> something material for the first time in the room,
> the pre-read failed." — the framing this chapter
> is organised around.

## Motivation

Every seed → Series-A CTO ends up in some version of the
same first board meeting: they present a beautifully
detailed engineering update, walk through the last
quarter's shipping velocity, and finish. Then a board
member asks *"and how does that tie to the fundraising
narrative Sarah [the CEO] walked through last week?"*, or
*"what technical risks are you worried about that we're
not going to see in this deck?"*, or *"what are you
asking us to decide?"*, and the CTO realises the update
answered the wrong questions.

The pre-read is the fix. A well-authored pre-read (a) is
sent 48-72 hours before the meeting, so the board *reads
it* rather than being read *to*, (b) is structured
against the questions the board actually cares about, and
(c) names — explicitly — what the board is being asked to
decide vs. what the board is being informed of vs. what
the CTO wants advice on but is not escalating.

This chapter is the standing pre-read structure the CTO
should be able to instantiate every quarter, and the
supporting decision log and narrative discipline that
make the structure work.

## What the board actually reads for

A pre-read is written for the board's job, not the CTO's.
The board — a mix of the CEO, the CTO, one or two
investor-appointed directors, and (past Series-A) usually
one independent director — has a specific and short list
of jobs at each meeting:

- **Confirm progress against the plan** the CEO briefed
  at the last meeting or in the last investor update.
- **Approve the small set of decisions** that are on
  the map as board-escalation (equity grants above the
  standard ladder, executive hires, material
  fundraising terms, capital commitments above the
  agreed threshold — see chapter 01 for the four-column
  decision-rights map).
- **Bound risk.** Understand the largest technical,
  organisational, and commercial risks the company is
  carrying, whether they are increasing or decreasing,
  and whether any of them are approaching a threshold
  that would change the plan.
- **Provide operator judgment** on hard calls the
  founders have surfaced but are not yet asking the
  board to decide.

A pre-read that supports those four jobs looks nothing
like a good engineering-team update. Engineering-team
updates are ~80% *what shipped*; board pre-reads are ~80%
*what the numbers mean, what changed since last time, and
what you're being asked to do*.

## The standing pre-read structure — six sections

A durable pre-read for the CTO section of the board
packet has six sections, in this order:

### Section 1 — Roadmap progress against the last-meeting commitments

The CTO named a small number of specific deliverables at
the last board meeting (or the last investor update). This
section states — for each — the status: shipped, in
progress, deferred, or descoped. Every deferred and
descoped item names *why*, and whether the underlying
capability has moved on the roadmap or been dropped.

The load-bearing property: this section is a *comparison*
to the last commitment, not a fresh restatement of the
current state. A pre-read that quietly changes the
commitments between meetings destroys the board's ability
to trust the update.

A worked example:

```markdown
### 1. Roadmap progress against Q2 board commitments

| Q2 commitment | Status | Notes |
|---|---|---|
| SAML SSO GA to enterprise | ✅ shipped | Shipped Jun 12; 3 customers migrated |
| SOC 2 Type I report | 🟡 in progress | Type I fieldwork complete; report expected Aug 30 |
| Multi-region read-replica | 🔴 deferred to Q4 | Deferred: Q3 capacity absorbed by SSO + SOC 2 fieldwork; deferral risk = one named EU prospect asked, agreed a Q4 delivery |
| Model-eval regression harness | ✅ shipped | Shipped Jul 3; running on every release |
```

### Section 2 — Technical risks and their trajectory

The three-class risk register from chapter 06:

- **Existential vulnerabilities.** A single unresolved
  risk that, if realised, would materially harm the
  company (a critical security exposure with a public
  CVE and no patched path, a load-bearing key-person
  dependency with no successor, an un-scoped
  compliance obligation that is on the wrong side of
  a statutory clock).
- **Key-person risk.** Any place in the org chart or
  the codebase where the loss of a single person
  would take the company more than 30 days to
  recover from. Named by role, not by name, in the
  board deck; the actual names live in the DD data
  room (chapter 04).
- **Un-scoped compliance obligations.** Any compliance
  obligation the company has *acquired* — through a
  customer contract, a new jurisdiction, a new data
  type, a new integration — that is not yet scoped
  into the compliance posture from
  [`mod-107`](../mod-107-founder-scope-security-and-compliance/README.md).

For every risk in the register, the section names: the
risk in one sentence, the trajectory (increasing /
stable / decreasing since last meeting), the current
mitigation, and — if applicable — the decision the
board is being asked to help with. Risks that live
*inside* the engineering org (dev velocity, code
quality, tooling choices) do not belong in the board
risk register unless they have crossed into one of the
three classes.

### Section 3 — Hiring status against the plan

The engineering hiring plan the board approved at the
last meeting, with actuals against the plan:

- Open roles, filled roles, and offers-out roles.
- Departures (voluntary and regretted) since the last
  meeting.
- Any deviation from the approved plan and why.
- Any role the board is being asked to help source
  (typically at VP Eng, staff engineer, and
  specialist-domain levels).

The board is a distribution channel for exec and staff-
level hires. Pre-reads that name specific roles the
board can help with typically produce candidate
introductions between meetings; pre-reads that do not
name specific asks do not.

### Section 4 — Security and compliance posture

The one-paragraph posture articulation from
[`mod-107` chapter 01](../mod-107-founder-scope-security-and-compliance/01-founder-scope-security-posture.md)
— what is in place, what is in flight, what is
deferred — updated for the current quarter. Any change
in scope (a new customer contract that triggered a
BAA, a new jurisdiction that added GDPR obligations, a
new data type that changed the HIPAA scope call) is
named here.

Two situations that always rise from this section to
the board decision log:

- **A material compliance obligation acquired since
  the last meeting** that changes the scope of the
  security posture or the timeline of an attestation
  the board is expecting.
- **A material incident** — one that met the customer-
  or regulator-notification threshold, or one that
  produced a formal customer or investor concern —
  since the last meeting.

### Section 5 — Key technical decisions since last board

A short (three to seven items) log of the *material*
technical decisions the founders and the engineering
leadership have made since the last meeting, in the
same format the ADR discipline from
[`mod-102`](../mod-102-architecture-under-uncertainty/README.md)
uses: the decision, the context, the alternatives
considered, the choice, and the reversibility (one-way
door / two-way door).

The point is not to *seek approval* on these — they
have been made — but to give the board the running
list of what the company is *becoming* underneath the
top-line metrics. A board that reads this list every
quarter can see architectural drift, platform-vendor
concentration, hiring-driven language choices, and
build-vs-buy patterns without asking.

### Section 6 — Decision log — what the board is being asked to decide

The single most-important section. A numbered list of
the specific things the board is being asked to decide
in-meeting, in this format:

```markdown
### 6. Board decisions requested

**D-2026-Q3-01 — Approve $180k capex for GPU commitment.**
Context: Q4 model-eval workload has outgrown on-demand;
committed capacity at $180k for six months brings unit
economics from $0.42/eval to $0.19/eval. Alternatives:
stay on-demand ($270k projected six-month spend at
current growth); wait a quarter (blocks Q4 model
release). Recommendation: approve. Sponsor: CTO.

**D-2026-Q3-02 — Approve VP Eng offer at $290k / 0.7% /
1-year sign-on cliff.** Context: 3 finalist loops, 2
offers extended, 1 accepted subject to board approval;
compensation is 15% above the Radford-band midpoint
for Series-A. Sponsor: CEO and CTO. Recommendation:
approve.

**D-2026-Q3-03 — Ratify SOC 2 scope selection (Security
+ Availability + Confidentiality; not Processing
Integrity, not Privacy).** Context: Type I fieldwork
complete on this scope; two customer prospects have
asked whether Privacy will be added. Recommendation:
ratify current scope; revisit Privacy addition in Q1
2027. Sponsor: CTO.
```

Every item numbered so it can be minuted. Every item
naming context, alternatives, recommendation, and
sponsor. Every item small enough to be decided in the
meeting with the pre-read and 15 minutes of discussion.

Items that are *not* board decisions — items the CTO
wants operator advice on, items that are informational
only, items that will become a board decision at the
*next* meeting — go into an *advice-sought* subsection
below the decision log, so the board's decision list
is clean.

## The decision-log discipline

The board decision log is a *durable* artifact — not a
one-meeting deck, not a per-meeting reset. Every
decision made at a board meeting gets a permanent entry:
identifier, date, decision, sponsor, minute reference.
Every decision the board is asked to make in a future
meeting gets a *pending* entry with the meeting it
will be tabled at. Every board pre-read starts by
naming the prior-meeting decision entries that have
been closed since (with the outcome), the ones still
open, and the ones being added.

The log lives in the board data room, versioned. Its
purpose is to make the board's own history a look-up
rather than a re-argument, exactly like the running
decision log inside the 1:1 (chapter 01) does for the
founders. When a new board member joins — a second
investor director at Series-B, an independent director
at Series-A — the decision log is the single most-
efficient way to bring them current on what the
board has already decided and why.

An illustrative structured version:

```yaml
# docs/founder-comms/board-decision-log.yaml
decisions:
  - id: D-2026-Q3-01
    date: 2026-08-12
    title: "Approve $180k GPU capex commitment"
    sponsor: cto
    context: "Q4 model-eval workload beyond on-demand economics"
    alternatives:
      - "Stay on-demand — $270k projected 6-mo spend"
      - "Defer Q4 model release"
    outcome: approved
    minute_ref: "Q3 board minutes, item 4.2"
  - id: D-2026-Q3-02
    date: 2026-08-12
    title: "Approve VP Eng offer"
    sponsor: [ceo, cto]
    outcome: approved
    minute_ref: "Q3 board minutes, item 4.3"
  - id: D-2026-Q3-03
    date: 2026-08-12
    title: "Ratify SOC 2 scope selection"
    sponsor: cto
    outcome: ratified
    minute_ref: "Q3 board minutes, item 4.4"
```

## The narrative tie to the CEO's fundraising story

The CTO section of the board packet lives *underneath*
a top-line story the CEO owns: the fundraising narrative,
the *"here's what this company is becoming"* story that
the CEO uses with investors and that the board is
expected to be able to repeat back to their partnerships
and to their networks. The CTO's pre-read is only as
useful as the tie between the technical progress it
reports and that narrative.

The tie is made concrete in two places:

- **The commitment table in Section 1** references
  which of the last-meeting commitments *ladder up to*
  which piece of the CEO's narrative. If the narrative
  is *"we are the enterprise-ready AI application for
  regulated healthcare"*, then SAML SSO, SOC 2 Type I,
  and the HIPAA BAA path are all narrative-supporting
  commitments and their status is a narrative-status
  update; the model-eval regression harness is
  narrative-adjacent (it is table stakes for AI-native
  companies, not the enterprise-ready story) and gets
  briefer treatment.
- **Section 5** — the material-decision log — flags
  which decisions *move* the narrative. A decision to
  build a bespoke inference stack rather than depend
  on a foundation-model provider changes the *"what
  are we"* answer at the next fundraise; a decision to
  standardise on a specific cloud region for EU data
  residency changes the *"who can we sell to"* answer.
  These belong in Section 5 with an explicit narrative-
  tie note.

The CTO does not author the fundraising narrative
(chapter 07 walks the boundary to
[`founder-ceo-curriculum`](https://github.com/ai-startup-curriculum/founder-ceo-curriculum)
on that). The CTO *serves* the narrative — by making
sure every technical commitment, risk, and decision
that shows up in the pre-read either supports the
narrative, is neutral to it, or explicitly acknowledges
that it changes it.

## Timing, distribution, and the "no surprises" rule

Three operational disciplines that make the pre-read
work:

- **48-72 hours before the meeting.** Any earlier and
  material changes force a revision; any later and
  the board does not read it. The industry norm is
  Friday-noon for a Tuesday-morning meeting or
  Monday-noon for a Thursday-morning meeting.
- **Sent through the CEO.** The CTO section is part of
  the CEO's board packet, not a separate CTO
  distribution. This preserves the CEO's role as the
  board's primary point of contact and prevents
  parallel narratives from developing between board
  meetings.
- **The no-surprises rule.** No item in the board
  pre-read should be new to any individual board
  member. Any decision the CTO expects the board to
  contest — a scope descope, a hiring miss, an
  incident, a compliance-obligation acquisition — has
  been briefed to the lead director in a 1:1 call the
  week before, and the CEO knows the brief happened.
  Board meetings are the ratification step; the
  1:1 calls and the pre-read are where the actual
  alignment happens.

The board members that keep saying yes to the CEO's
raises are the board members who feel *ahead* of the
information, not behind it. The pre-read discipline —
same structure every quarter, decision log with
identifiers, narrative-tie in every commitment, no
surprises — is how the CTO earns and keeps that
position.

## Signals that the pre-read is not working

Three signals that the pre-read discipline has drifted
and needs re-installing:

- **A board member is reading the deck during the
  meeting.** They didn't receive it, or they didn't
  read it because the format is not stable enough to
  scan. Sent 48-72h out; same six sections every
  quarter; commitments in a table; decisions
  numbered.
- **The decision log has surprises.** A decision
  appears in the log that the CTO or CEO does not
  remember briefing the sponsoring board member on.
  Every board-escalation item goes through a 1:1
  brief the week before.
- **The narrative-tie section has to be reconstructed
  every quarter.** The pre-read is not just being
  authored, the *narrative* is being re-authored
  each quarter. Push back to the CEO — the
  fundraising narrative should be stable across at
  least three quarters, otherwise the company is
  running a pivot rather than executing a plan.

## Summary

- The board pre-read is a **standing, stable
  structure**: (1) roadmap progress against last-
  meeting commitments; (2) technical risks and
  trajectory; (3) hiring status; (4) security and
  compliance posture; (5) key technical decisions
  since last board; (6) decision log — what the
  board is being asked to decide.
- The **decision log is a durable, numbered,
  versioned artifact** — every past board decision
  and every requested decision has an identifier, a
  sponsor, and a minute reference. The log is the
  board's own history as a look-up.
- The **narrative tie** — every commitment references
  which piece of the CEO's fundraising narrative it
  ladders up to; every material decision that
  *changes* the narrative flags the tie explicitly.
- The **operational disciplines**: 48-72 hours before
  the meeting; sent through the CEO; no surprises
  (every decision briefed to its sponsoring director
  in a 1:1 the week before).
- **Advice-sought items** go in a separate subsection
  from decisions-requested so the board's decision
  list stays clean.

The exercise for this chapter —
`exercise-03-board-pre-read-authoring.md` — walks the
authoring of a real (or reference-startup) pre-read
using the standing structure.
