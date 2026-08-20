# Exercise 05 — Promote-vs-Hire First-EM Drill

**Module:** `mod-104-first-engineering-hires-and-team-topology`
**Planned time:** ~2 hours
**Chapter this builds on:** [`05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md`](../05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md)

## Problem statement

Run the **two-column promote-vs-hire drill** from
chapter 05 against a **specific first-EM decision** —
either a real one you are facing, or a realistic
composite drawn from the shape of your (or a real
reference) startup at the point where the first-EM
trigger would fire.

Produce a **written decision memo** the CEO could
read in ten minutes and either accept, reject, or
push back on with specific questions. The memo is the
artifact that turns the informal "we probably need to
promote / hire an EM" conversation into a decision
that has been thought through and can be defended.

## Requirements

Produce a single document, `docs/hiring/decisions/
first-em-<version>.md` (or the equivalent in your
repo), with the following sections.

### 1. Situation

- **The trigger.** Which of chapter 05's three
  first-EM triggers has fired — team-size (6-8
  direct reports to the CTO), calendar composition
  (CTO calendar is >50% 1:1s and hiring), or
  interpersonal complexity (a performance-management
  or difficult-conflict conversation on the
  horizon)? Be specific — cite the actual signal.
- **The team.** Which team (from the topology in
  exercise 04) does this EM own? How many ICs?
  What is the current management arrangement (CTO
  as EM, informal tech lead, unclear)?
- **The internal candidate(s).** If any, name them
  by role — do not use real names in the memo if it
  will be shared beyond a private founder audience;
  use archetypes. For each internal candidate,
  three sentences on what makes them a plausible
  fit.
- **The role charter.** One paragraph on what the
  first EM will own — hiring, 1:1s, feedback,
  performance-management, delivery cadence, career
  conversations. Anchor to the day-two management
  craft owned by
  [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (level 30) — the CTO is *deciding to hire* the
  EM here; the day-two craft is that peer track.

### 2. The two-column drill

Reproduce chapter 05's honest promote-vs-hire drill
verbatim, and fill in your answers per row. Do not
skip rows. Chapter 05's table has ten questions; use
all ten.

For each row, write **one sentence of reasoning**
justifying the answer. A one-word "Yes / No" is not
enough — the memo has to be readable by someone who
was not in your head when you filled it in.

The two hard-signal rows — "Am I promoting to retain
them?" and "Am I hiring to avoid a hard
conversation?" — get **a full paragraph each**
regardless of the answer, because those are the
failure modes the drill exists to surface. If you
answer "no" to both, the paragraph explains why the
temptation to answer "yes" is not present. If you
answer "yes" to either, the paragraph explains what
you are going to do instead of promote or hire.

### 3. The decision

- **Direction** — promote or hire.
- **The specific person or profile.** If promote,
  name the archetype and the role change (what the
  promoted person stops doing IC-side to make room
  for the EM work). If hire, name the profile
  (seniority, EM archetype from the ladder v0 in
  exercise 06, prior-experience must-haves) and
  reference the interview loop (from exercise 02, or
  a new one if the loop for this role doesn't exist
  yet).
- **The reversibility.** How reversible is this
  decision at 90 days if it isn't working? Chapter
  05's failure modes ("promoted-to-management-
  without-choice", "hired-externally-into-a-broken-
  team") both have specific 90-day symptoms; name
  the symptoms you would look for and the reversal
  you would run.

### 4. The onboarding plan (first ninety days)

Regardless of direction, sketch the first-ninety-day
onboarding plan for the new EM. Cover:

- **Week 1-2.** Meet-the-team, calendar reset,
  1:1s installed, immediate delivery cadence
  observed.
- **Month 1.** First difficult conversation (if
  any) handled by the new EM with the CTO in
  support; first hiring loop the EM owns end-to-
  end; first tools installed (1:1 template,
  feedback template, career-conversation template
  — the day-two content owned by
  [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)).
- **Month 2-3.** First calibration conversation
  with peers (chapter 06's ladder v0 is the
  input); first team-level retrospective the EM
  runs; first roadmap iteration the EM owns.
- **90-day check-in.** Explicit success criteria
  the CTO and CEO agree on now, and which the CTO
  would use to confirm the direction was correct.

### 5. The alternative you rejected

One paragraph on the other direction of the
decision. What would you have done if you had gone
the other way? What are the two or three specific
risks that made you *not* go that way? This section
is what makes the memo defensible against a "did you
really consider the alternative?" board question.

### 6. Sign-off

The memo ends with:

- The date.
- The author (you, as CTO).
- The intended audience (CEO; optionally CEO +
  founding-team; optionally CEO + board — call it).
- The **decision deadline** — when the CEO / board
  needs to have said yes or no.

## Starter guidance

- **Use a realistic composite if the real decision
  is too sensitive to write down.** The learning
  lands either way. If you do use a composite, note
  it at the top of the memo so future-you (or the
  peer reading over your shoulder) does not
  confuse it with a real decision.
- **The two hard-signal rows are the whole point.**
  If the drill surfaces retention-promotion or
  conflict-avoidance-hiring, you already got the
  value; the memo's next step is to name the
  alternative action (a compensation review, a
  frank conversation, a scoped promotion below
  EM). Do not overwrite the hard signal.
- **Cite the readings.** Fournier's *The Manager's
  Path* (CTO / EM chapters —
  [oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/))
  and Horowitz's *The Hard Thing About Hard
  Things* (chapters on hiring executives and
  management debt —
  [harpercollins.com](https://www.harpercollins.com/products/the-hard-thing-about-hard-things-ben-horowitz))
  are the two load-bearing texts. Cite the specific
  chapter or vocabulary you drew from.
- **The pendulum vocabulary.** If you are
  considering promoting an IC to EM, note whether
  they see the switch as one-way ("I'm becoming a
  manager") or pendulum ("I'll try the EM seat and
  return to IC if it doesn't fit"). Charity
  Majors's *Engineering Management: The Pendulum
  Or The Ladder*
  ([charity.wtf/2019/01/04](https://charity.wtf/2019/01/04/engineering-management-the-pendulum-or-the-ladder/))
  is the reference; making the pendulum explicit
  is one of the highest-leverage things you can do
  for the promoted person's psychological safety.
- **The 90-day reversibility question is not
  hypothetical.** Chapter 05's failure modes have a
  90-day symptom set; know what yours are before
  the person starts.
- **Do not decide in the memo what you did not
  research.** If you are unsure about the
  compensation implication, mark it `<comp: People
  lead to confirm>` and move on. The memo does not
  need to close every open question — it needs to
  make the decision clear.

## Acceptance criteria

The memo is complete when:

- A reader (CEO, co-founder, board member) can
  read it in ten minutes and know (a) the trigger
  that made the decision timely, (b) which
  direction you are recommending, (c) the specific
  person or profile, (d) the alternative you
  rejected and why, and (e) the 90-day check-in
  criteria.
- The two-column drill is filled in, every row
  justified in one sentence, and the two hard-
  signal rows have a full-paragraph answer each.
- The onboarding plan names specific week-1-2 /
  month-1 / month-2-3 / 90-day-check-in
  activities, not generic phrases.
- The boundary to
  [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (level 30) is cited — the memo names what the
  CTO is *deciding* (the hire / promotion) versus
  what the day-two craft (owned by the peer track)
  is.
- The memo has a decision deadline. An open-ended
  memo is not a decision memo.

The output of this exercise feeds directly into:

- The lab (`lab-01-first-year-hiring-and-org-package-for-your-startup`)
  — the memo is one of the six bundled artifacts.
- Exercise 06 — the direction (promote or hire) is
  reflected on the org chart, and the ladder v0
  must have an EM role described clearly enough
  for the drill's role charter to reference it.
- Capstone
  [`project-103`](../../../projects/project-103-scaling-plan-from-five-to-fifty-engineers)
  — the first-EM decision is a load-bearing
  artifact in the scaling plan.
