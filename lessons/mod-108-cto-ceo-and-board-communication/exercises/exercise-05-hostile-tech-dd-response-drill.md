# Exercise 05 — Hostile Tech-DD Response Drill

**Module:** `mod-108-cto-ceo-and-board-communication`
**Planned time:** ~2 hours
**Chapter this builds on:** [`05-hostile-technical-dd-session.md`](../05-hostile-technical-dd-session.md),
supported by
[`04-technical-due-diligence-data-room.md`](../04-technical-due-diligence-data-room.md)
(the data room the drill attacks and the artifacts
the drill produces to close the gaps), and by
[`mod-105`](../../mod-105-technical-debt-as-business-decision/README.md)
(the technical-debt portfolio the architectural-risk
angle draws from),
[`mod-106` chapter 05](../../mod-106-scaling-org-and-stack/05-dora-four-keys-as-signal.md)
(the DORA metrics the architectural-risk angle
draws from), and
[`mod-107`](../../mod-107-founder-scope-security-and-compliance/README.md)
(the compliance package the hidden-compliance-debt
angle attacks).

## Problem statement

Run the **three-angle hostile-DD attack** — architectural
risk, key-person risk, hidden compliance debt — against
the DD data room scaffolded in exercise 04. For each of
the angles, play the buyer's technical DD lead: generate
the specific questions the DD lead would ask, identify
what the current data room does and does not answer, and
produce the **pre-empting evidence artifact** that
closes each identified gap.

The point of the drill is not to *become* the hostile
DD lead. The point is to install the *"don't argue,
produce the artifact"* reflex from chapter 05 by
running the attack against your own posture before a
real buyer runs it against you. Every gap the drill
surfaces is a gap the drill closes with an artifact
that lands in the DD data room — turning a discovered
finding into a bounded one.

## Requirements

Author a document at
`docs/founder-comms/hostile-dd-response-drill.md`
(or the equivalent convention in your working repo).
The drill produces both (a) a written response
memorandum and (b) commits or references the new
pre-empting artifacts into `docs/dd-data-room/`.

### Context header

- **Company** (real or reference).
- **Stage** — pre-seed / seed / Series-A / Series-B,
  the transaction context you are drilling against
  (fundraise DD, acquisition DD, or purely
  hypothetical).
- **Data-room baseline** — pointer to the state of
  `docs/dd-data-room/` at the start of the drill
  (a specific commit SHA or a dated snapshot).
- **Adversarial framing** — the specific hostile-DD
  archetype the drill assumes (price-driven
  strategic acquirer / competitive Series-B lead
  hunting for a discount / late-stage PE
  reviewer). Chapter 05's framing.

### Angle 1 — Architectural risk

Play the DD lead attacking this angle. Generate the
attack and the response.

- **Question set** — at least the six questions from
  chapter 05, adapted to your product surface. Add
  any product-specific attack a competent DD lead
  would run (foundation-model vendor concentration
  for AI-native products; single-cloud dependency
  for multi-region-committed products; language-
  runtime concentration for niche stacks).
- **Data-room baseline read** — for each question,
  state which artifact in `docs/dd-data-room/01-*`
  or `05-*` answers it today, what the answer is
  (in a sentence), and what a competent DD lead
  would still push on.
- **Gap set** — for each unanswered or partially-
  answered question, name the gap in one sentence.
- **Pre-empting artifact per gap** — either a
  pointer to a new artifact you commit to the data
  room as part of the drill (a unit-economics
  profile, a dependency-cost analysis, a bounded
  rewrite roadmap, a DORA metric snapshot, a
  pattern-analysis update on the incident register)
  or a written *"why not required at our stage"*
  rationale with a target date for the artifact if
  the stage moves.
- **Response script** — a paragraph per question
  written in the CTO's voice as it would land in
  a hostile DD session: *"here is the artifact,
  here is the number, here is the trajectory"*,
  not *"we haven't looked at it that way"*.

At least **four** of the questions must produce a
new-or-updated artifact commit to the DD data room.

### Angle 2 — Key-person risk

Same structure as Angle 1.

- **Question set** — at least the five questions
  from chapter 05, adapted.
- **Data-room baseline read** — what
  `docs/dd-data-room/04-*` currently says and where
  a DD lead would push.
- **Gap set** — the missing pieces of the key-
  person register, the bus-factor analysis, the
  retention posture, the departure history, and
  the founders' own vesting-and-retention posture.
- **Pre-empting artifact per gap** — the updated
  key-person register, the bus-factor analysis per
  top-5 component, the retention-and-refresh
  posture document, the departure-history log with
  cause classification, and the founder-vesting-
  posture note (the last routed via counsel where
  it touches personal detail).
- **Response script** — same discipline. *"The
  register names five key-person roles. For each
  the mitigation is [specific]. The founder-CTO's
  vesting sits at [X] and the posture on a
  post-close operating period is [Y]"* — a
  bounded answer, not a defensive one.

At least **three** of the questions must produce a
new-or-updated artifact.

### Angle 3 — Hidden compliance debt

Same structure.

- **Question set** — at least the six questions
  from chapter 05, adapted to your compliance
  posture from
  [`mod-107`](../../mod-107-founder-scope-security-and-compliance/README.md).
- **Data-room baseline read** — what
  `docs/dd-data-room/02-*` and `05-*` currently say.
  For AI-native products, include the foundation-
  model BAA / zero-retention posture question set.
- **Gap set** — un-scoped compliance obligations,
  missing DPAs / BAAs, un-refreshed sub-processor
  list, missing notification-clock evidence,
  incomplete Type II observation-window plan.
- **Pre-empting artifact per gap** — the
  compliance-obligation register, the updated
  sub-processor list with DPAs / BAAs per vendor,
  the RoPA update, the notification-clock evidence
  log, the SOC 2 observation-window plan.
- **Response script** — *"the compliance-obligation
  register names three acquired-but-not-fully-
  scoped items; each is sized at N months of work
  and slotted in the roadmap at [Q]"*, not *"we
  aren't aware of that gap"*.

At least **three** of the questions must produce a
new-or-updated artifact.

### Section 4 — Commercial-in-technical-clothing escalation drill

Chapter 05 walks the moment the hostile DD session
crosses from technical questions to commercial
proposals (retention pools carved from proceeds,
earn-outs tied to technical milestones, walk-away
triggers on DD findings). Author, for at least
**three** of the questions across Angles 1-3:

- The escalation trigger — what the DD lead's
  question or proposal would sound like when it
  has crossed the line.
- The CTO's in-session response — *"that sounds
  like a question for [CEO] and counsel; can we
  take it off the technical DD agenda and route
  it to the commercial discussion?"* — with the
  specific wording adapted to your CEO and
  counsel names.
- The out-of-session escalation — how the CTO
  briefs the CEO in the break, the board's DD-
  liaison director post-session, and the counsel
  of record.

### Section 5 — The post-session retro

Chapter 05's same-day retro discipline. Author the
retro template as it would run after a real
hostile DD session:

- **Answers-file updates** — the entries added to
  `docs/dd-data-room/06-answers-file/answers.md`
  for the questions the file did not fully cover.
- **Artifact-gap action items** — the artifacts
  identified as gaps that the drill did not close
  (targeted for the next data-room refresh cycle).
- **Escalations logged** — the commercial-in-
  technical-clothing escalations that ran to the
  CEO and counsel, with the entry that goes into
  the running decision log (chapter 03).
- **CEO brief** — the one-paragraph brief the CTO
  would send the CEO after the session: what was
  asked, what was answered, what was escalated,
  and the DD lead's apparent read on the answers.

### Section 6 — Reflex-installation notes

A short (150-250 words) note on the *four failure
modes* from chapter 05 (defensive posture, ad-hoc
estimation, discovered surprise, cross-answer
inconsistency), with a specific commitment for
each on how the CTO will avoid it in a real
session. This is a *self-authored discipline*
statement, not a rule imposed from outside.

## Starter guidance

- **Play the buyer honestly.** The drill is worth
  what the DD lead persona is worth. Read the
  chapter 05 attack questions and generate the
  most-pointed version of each — as if the buyer
  wants the discount. A soft attack produces a
  soft response and no artifact update.
- **Every gap is either closed or bounded.** A
  gap identified without a corresponding
  artifact commit or a specific *"why not
  required at our stage"* with a target date is
  a failed requirement. Chapter 05's reflex
  turns gaps into artifacts, not into apologies.
- **Read from the artifact, do not extemporise.**
  The written response script per question is a
  read-from-the-artifact answer, not an ad-hoc
  estimate. If the artifact does not yet contain
  the numbers the response script quotes, the
  gap is the artifact, not the response.
- **Use real numbers where available; label the
  reference-startup numbers explicitly.** For a
  real company, unit economics, DORA metrics,
  incident counts, and vendor counts must be
  real. For a reference-startup version, the
  numbers are labelled *"illustrative"* so the
  drill does not accidentally publish false
  data.
- **Commit the artifacts.** The drill's most-
  valuable output is the artifact commits into
  `docs/dd-data-room/`. A response memorandum
  with no committed artifacts closes no gaps.
- **The commercial-in-technical escalation is
  practiced in advance.** The single sentence
  the CTO uses to route the earn-out or the
  retention-pool question to the CEO and
  counsel is one that improves with rehearsal.
  Draft the wording; do not extemporise it in
  the real session.
- **The reflex is a habit, not a mindset.**
  Chapter 05's *"don't argue, produce the
  artifact"* is installed by running this
  drill quarterly, not by reading the chapter
  once. Schedule the next run.

## Acceptance criteria

The drill output is complete when:

- The response memorandum exists at
  `docs/founder-comms/hostile-dd-response-drill.md`.
- Angles 1-3 each carry the full question set,
  data-room baseline read, gap set, pre-empting
  artifact per gap, and response script per
  question.
- At least **ten** total new-or-updated artifact
  commits (four for Angle 1, three each for
  Angles 2 and 3) land in `docs/dd-data-room/`.
- Section 4 provides the escalation trigger and
  response wording for at least three commercial-
  in-technical-clothing scenarios.
- Section 5 provides the same-day retro template
  populated as if a real session had been run.
- Section 6 states the four-failure-mode
  discipline in the CTO's own voice.
- Every gap identified is either closed with a
  committed artifact or bounded with a
  *"why not required at our stage"* rationale
  and a target date.
- A technical reviewer who does not know your
  DD data room can read the response memorandum
  and (a) name the three angles a hostile DD
  lead would attack from, (b) name at least
  one pre-empting artifact for each angle, and
  (c) describe the commercial-in-technical
  escalation reflex.

## What this feeds into

- **The DD data room from exercise 04** is
  materially strengthened by the artifacts
  committed as part of this drill. The
  running-artifact discipline is that every
  hostile-DD drill triggers a refresh, not just
  the quarterly cadence.
- **The board pre-read from exercise 03** —
  Section 2 (risk register) and Section 5
  (material technical decisions) — draws from
  the pattern-analysis artifacts this drill
  produces on the incident register.
- **The module lab** consolidates this drill
  with exercises 01, 02, 03, 04, 06 into the
  `docs/founder-comms/` sub-tree.
- **The next real DD engagement** — Series-A
  round, Series-B round, acquisition offer —
  begins with a data room that has already
  survived a hostile attack once.

The drill's discipline is *pre-empting evidence
before adversarial pressure*. The CTO who has run
the three-angle attack against their own posture
walks into the real hostile DD session with the
artifacts already produced and the reflex
already installed. The CTO who has not has to
develop both under time pressure — with the
buyer's DD lead in the room and the price on the
line.
