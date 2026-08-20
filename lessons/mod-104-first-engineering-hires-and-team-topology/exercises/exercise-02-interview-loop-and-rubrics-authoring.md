# Exercise 02 — Interview Loop and Rubrics Authoring

**Module:** `mod-104-first-engineering-hires-and-team-topology`
**Planned time:** ~3.5 hours
**Chapter this builds on:** [`02-interview-loop-and-rubrics.md`](../02-interview-loop-and-rubrics.md)

## Problem statement

Pick **one open role** from your hiring plan (exercise
01) — ideally the *next* role you will actually run a
loop for — and author the **complete five-stage
interview loop** the org will use to fill it.

The output is not a template. It is a set of documents
another engineer at your company could pick up and use
to interview a candidate for this role tomorrow,
without needing you in the room to explain what any
stage is measuring or how to score it.

## Requirements

Produce **six documents** in a `docs/hiring/loops/<role-slug>/`
directory (or the equivalent shape in your repo):

- `README.md` — the loop overview.
- `stage-01-recruiter-screen.md`.
- `stage-02-technical-screen.md`.
- `stage-03-technical-deep-dive.md` (either take-home
  or pair-programming — you pick which, and justify
  it in the README).
- `stage-04-values-bar-raiser.md`.
- `stage-05-founder-interview.md`.

Plus a `calibration.md` describing the calibration
protocol for the loop.

### The `README.md`

Names the role (with a link back to the row in
exercise 01's plan), summarises the loop, and includes:

- **Role charter** — three sentences on the scope of
  the role, who the hire will report to, and the
  first-90-days success shape.
- **Loop shape at a glance** — the five stages, who
  runs each, and the total candidate-time budget.
- **Take-home vs. pair-programming decision.** Which
  did you pick, and why? Reference chapter 02's
  trade-off explicitly — what does the day-two work
  of this role look most like, and which format
  measures that better?
- **Sourcing note.** Where are candidates coming from
  (referrals, applicants, sourced)? Name the specific
  bias each sourcing channel introduces, and how the
  loop compensates for it.
- **Loop owner.** The person accountable for keeping
  the loop honest — reviewing rubric evidence,
  scheduling calibration, deciding when to change the
  loop.

### Each stage document

Each stage document (`stage-0N-...md`) must include:

- **Purpose.** One paragraph on what this stage is
  measuring that the other four stages are not.
- **Format.** Duration, medium (phone / video / in-
  person), interviewer count, materials (starter repo,
  design prompt, take-home spec).
- **Rubric.** A table with **dimensions** (rows) and
  a **1-4 or 1-5 scale** (columns). Each cell has a
  short **behavioural anchor** — what does a "3 — At
  bar" candidate look like on this dimension? Anchors
  are what stop grading against interviewer mood; fill
  them in.
- **Decision rule.** A written rule for how the stage-
  level score rolls up to a stage-level yes / no. "Any
  1 is a no-hire; two 2s is a no-hire; otherwise
  advance" is a workable default; use it or state your
  variant.
- **Interviewer script / prompt.** What the interviewer
  actually says or shows. For the technical stages
  this includes the code / design prompt. For the
  values / bar-raiser stage this includes the specific
  behavioural questions and the follow-up prompts.
  For the founder stage this includes the founder-
  attachment questions from [`chapter 03`](../03-founding-engineer-profile-and-first-project.md).
- **What the interviewer records.** The evidence
  packet — quotes, code snippets, approaches taken —
  that the debrief will discuss. Not "my impression
  was".

### The take-home OR pair-programming decision

You **must pick one**, not both. The stage-03 document
should read as a coherent single-format stage.

- If you picked **take-home**: the stage document
  includes the specification (a real spec candidates
  will see, not a placeholder), an explicit
  **candidate-time cap** ("this should take 4 hours;
  submit what you have and note where you would go
  next"), the deliverables list, and the debrief
  format (typically a 45-minute walk-through with the
  candidate).
- If you picked **pair-programming**: the stage
  document includes the starter repo (or its
  description), the problem the pair will work on for
  90 minutes, the two-interviewer protocol (who
  drives what portion, when hints are offered), and
  the debrief format (typically a short synchronous
  interviewer huddle within an hour).

### The values / bar-raiser stage

Cite the values the bar-raiser is testing against.
These should be **actual written values**, not
slogans. If your company doesn't have values written
down, this exercise is the trigger to write v0 of
them (2-4 values, one paragraph each on what the
value looks like in practice, with a specific example).

Give the bar-raiser explicit **veto authority** in
the stage document. Chapter 02 makes the point that a
paper-only veto does no work; the stage doc is where
the veto becomes real.

### The `calibration.md`

Describes the calibration protocol that keeps rubric
grading honest:

- **New-interviewer shadowing.** How many shadow loops
  before a solo run? Who observes the first solo
  loops?
- **Weekly hiring debrief.** Cadence, participants,
  agenda (evidence-not-vibes protocol from chapter
  02).
- **Quarterly rubric review.** When the rubric anchors
  themselves get re-read against the last quarter's
  loops.
- **Hiring committee.** If your team is or will pass
  ~10 engineers inside this loop's active window,
  describe the committee's composition, scope, and
  decision rule.

## Starter guidance

- **Pick the role you would actually run next.** Do
  not invent a hypothetical role. The loop only lands
  if it is designed against a specific candidate
  profile and a specific day-two workload.
- **Anchors are the artifact.** The single biggest
  quality lift on a rubric is *writing the anchor
  descriptions*. Skip them and you have a scoring
  form, not a rubric. Write them before running the
  first loop.
- **Prompt-test the stages.** Take a colleague through
  each stage as a mock candidate. If any stage takes
  materially longer than the budget, or leaves the
  colleague unsure what was being measured, revise
  the stage doc — not the interpretation.
- **Do not exceed four hours of candidate loop time**
  (excluding the take-home, if used). Longer loops
  self-select for candidates with slack calendars and
  no competing offers.
- **The founder-attachment questions in stage 5** are
  the ones from [`chapter 03`](../03-founding-engineer-profile-and-first-project.md).
  Do not paraphrase them into blandness — the point
  of the specific questions is the specific answers
  they surface.
- **Cite public references** where relevant. Laszlo
  Bock's *Work Rules!*
  ([worldcat.org — Work Rules!](https://search.worldcat.org/title/875999008))
  is the canonical public reading on Google's
  structured-interview practice; *Software
  Engineering at Google*
  ([abseil.io/resources/swe-book](https://abseil.io/resources/swe-book))
  codifies the hiring-committee mechanic; Amazon's
  Bar Raiser is described publicly at
  [amazon.jobs/en/landing_pages/in-person-interview](https://www.amazon.jobs/en/landing_pages/in-person-interview).
  Cite what you borrow.
- **Avoid interview theatre.** Every question in the
  loop should be solvable at a "3 — at bar" level by
  a current engineer in the same role. Sanity-check
  each stage against this before the first candidate.

## Acceptance criteria

The loop is complete when:

- Another engineer at your company can pick up the
  six documents and run a full loop tomorrow, without
  needing you in the room to interpret any stage.
- Every stage has a written rubric with behavioural
  anchors for each score level and a written
  decision rule for the stage.
- The take-home vs. pair-programming choice is made
  and justified explicitly against the day-two
  workload of the role.
- The bar-raiser stage has an explicit veto and
  cites the values it tests against.
- The founder-interview stage uses the founder-
  attachment questions from chapter 03, not generic
  behavioural questions.
- The calibration document names shadowing, weekly
  debrief cadence, quarterly rubric review, and (if
  applicable) the hiring committee.
- The loop is under 4 hours of candidate time
  (excluding take-home if used).
- The sourcing bias of each channel is named in the
  README, and the loop compensates for it.

The output of this exercise feeds directly into:

- Exercise 05 (promote-vs-hire drill) — the loop the
  external-hire path would run.
- The lab (`lab-01-first-year-hiring-and-org-package-for-your-startup`)
  — the loop is one of the six bundled artifacts.
- Capstone
  [`project-101`](../../../projects/project-101-first-year-technical-strategy-for-one-seed-startup)
  — the loop is a required artifact in the first-year
  technical-strategy package.
