# Exercise 06 — Board-Ready Technical Narrative Authoring

**Module:** `mod-108-cto-ceo-and-board-communication`
**Planned time:** ~2 hours
**Chapter this builds on:** [`06-board-ready-technical-risk-narrative.md`](../06-board-ready-technical-risk-narrative.md),
supported by
[`03-board-pre-read.md`](../03-board-pre-read.md)
(the pre-read structure this narrative slots into as
Section 2 and Section 5) and by
[`mod-107`](../../mod-107-founder-scope-security-and-compliance/README.md)
(the compliance posture the un-scoped-compliance-
obligation class draws from).

## Problem statement

Author the **risk-engineering slice** of a board-
ready technical narrative for your next board
meeting (or a reference-startup board meeting). The
artifact has three parts: (a) the three-class board
risk register applied to your current posture, (b)
the explicit *what belongs on the board slide vs.
what stays inside engineering* decision for each
candidate risk, and (c) the narrative arc that ties
each board-visible risk to the CEO's fundraising
story.

The point of the drill is to install chapter 06's
three-class filter and the narrative-arc discipline
*before* an omitted risk crystallises or an over-
included operational item drowns the material
signal. The under- and over-reporting failure modes
from chapter 06 are symmetric; the discipline the
drill installs is symmetric too.

## Requirements

Author a document at
`docs/founder-comms/board-risk-narrative-<yyyy-mm>.md`
(or the equivalent convention in your working repo).
A paired structured artifact at
`docs/founder-comms/board-risk-register.yaml` is
optional but recommended — the structured version
makes the register diff-able across quarters and
maps cleanly onto Section 2 of the board pre-read.

### Context header

- **Company** (real or reference) and **quarter**.
- **CEO fundraising narrative** in one sentence
  (verbatim, as it appears in the CEO's current
  investor deck or last board deck).
- **Prior-meeting risk-register state** — pointer
  to the last meeting's register with the closed /
  changed / carried-forward status per prior
  entry. If this is the first authoring, name
  that.
- **Reference to the current board pre-read**
  (from exercise 03) that this narrative
  populates.

### Section 1 — Engineering-org-internal risk register (source)

Before the filter runs, the engineering-org-
internal register the CTO maintains. This is *not*
the board deck; it is the working register from
which the board section is filtered.

- A table of the current in-flight engineering
  risks — sprint-level delivery risk, individual-
  performance concerns (referenced by role, not
  by name — the per-name detail lives elsewhere),
  tooling and process choices, DORA-metric
  fluctuations, technical-debt items from the
  portfolio in
  [`mod-105`](../../mod-105-technical-debt-as-business-decision/README.md).
- At least **10 rows** — the register from which
  the three-class filter selects.
- Each row: risk in one sentence, current
  ownership, trajectory since last review.

This section is what the CTO carries in the
operating review; naming it explicitly makes the
three-class filter that follows honest.

### Section 2 — Three-class filter application

For every row in the Section 1 register, state
whether it lifts to the board this quarter, and
why. Format:

- **Risk id / one-sentence description.**
- **Filter verdict** — one of *lifts (existential
  vulnerability)*, *lifts (key-person risk)*,
  *lifts (un-scoped compliance obligation)*, or
  *stays in engineering* (with a one-line
  rationale — most-often *"does not cross into
  any of the three classes at current threshold"*).
- **Cross-over trigger** — for the *stays in
  engineering* rows, the specific condition
  under which the risk *would* lift to the board.
  Naming the trigger keeps the filter honest —
  the risk lifts when the trigger fires, not
  when the CTO notices belatedly.

At least **two** rows must lift in each of the
three classes for this quarter's authoring, or an
explicit *"no candidate this quarter, register
maintained"* note per empty class. Zero rows
lifting in a class is a signal — either the
posture is genuinely clean (rare) or the
engineering-internal register is not surfacing
the right classes (more common).

### Section 3 — Board risk register (destination)

The register as it appears in Section 2 of the
board pre-read (chapter 03), populated from the
lifted rows in Section 2. Format per entry:

- **Identifier** (`R-<year>-Q<quarter>-<class>-<nn>`
  where `<class>` is `EX`, `KP`, or `CP` for the
  three classes).
- **Risk** in one sentence.
- **Realisation impact** — what happens if the
  risk fires; specifically, which of *anchor-
  customer loss*, *regulator threshold breach*,
  *distressed-valuation fundraise*, *product
  unshippable for more than a specified window*,
  or *board-approved-plan miss* is triggered.
- **Current mitigation** — bulleted, with the
  in-flight status per bullet.
- **Trajectory** — increasing / stable /
  decreasing since last meeting.
- **Board ask** — informational / advice-sought
  / decision-requested. If *decision-requested*,
  cross-reference the entry in Section 6 of the
  board pre-read.

At least **one** entry per class (existential,
key-person, un-scoped compliance). The key-person
entries name the *role*, not the individual — the
per-name detail lives in
`docs/dd-data-room/04-engineering-org-and-key-persons/`
from exercise 04.

### Section 4 — Narrative arc

For every entry in Section 3, name the specific
narrative pattern from chapter 06 that frames the
risk in the board deck:

- **The *"here is what we have already de-risked"*
  pattern** — for entries where a prior-meeting
  risk has closed, materially mitigated, or
  unchanged. Cite the prior-meeting entry and the
  current state.
- **The *"here is what the next round de-risks"*
  pattern** — for entries where the mitigation
  is hire-driven or capital-driven and the next
  round (or the next quarter's capital allocation)
  closes the risk. Name the specific investment
  and the specific risk retirement.
- **The *"here is what we are asking your help
  with"* pattern** — for entries where a board
  member's operator judgment or network is a
  mitigation. Name the specific ask (a candidate
  introduction, a compliance-advisor intro, a
  scope-decision request).

Every Section 3 entry must map to at least one
pattern. Entries that map to none are a signal —
either the risk is under-scoped (the mitigation
has not been thought through) or the risk is
misclassified (it belongs in the engineering-
internal register, not the board section).

### Section 5 — Narrative-tie to the fundraising story

For each entry in Section 3, one sentence tying
the risk to the CEO's fundraising narrative from
the context header:

- If the risk *supports* the narrative — the
  mitigation directly enables a narrative pillar
  (SOC 2 attestation for a regulated-buyer
  narrative; multi-region posture for an
  international narrative; foundation-model
  fallback for an AI-native narrative) — name
  the pillar.
- If the risk is *neutral* to the narrative —
  the risk lives underneath the narrative, and
  its mitigation is table-stakes rather than
  narrative-defining — label it *neutral*.
- If the risk *changes* the narrative — a
  vendor-concentration risk whose realisation
  would force a *"we are becoming X"* pivot; an
  un-scoped compliance obligation whose scoping
  would open a new customer segment — name the
  narrative implication.

The load-bearing property: no entry is *stranded*
from the narrative. A risk that connects to
nothing is either misclassified or under-scoped —
apply the filter again.

### Section 6 — Delivery script

A one-paragraph delivery script for the risk
section of the board meeting. What the CTO will
*say* while the board is looking at the pre-read
section — the framing sentence, the summary line
per class, the specific asks. The script is
*shorter than the register* — the register is the
board's read-ahead, the script is the CTO's
in-meeting delivery.

Chapter 06's warning: the board that gets the
same risk-section-delivery every quarter loses
the ability to distinguish material risks from
routine ones. The delivery script varies with the
register; it does not become a template.

### Section 7 — Signals-tracking commitments

Chapter 06 names three signals that the
narrative has drifted:

- The board sees a material risk for the first
  time on the day it crystallises.
- The board's response is *"tell us more"*
  three quarters in a row.
- The board's response is *"none of these seem
  material"*.

For each signal, a written commitment on the
counter-measure the CTO will run. If the signal
fires, this section is what tells you which
discipline needs re-installing.

## Starter guidance

- **Populate Section 1 first, filter second.**
  The three-class filter is worth what the
  Section 1 register is worth. A thin
  engineering-internal register produces a thin
  board register. Start with the full working
  register; let the filter do the work.
- **The three classes are load-bearing.** Chapter
  06 chose *existential*, *key-person*, and *un-
  scoped compliance* for a reason — those are
  the three risk types where the board's
  intervention is (a) legitimate and (b)
  operative. Do not invent a fourth class for
  operational items you want the board to
  notice.
- **Name the cross-over trigger for the
  *stays-in-engineering* rows.** Chapter 06's
  discipline: engineering-internal risks *cross
  over* to board risks when they enter one of
  the three classes. The trigger is what tells
  you when the crossover has fired — a
  key-person departure, a vendor-terms change,
  a new customer contract that acquires a
  compliance obligation.
- **Roles, not names.** Every key-person entry
  in Section 3 is by role. The board deck lives
  in a shared vehicle; per-name detail is
  privileged (chapter 04, folder 04 of the DD
  data room). Chapter 06 walks this discipline
  explicitly.
- **Read the CEO's current narrative before
  authoring.** Section 5's narrative-tie fails
  if the narrative in the context header is
  stale. If you do not know the current
  phrasing verbatim, brief the CEO before you
  write.
- **The delivery script is *short*.** A five-
  minute delivery for a five-entry register is
  correct. A twenty-minute delivery is a signal
  that the register is over-populated or the
  script has become a re-reading of the
  register. Speak to what the register says;
  do not narrate it.
- **Cross-reference exercise 03.** The board
  risk section produced here is a section of
  the pre-read authored in exercise 03. Link
  the two documents in both directions so the
  reader (and future-you) sees the composition.

## Acceptance criteria

The drill output is complete when:

- The narrative exists at
  `docs/founder-comms/board-risk-narrative-<yyyy-mm>.md`.
- Section 1 has at least 10 engineering-internal
  register rows.
- Section 2 applies the three-class filter to
  every Section 1 row, with a filter verdict and
  (for *stays-in-engineering* rows) a specific
  cross-over trigger.
- Section 3 has at least one entry per class
  (existential, key-person, un-scoped
  compliance), each with the full field set
  (identifier, risk, impact, mitigation,
  trajectory, board ask). Key-person entries
  are by role.
- Section 4 maps every Section 3 entry to at
  least one narrative pattern.
- Section 5 ties every Section 3 entry to the
  fundraising narrative — supporting, neutral,
  or changing.
- Section 6 has a delivery script for the risk
  section of the meeting.
- Section 7 states the counter-measure for each
  of the three drift signals.
- No engineering-org-internal noise (sprint-
  level delivery, individual-performance
  concerns below the founder level, tooling
  choices, DORA fluctuations, minor debt items)
  appears in Section 3.
- No entry in Section 3 is stranded from the
  narrative arc (Section 4) or the fundraising
  story (Section 5).
- A technical reviewer who does not sit on
  your board can read the narrative in 15
  minutes and articulate (a) the three-class
  filter, (b) the top risk per class, and (c)
  the narrative pattern that frames each.

## What this feeds into

- **Section 2 (risks) and Section 5 (material
  technical decisions) of the board pre-read
  from exercise 03** are populated directly
  from this narrative.
- **The board decision log from chapter 03**
  gets an entry for every *decision-requested*
  board-ask in Section 3.
- **The DD data room from exercise 04** —
  specifically the key-person register in
  folder 04 and the pattern analysis on the
  incident register in folder 05 — is the
  source for the key-person and (partial)
  existential-vulnerability sections here.
  Keep them in sync.
- **The module lab** consolidates this
  narrative with exercises 01-05 into the
  `docs/founder-comms/` sub-tree.
- **Capstone
  [`project-103`](../../../projects/project-103-scaling-plan-from-five-to-fifty-engineers)**
  uses the risk narrative as the risk-section
  vehicle for the scaling plan presented to
  the board.

The drill's discipline is *the three-class
filter, applied honestly*. The CTO who
under-reports damages board trust when a
material risk crystallises. The CTO who over-
reports drowns the material risks in
operational noise. The filter — applied every
quarter to a maintained engineering-internal
register — is what keeps both failure modes
from firing.
