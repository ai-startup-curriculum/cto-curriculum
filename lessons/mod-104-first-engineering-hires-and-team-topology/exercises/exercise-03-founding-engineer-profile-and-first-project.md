# Exercise 03 — Founding Engineer Profile and First Project

**Module:** `mod-104-first-engineering-hires-and-team-topology`
**Planned time:** ~2.5 hours
**Chapter this builds on:** [`03-founding-engineer-profile-and-first-project.md`](../03-founding-engineer-profile-and-first-project.md)

## Problem statement

For the first founding-engineer role in your hiring
plan (exercise 01), author three linked artifacts:

- The **founding-engineer profile** — the T-shape
  description, the Larson staff-archetype hybrid, the
  must-haves, the nice-to-haves, and the honest
  non-goals.
- The **founder-attachment interview kit** — the
  specific questions the founder interview (stage 5
  of the loop from exercise 02) will ask, with the
  "listening-for" notes that turn candidate answers
  into evidence.
- The **first-project brief** — the scoped, two-week
  first-project the hire will pick up on day one,
  designed *before* the offer letter goes out.

Together these three artifacts turn the abstract
"we're hiring a founding engineer" line in the plan
into a concrete definition of who you are hiring, how
you will assess their fit for the founder team, and
what they will actually do on day one.

## Requirements

Produce three documents in a
`docs/hiring/founding-engineer/<role-slug>/`
directory:

- `profile.md`
- `founder-interview-kit.md`
- `first-project-brief.md`

### `profile.md`

- **Role title and level.** Match the seniority in
  your hiring plan (exercise 01) and the level on
  your ladder v0 (exercise 06). Do not over-title.
- **T-shape description.** One paragraph on the top
  of the T (the breadth expected — see chapter 03 for
  the list), one paragraph on the vertical stroke
  (the deep specialism that must exist), and one
  sentence naming *which specialism gap in the
  founding team* this hire is closing. Explicitly
  name the specialisms this hire is *not* going to
  cover — those belong to other hires or to the
  founders.
- **Larson archetype hybrid.** Which of the four
  staff-engineer archetypes from
  [`Staff Engineer`](https://staffeng.com/book)
  (Tech Lead, Architect, Solver, Right Hand) is this
  role a hybrid of? Chapter 03 walks the typical
  founding-engineer hybrid (Tech Lead + Solver); if
  yours is different, justify why.
- **Must-haves.** 4-7 non-negotiable behavioural or
  technical traits, each with a one-sentence
  behavioural marker ("has shipped a production
  system on the primary language of our stack and
  can walk the code" — not "strong engineer").
- **Nice-to-haves.** 3-5 traits that would tip the
  offer but are not necessary. Do not conflate these
  with must-haves.
- **Non-goals.** 2-4 things this role is *not* — a
  full-stack senior product engineer is *not* your ML
  platform engineer; be explicit so the sourcing and
  the loop don't drift.

### `founder-interview-kit.md`

The founder interview (stage 5 of the loop from
exercise 02) uses a specific question set. Author it
here. At minimum, include the founder-attachment
questions from chapter 03, adapted to your specific
situation:

- **"Why us specifically?"** — with 2-3 sentences of
  listening-for notes on what a strong answer looks
  like vs. a weak one for *your* company.
- **"What would make you leave in six months?"** —
  with listening-for notes on what would be a
  disqualifier (the company is visibly on track to
  hit the condition) vs. what would be a healthy
  answer (the candidate is honest about their
  boundaries).
- **"Tell me about a time you disagreed with a
  founder or CEO. What happened?"** — with a
  listening-for note on the distinction between
  productive disagreement and toxic disagreement.
- **"What do you want me to be honest about that
  our careers page will not tell you?"** — with a
  set of specific answers *you* have ready if the
  candidate asks (runway length, specific vendor
  bet, co-founder alignment status, specific
  customer risk).
- **"What are you not going to enjoy about this
  role?"** — with listening-for notes on the fit-
  vs-friction distinction from chapter 03.
- **"How do you make decisions when you don't have
  enough information?"** — with a listening-for note
  on the bias-to-ship-and-revise signal that
  pre-seed / seed work requires.

You may add up to two additional questions specific
to your company. For each question include (i) the
question as the interviewer will ask it, (ii) at
least one follow-up prompt, and (iii) 2-4 sentences
of listening-for notes.

### `first-project-brief.md`

The first-project brief the CTO would share with the
candidate as part of the offer packet. It should:

- **Fit in one page.** Anything longer is a project
  brief, not a first-project brief.
- **Include the goal** — one paragraph on what the
  project is and why it matters.
- **Include the scope** — a bulleted list of what
  is in scope and what is explicitly out of scope,
  with the two-week target.
- **Include the load-bearing-but-not-critical-path
  test** — a sentence explicitly naming that this
  project is not on the path of any customer demo,
  compliance deadline, or launch commitment inside
  the two-week window.
- **Include the day-two-relevance test** — one
  sentence naming *which parts of the day-two role*
  this project rehearses.
- **Include the written-artifact requirement** — the
  ADR (see [`mod-102` chapter 02](../../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md))
  or short design doc the project ends in.
- **Include the "honest fit-check" line** — the note
  in the offer packet cover email that invites the
  candidate to say if this is *not* the kind of
  first-two-weeks work they were hoping for.

## Starter guidance

- **Do not write for a generic founding engineer.**
  Every artifact must be readable as "for *this*
  role, at *this* company, at *this* stage". Generic
  profiles produce generic loops that produce mis-
  hires.
- **The specialism-gap-in-the-founding-team rule** is
  the most important sentence in the profile. If you
  are a deep back-end engineer, do not write a
  profile for a founding engineer with a deep
  back-end specialism — that is the mirror-image
  failure mode from chapter 03.
- **Do not write the founder-attachment questions in
  interview-training-video prose.** Write them as you
  would actually ask them. If your natural phrasing
  is "so — what would make you leave in six months?"
  and not "please share with me the conditions under
  which you might reevaluate your commitment", write
  the former.
- **First-project options to consider** (chapter 03
  works three examples): the observability first-
  project, the Chesterton's-Fence first-project, the
  vendor-swap first-project. Pick the one that
  matches your specific day-two role, and adapt.
- **Do not use the first-project brief as free
  labour.** It is *not* a take-home. The candidate
  is a paid employee at this point; the brief is
  onboarding, not evaluation.
- **Cite the readings you drew from.** Larson's
  *Staff Engineer* ([staffeng.com/book](https://staffeng.com/book))
  for the archetype hybrid; Charity Majors's
  *Engineering Management: The Pendulum Or The
  Ladder*
  ([charity.wtf/2019/01/04](https://charity.wtf/2019/01/04/engineering-management-the-pendulum-or-the-ladder/))
  if you are considering the IC-vs-manager fit of
  the candidate at any point.
- **Do not invent public compensation data.** If the
  equity or base numbers you reference in the profile
  are placeholders, mark them as such (e.g. `<equity
  band: Index Ventures Option Plan lookup pending>`).

## Acceptance criteria

The artifact set is complete when:

- A reader (co-founder, first EM, technical advisor)
  can read `profile.md` in five minutes and
  reproduce the archetype, the must-haves, the
  nice-to-haves, and the specialism-gap this hire is
  closing.
- The founder-interview kit contains at least the
  six chapter-03 questions, each with the
  interviewer's asking phrasing and 2-4 sentences of
  listening-for notes.
- The first-project brief fits on one page, states
  the load-bearing-but-not-critical-path check
  explicitly, and ends in a specified written
  artifact.
- All three documents are consistent — the profile's
  must-haves show up as testable in the founder-
  interview kit; the day-two-relevance test in the
  first-project brief matches the specialism the
  profile requires.
- The artifact set names at least one non-goal in
  the profile and at least one candidate-answer
  category (in the founder-interview kit) that would
  be a disqualifier.
- Nothing in the artifact set is a paste from a
  generic template. Every specific detail is your
  company's specific detail.

The output of this exercise feeds directly into:

- Exercise 02 (loop authoring) — the profile
  informs the technical-screen rubric and the
  founder-interview kit is stage 5 of the loop.
- The lab and capstone
  [`project-101`](../../../projects/project-101-first-year-technical-strategy-for-one-seed-startup)
  — the profile and first-project brief are
  required artifacts in the first-year package.
