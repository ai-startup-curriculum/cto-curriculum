# Exercise 01 — CTO↔CEO Decision-Rights Map

**Module:** `mod-108-cto-ceo-and-board-communication`
**Planned time:** ~2 hours
**Chapter this builds on:** [`01-cto-ceo-decision-cadence.md`](../01-cto-ceo-decision-cadence.md)

## Problem statement

Author the **four-column decision-rights map** for
your CTO / CEO pair — either your real cofounder
pair or a reference startup you can describe in a
paragraph (product, team size, primary customer
profile, funding stage, whether AI-native, whether
handling regulated data). Agree the tie-breaker
mechanism for every consensus-column row, and name
the escalation path to the board or a board
observer.

The point of the drill is not to invent hypothetical
decisions. The point is to force the map onto the
*live* decision surface your founder pair faces
this quarter, and to install the tie-breaker and
escalation mechanics *before* a real decision
demands them under time pressure.

## Requirements

Author a document at
`docs/founder-comms/decision-rights-map.md` (or the
equivalent convention in your working repo). A
paired YAML companion at
`docs/founder-comms/decision-rights-map.yaml` is
optional but recommended — the structured version
makes the map diff-able across quarterly reviews.

### Section 1 — Context (150-250 words)

- The founder pair — CEO and CTO — with roles and
  tenure at the company. If you are working from a
  reference startup, state that explicitly and
  give one paragraph of context.
- The stage of the company (pre-seed / seed /
  Series-A), team size, primary customer profile,
  whether AI-native, whether handling regulated
  data.
- The load-bearing customer or investor
  commitments already made that materially shape
  the decision surface this quarter (an
  enterprise-contract SLA, a data-residency
  posture, a fundraise timeline, an attestation
  deadline).

### Section 2 — The four-column map

A table with columns *Decision class*, *CEO
unilateral*, *CTO unilateral*, *Consensus*,
*Board escalation*. Populate with **at least 15
rows** drawn from the live decision surface of
your current stage. Chapter 01 gives a starter
list; extend or reshape it to your context.
Rows must cover, at minimum:

- **Hiring** — at least three rows spanning ICs,
  senior ICs / EMs, and executive hires.
- **Vendor and platform spend** — at least two
  rows spanning the current-stage threshold you
  and your cofounder have agreed for approval
  (typical seed: $10-25k; typical Series-A:
  $50-100k).
- **Customer contracting** — at least two rows
  spanning standard SLA and custom SLA / DPA /
  BAA / technical-commitment.
- **Roadmap and scope** — at least two rows
  spanning in-quarter re-scoping and annual
  re-baseline.
- **Fundraising and cap-table** — at least two
  rows spanning term-sheet review, equity
  grants above the standard offer ladder, and
  founding-team equity re-split.
- **Security and compliance** — at least two
  rows spanning scope choices (SOC 2, ISO,
  HIPAA) and material-incident notification.
- **Engineering process** — at least one row
  covering the day-to-day process choices
  (sprint length, on-call design, deployment
  process) that clearly sit in the CTO-
  unilateral column.

Each row lives in exactly one column. Rows that
feel like *"both a bit"* are consensus rows; the
consensus column is the correct home for the
ambiguous decisions.

### Section 3 — Tie-breaker mechanism per consensus row

For **every consensus-column row** in Section 2,
state which of the three tie-breaker mechanisms
from chapter 01 applies:

- **Domain veto** — one founder has the final
  word inside their craft. Name the founder.
- **Deferred-with-deadline** — state the timeout
  (e.g. two 1:1 cycles) and the default outcome
  if consensus is not reached.
- **Third-party tie-breaker** — name the specific
  advisor, director, or observer who has agreed
  to the role. This must be a *named* person,
  not *"a board member"* in the abstract.

A consensus row with no tie-breaker named is a
failed requirement. If you cannot name the
mechanism, that is a signal that you have not yet
agreed how the decision would be resolved — which
is the point of the drill.

### Section 4 — Escalation path to the board

- Name the **lead director or board observer**
  who has agreed to be the first call on a
  founder-level escalation. If your board does
  not yet exist or does not yet have a suitable
  named person, name the specific advisor or
  angel investor who fills that role at your
  current stage — and name the action item that
  moves the role to a director / observer once
  a board exists.
- State the **written-memo format** for a board
  escalation — either point at chapter 01's
  format or specify your own variant with the
  same fields (decision at issue, two positions,
  tie-breaker attempted, decision requested).
- State the **post-escalation retro discipline**
  — you and your cofounder will retro every
  board escalation in the next 1:1 and update
  the map if needed.

### Section 5 — The weekly 1:1 agenda

Reproduce (or adapt) the four-item weekly-1:1
agenda from chapter 01 with the specific time
allocations you and your cofounder have agreed
for a 30-, 45-, or 60-minute slot. Name the
day-of-week and the time. Name the location or
format (in-person / video / phone) with the
posture on degradation — under what conditions
the slot moves, and what the default is when
travel or unavailability forces it.

### Section 6 — The running decision log

Point at (or scaffold) the *running decision log*
that will capture the outcome of each consensus-
column decision as it is made. The log format
should match the board-decision-log format from
chapter 03 (identifier, date, decision, sponsor,
context, alternatives, outcome). At minimum, name
the file path where the log will live and the
weekly-1:1 agenda item that populates it.

## Starter guidance

- **Draft it alone; sign it together.** The map
  is meaningless if only one founder wrote it.
  Draft your version, share it with your
  cofounder before the next 1:1, and use that
  1:1 to align. Every disagreement you have in
  that 1:1 about the map is a *decision surface
  you did not have alignment on* — which is
  exactly the value the map surfaces.
- **Populate the map from the last four
  weeks of actual decisions, not from
  imagination.** Look at the last four weeks
  of Slack, email, and 1:1 notes. Every
  material decision you or your cofounder made
  in that window is a row candidate. Rows
  invented in the abstract usually turn out
  not to survive contact with a real decision.
- **Do not omit the awkward rows.** The
  founding-team equity re-split, the founder-
  departure process, and the fundraise-terms-
  deviation rows are the ones most-often
  omitted from first-draft maps because they
  feel improbable. They are the ones the map
  most-needs to name explicitly.
- **The tie-breaker must be *pre-agreed*.**
  A consensus row with a placeholder tie-
  breaker ("we'll figure it out") is worse
  than no map at all — it looks like the
  founders have agreed a mechanism when they
  have not. If you cannot converge on the
  mechanism in the drafting 1:1, park the row
  in the escalation column temporarily and
  come back to it.
- **Cite chapter 01 explicitly** in the
  document. This is the artifact you and your
  cofounder will return to when a decision
  gets contentious; making the reference to
  the chapter and the decision cadence
  discipline visible in the document itself
  keeps the mechanism honest.
- **Route the *legal* implications to
  counsel.** Rows about founding-team equity
  re-split, founder departure, cap-table
  changes, and material fundraise-terms
  deviations reference legal instruments
  (operating agreement, vesting schedule,
  voting agreement) — reference them but do
  not draft the instruments themselves. See
  chapter 02 for the strict boundary.

## Acceptance criteria

The drill output is complete when:

- The map exists at
  `docs/founder-comms/decision-rights-map.md`
  and (optionally) `.yaml`, and is signed and
  dated by both founders (or, for the
  reference-startup version, is signed by
  you with a note that a real map would be
  signed by both).
- Section 2 has **at least 15 rows** covering
  the seven required categories, with every
  row in exactly one column.
- Section 3 names a specific tie-breaker
  mechanism for **every** consensus-column
  row. No row is left with an unspecified
  mechanism.
- Section 4 names a specific person as the
  first-call for founder escalation, states
  the escalation-memo format, and states the
  post-escalation retro discipline.
- Section 5 names the day, time, format, and
  four-item agenda for the weekly 1:1.
- Section 6 points at (or scaffolds) the
  running decision log with a matched format
  to chapter 03's board-decision log.
- A technical reviewer who does not know your
  founder pair can read the map in ten
  minutes and identify (a) which of the two
  founders decides any given rowed
  decision, and (b) what happens if consensus
  cannot be reached on a consensus-column
  row.

## What this feeds into

- **Exercise 02** — the cofounder-dispute-
  mechanic drill audits the *legal*
  instruments (vesting, operating agreement,
  cofounder-relationship agreement, mediation
  route) that back the map produced here.
- **Exercise 03** — the board pre-read
  authoring uses the board-escalation column
  of this map to populate the decision-log
  section of the pre-read.
- **The module lab** consolidates this map
  with the outputs of exercises 02-06 into
  the `docs/founder-comms/` sub-tree.
- **Capstone
  [`project-103`](../../../projects/project-103-scaling-plan-from-five-to-fifty-engineers)**
  uses the map as an input to the scaling-
  plan governance section.

The drill's discipline is *installing the
mechanic before the disagreement*. The map is
useful in inverse proportion to the founder
tension in the room when it is drafted — draft
it now, review it quarterly, extend it as the
decision surface grows.
