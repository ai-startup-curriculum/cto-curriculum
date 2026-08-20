# Exercise 03 — Board Pre-Read Authoring

**Module:** `mod-108-cto-ceo-and-board-communication`
**Planned time:** ~3 hours
**Chapter this builds on:** [`03-board-pre-read.md`](../03-board-pre-read.md)

## Problem statement

Author a **real board pre-read** for the CTO
section of the next board meeting using the
six-section standing structure from chapter 03.
If you are authoring for a live company, use
this quarter's actual data; if you are working
from a reference startup, describe the startup
in a paragraph and generate plausible-but-
representative content for each section.

The pre-read is authored *as if it were being
sent to the board 48-72 hours before the
meeting*. Every commitment must be traceable to
a prior board meeting or fundraising narrative;
every risk must belong to one of the three
classes from chapter 06; every decision must be
sized to be decided in-meeting with the pre-read
and 15 minutes of discussion.

## Requirements

Author a document at
`docs/founder-comms/board-pre-read-<yyyy-mm>.md`
(or the equivalent convention in your working
repo). Paired structured artifacts — a decision-
log YAML and (optionally) a risk-register YAML —
are optional but recommended.

### Context header

Before Section 1, a short header:

- **Company** (real or reference).
- **Stage** and **team size**.
- **Meeting date** and **quarter**.
- **CEO fundraising narrative** in one sentence
  (the *"what is this company becoming"* claim
  the CEO is anchored on this quarter).
- **Prior board meeting date** and the commitments
  made at that meeting (a bulleted list). This
  is the anchor for Section 1.

### Section 1 — Roadmap progress against last-meeting commitments

- A table with columns: *Q[N] commitment*,
  *Status* (shipped / in progress / deferred /
  descoped), *Notes*, *Narrative tie*.
- At least six commitments from the prior board
  meeting.
- Every *deferred* or *descoped* row names the
  reason and the reworked delivery plan (if any).
- Every row has an explicit *narrative tie* —
  which piece of the CEO's fundraising narrative
  from the context header the commitment
  supports. Rows that support nothing are either
  misclassified (they belong lower in the
  pre-read) or the narrative anchor is stale.

### Section 2 — Technical risks and their trajectory

The three-class risk register from chapter 06:

- At least **one** existential technical
  vulnerability with the full field set
  (risk / impact / mitigation / trajectory /
  board ask).
- At least **two** key-person risks by role
  (not by name in the shared document), with
  the mitigation posture.
- At least **one** un-scoped compliance
  obligation with the scope-in plan and
  timeline.

For every entry, the trajectory (increasing /
stable / decreasing since last meeting) is
explicit, and the board ask is one of
*informational*, *advice-sought*, or
*decision-requested*.

The negative-space test: no engineering-org-
internal risk (sprint-level delivery,
individual-performance concerns, tooling
choices, DORA-metric fluctuations, minor
technical-debt items) appears in Section 2.
If a candidate risk does not fit one of the
three classes, it does not belong here.

### Section 3 — Hiring status against plan

- **Approved hiring plan** at last meeting —
  role, level, target start.
- **Actuals** — filled, offer-out, in-loop,
  paused.
- **Departures** — voluntary, regretted,
  performance, restructure — since the last
  meeting.
- **Deviations** from the approved plan and
  why.
- **Board asks** — specific roles the board can
  help source, in a format that lets a board
  member forward the ask to their network.

### Section 4 — Security and compliance posture

- **The one-paragraph posture articulation**
  from
  [`mod-107` chapter 01](../../mod-107-founder-scope-security-and-compliance/01-founder-scope-security-posture.md)
  updated for the current quarter.
- **Change since last meeting** — any new
  compliance obligation acquired (new
  jurisdiction, new data type, new customer
  contract with unsupported commitment),
  any material change in the attestation or
  audit timeline.
- **Incidents** — the summary of any incident
  since the last meeting that met the
  customer- or regulator-notification
  threshold, with the notification-clock
  evidence.
- **Board decisions requested** — any scope,
  timeline, or budget decision on the
  compliance posture that requires board
  ratification.

### Section 5 — Key technical decisions since last board

A short (3-7 item) log of material technical
decisions the founders and the engineering
leadership have made since the last meeting,
each in the ADR format from
[`mod-102` chapter 03](../../mod-102-architecture-under-uncertainty/README.md):

- Decision.
- Context.
- Alternatives considered.
- Choice.
- Reversibility (one-way door / two-way door).
- **Narrative tie** — which piece of the
  fundraising narrative the decision supports,
  or an explicit note that the decision
  *changes* the narrative.

Decisions that changed the narrative are
flagged; decisions that are neutral to it are
labelled as such.

### Section 6 — Decision log — what the board is being asked to decide

At least **three** numbered board decisions
requested at this meeting, each in the format
from chapter 03:

- Identifier (`D-<year>-Q<quarter>-<nn>`).
- Title.
- Context.
- Alternatives considered.
- Recommendation.
- Sponsor (CEO / CTO / both).

Every decision is sized to be resolved in-
meeting with 15 minutes of discussion. Every
sponsor is prepared to defend the
recommendation. No decision has been surprise-
delivered to any board member (the *no-
surprises rule* from chapter 03 — briefed to
the sponsoring director in a 1:1 the week
before).

If any of the decisions are *advice-sought*
rather than *decision-requested*, place them
in a separate subsection so the board's
decision list stays clean.

### Section 7 — Advice-sought items (optional)

For items the CTO wants operator advice on
but is not yet asking the board to decide:

- The item in one sentence.
- The context.
- The specific advice sought (a named framing:
  *"we are torn between A and B, our lean is
  A, want a sanity check"* vs. *"we do not have
  a lean yet, want operator input"*).

## Starter guidance

- **Author the pre-read for the *board's* job,
  not yours.** The board wants (a) progress
  against the plan, (b) decisions to ratify,
  (c) bounded risk, (d) advice-sought items.
  A pre-read that is 80% *what shipped* and
  20% everything else is misaligned to the
  board's actual job.
- **Reference the prior board meeting
  explicitly.** Section 1 fails if the
  commitments listed do not match the prior
  meeting's minutes. Read the last board
  minutes before writing.
- **Cite the fundraising narrative
  verbatim** in the context header. If you
  do not know the current phrasing of the
  narrative, brief the CEO before writing.
  A pre-read that ties to a stale narrative
  looks like the CTO is not aligned with the
  CEO — which the board will notice.
- **The risk section is the highest-signal
  section.** Under-report and the board loses
  trust when a risk crystallises; over-report
  and the material risks get lost in the
  noise. The three-class filter from chapter
  06 is the discipline. If a candidate risk
  does not fit, do not force it.
- **Identifiers are load-bearing.** Every
  board decision (Section 6), every risk
  register entry (Section 2), and every
  material technical decision (Section 5) has
  a stable identifier that will follow it
  across quarters. Use them.
- **The no-surprises rule** applies to Section
  6. If any decision in Section 6 is a
  surprise to any board member on the day
  of the meeting, the pre-read failed. Brief
  the sponsoring director 1:1 in the week
  before.
- **Distribute through the CEO.** In a live
  company, the pre-read is a subsection of
  the CEO's board packet. In the exercise,
  state that explicitly at the top so the
  reader understands the delivery mechanic.
- **Length target** — 4-8 pages when
  rendered. A 2-page pre-read is
  under-substantiated; a 15-page pre-read is
  a document the board will skim.

## Acceptance criteria

The drill output is complete when:

- The pre-read exists at
  `docs/founder-comms/board-pre-read-<yyyy-mm>.md`,
  4-8 pages rendered.
- The context header names company, stage,
  team size, meeting date, quarter, CEO
  fundraising narrative, and prior-meeting
  commitments.
- Section 1 has at least six commitments in a
  table with status, notes, and narrative-tie
  per row.
- Section 2 has at least one entry per risk
  class (existential vulnerability, key-person
  risk, un-scoped compliance obligation), each
  with the full field set.
- Section 3 states hiring actuals against
  plan, departures, deviations, and board
  asks.
- Section 4 states the updated posture
  articulation, change since last meeting,
  incidents, and any compliance decisions
  requested.
- Section 5 has 3-7 material technical
  decisions in ADR format with narrative-tie
  per decision.
- Section 6 has at least three numbered board
  decisions requested, each sized to be
  decided in-meeting.
- No engineering-org-internal noise appears in
  Section 2, and no *what shipped* status
  appears in Section 6.
- A technical reviewer who does not sit on
  your board can read the pre-read in 15
  minutes and articulate (a) the three
  decisions being asked, (b) the top three
  risks, and (c) how the technical roadmap
  ties to the fundraising narrative.

## What this feeds into

- **Exercise 06** — the board-ready technical
  narrative-authoring drill extends Section 2
  and Section 5 of this pre-read into a
  standalone risk-and-narrative artifact.
- **The board decision log** populated in
  Section 6 becomes the durable, versioned
  artifact chapter 03 describes.
- **The module lab** consolidates this pre-
  read with exercises 01, 02, 04, 05, 06 into
  the `docs/founder-comms/` sub-tree.
- **Capstone
  [`project-103`](../../../projects/project-103-scaling-plan-from-five-to-fifty-engineers)**
  presents its scaling plan through a variant
  of this pre-read structure.

The drill's discipline is *authoring for the
board's job*. If any section of the pre-read
serves the CTO's need to be *seen doing work*
rather than the board's need to be *informed and
asked*, that section is misaligned. Revise.
