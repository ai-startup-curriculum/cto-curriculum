# Designing an Interview Loop That Scales

> An interview loop is the process the company runs on
> every candidate. If it works only when the CTO is in the
> debrief, it doesn't work — it's a bottleneck that
> becomes the reason strong candidates go elsewhere while
> the loop waits for a founder calendar slot.

## Motivation

At the founding-team stage, the interview loop is often
"the CTO talks to the candidate for two hours, likes them,
sends an offer". That works for the first two hires — the
candidate self-selected by knowing the founder, the
signal is unambiguous, and the calendar has room.

It stops working somewhere between the fourth and the
sixth hire, for four reasons:

- **Volume.** At a seed hiring pace of two hires per
  quarter across two open roles, you are seeing 40-100
  candidates a quarter through a top-of-funnel that has
  to say no to most of them fast.
- **Calibration drift.** Without a rubric, each engineer
  who joins the debrief judges candidates against a
  different bar, and the bar drifts based on which
  candidate the interviewer talked to last.
- **Legal exposure.** Unstructured interviews with no
  rubric produce hiring decisions that cannot be
  defended against a discrimination claim. The rubric is
  the artifact that proves the decision was made against
  the same criteria for every candidate.
- **Founder-only failure mode.** The loop cannot scale
  past what the CTO's calendar can absorb. Every open
  role starves.

This chapter names the five-stage loop the CTO authors
once and the org runs many times, walks the take-home
vs. pair-programming trade-off in the technical stage,
and describes the rubric and calibration process that
keeps the loop honest as the interviewer pool grows.
Google's own writeup of its structured-interview and
hiring-committee practice — most legibly in *Work Rules!*
by Laszlo Bock — is a reasonable public reference for the
shape; *Software Engineering at Google*
([abseil.io/resources/swe-book](https://abseil.io/resources/swe-book))
codifies the operational discipline for the loop and the
committee.

## The five-stage loop

Every stage has (i) a clear purpose, (ii) a rubric, (iii)
an explicit *what would make me say no* criterion, and
(iv) a time budget that keeps the whole loop under
roughly four hours of candidate time (excluding the
take-home, if one is used).

### Stage 1 — Recruiter screen (25-30 minutes, phone)

- **Purpose** — confirm the fit basics: role, seniority,
  target compensation, location / remote, timing,
  motivation for looking. Save both sides the deeper
  loop if these don't line up.
- **Who runs it** — a recruiter (in-house or contracted).
  At pre-seed / seed the "recruiter" is often the CTO or
  the CEO. That's fine — but the *screen* is still a
  structured 25-minute call, not an hour of unstructured
  founder time.
- **Rubric focuses on** — verifiable basics only:
  employment history matches the resume, comp expectation
  is inside the band (chapter 01), the candidate can
  articulate one specific reason they want to join this
  specific company. Do not attempt technical assessment
  here.
- **No-go criteria** — comp expectation is materially
  above the band and cannot be closed with equity;
  location / work-authorisation does not work; motivation
  is generic ("I want to work at a startup").

### Stage 2 — Technical screen (60 minutes, video)

- **Purpose** — assess the candidate can *think about*
  and *talk about* engineering work at the level the role
  requires. Not a full technical assessment; a filter
  that rules out mis-hires before the loop invests four
  more hours in them.
- **Who runs it** — a senior engineer or a tech lead. At
  founding-team scale it is the CTO or the first
  founding engineer. As soon as there are two engineers
  who can run this stage, alternate them.
- **Format options** — a scoped 45-minute code /
  design exercise plus 15 minutes of Q&A, OR a
  discussion of a past project the candidate led plus a
  short whiteboard problem. Pick one format and stick to
  it across the entire pipeline for the role — mixing
  formats is a common source of calibration drift.
- **Rubric focuses on** — problem decomposition, choice
  of data structures / algorithms, ability to reason
  about failure modes, and communication. For senior /
  staff candidates the rubric weighs *judgment* and
  *scoping* — how the candidate decides what *not* to
  build — as heavily as raw coding skill.
- **No-go criteria** — cannot articulate the constraint
  that motivates a technical choice; cannot describe a
  failure mode of their own design; does not respond to
  hints or push-back in a way that suggests they will
  collaborate on architecture decisions.

### Stage 3 — Deeper technical: take-home OR pair-programming

This stage is the one the loop designer must decide about
explicitly. Each format has costs the other does not, and
you should not run both — that is four hours of the
candidate's time for a signal one of them would give.

#### Option A — take-home exercise (candidate-time budget: 3-5 hours, capped)

- **Shape** — a scoped problem the candidate solves
  offline, with a written README explaining the design.
  Followed by a 45-minute debrief where the candidate
  walks the code and answers questions.
- **What it measures well** — how the candidate writes
  code they are willing to put their name on; how they
  document trade-offs; how they scope; how they handle
  the edge cases they had time to think about rather than
  the ones they were surprised by in an interview.
- **What it measures poorly** — how the candidate
  performs under time pressure; how they collaborate
  live; how they respond to a real-time push-back.
- **Cost to the candidate** — real hours of unpaid
  weekend / evening work. This *selects against*
  candidates with caregiving responsibilities, second
  jobs, or existing full-time roles they cannot dial
  down. The bar for imposing a take-home is that the
  role's day-to-day work is closer to "long-form deep
  work" than to "live collaboration under uncertainty".
- **Cap the time.** State an explicit cap ("this should
  take four hours; if it takes longer, submit what you
  have and note where you would go next"). Reject the
  temptation to reward the candidate who spent twelve
  hours — you are hiring for judgment, not availability.

#### Option B — pair-programming (candidate-time budget: 90 minutes, on the loop)

- **Shape** — a live 90-minute session with two
  interviewers, working through a scoped problem with a
  starter repo. The candidate drives; the interviewers
  ask questions, offer hints, and sometimes take the
  keyboard.
- **What it measures well** — how the candidate thinks
  live, collaborates, handles push-back, absorbs new
  code, and prioritises under time pressure. Closer to
  the actual day-two experience of on-call and incident-
  response work.
- **What it measures poorly** — how the candidate writes
  code they would put their name on; how they scope over
  a longer time horizon.
- **Cost to the candidate** — 90 minutes of stressful
  live-coding. Does not select against caregivers the way
  a take-home does, but does select against candidates
  who freeze under observed coding pressure — some of
  whom will be excellent day-two colleagues.

#### How to choose

- **Take-home fits** roles where the day-two work is
  weeks-long deep work — foundational back-end, ML
  research engineer, infra platform, security engineer.
- **Pair-programming fits** roles where the day-two work
  is high-velocity collaborative iteration — full-stack
  product engineer, on-call SRE, tech-lead-track hires.
- Whichever you choose, **choose one per role and stick
  with it**. The most common failure mode here is running
  a take-home for the first three candidates, running a
  pair session for the next two because the founder heard
  a talk about it, and then trying to compare the debrief
  packets. You cannot; the signals are not commensurable.

### Stage 4 — Values / bar-raiser interview (45-60 minutes)

- **Purpose** — assess *how* the candidate works, not
  *whether* they can code. Whether they collaborate,
  disagree well, own mistakes, mentor peers, and — the
  hard-to-name-but-real signal — whether they raise the
  bar of the team they join or drop it.
- **Who runs it** — a senior engineer or a founder who is
  *not* the hiring manager. Amazon's original naming for
  this role is "Bar Raiser" — a trained interviewer whose
  charter is to protect the long-term hiring bar even at
  the cost of the specific hiring manager's short-term
  need. Amazon's public description of the practice is at
  [amazon.jobs/en/landing_pages/in-person-interview](https://www.amazon.jobs/en/landing_pages/in-person-interview).
- **Format** — structured behavioural questions ("tell me
  about a time you disagreed with a technical decision
  your manager made") with follow-ups that pressure-test
  the specifics. The interviewer takes notes on the
  specific *behaviour*, not on their impression of it.
- **Rubric focuses on** — the company's actual values
  (which must exist as written statements, not slogans;
  see chapter 06 for the values-in-the-ladder mechanic);
  disagreement style; ownership of past failures;
  evidence of mentoring or lifting the bar for peers.
- **The bar-raiser has a veto.** By construction. If the
  bar-raiser says no, the offer does not go out — even
  if the hiring manager is enthusiastic. Making this
  veto real is the *point* of the role; if the bar-
  raiser's opinion can be overruled by the hiring
  manager's enthusiasm, the role does no work.

### Stage 5 — Founder interview (30-45 minutes)

- **Purpose** — the founder-attachment stage. The
  founder assesses (a) mission alignment ("why *this*
  company and not the fifty others hiring right now?"),
  (b) sensor for the specific ambiguity of pre-seed /
  seed work, and (c) the founder's own gut ("would I
  want to be in a war-room with this person at 2 a.m.
  when the incident is bad?"). The candidate assesses
  the founder in return — this stage is a two-way sell.
- **Who runs it** — the CEO or the CTO, depending on the
  role. At founding-team scale it is often both, in
  sequence.
- **Rubric focuses on** — founder-attachment questions
  the CTO should have written down in advance (see
  chapter 03 for a specific set): what motivated the
  candidate to look now? what have they turned down
  recently and why? what would make them leave in six
  months? what would they want the CTO to be honest
  about that a career page will not tell them?
- **No-go criteria** — the candidate cannot articulate a
  specific reason for wanting *this* company; the
  candidate's honest answer to "what would make you
  leave in six months" is a condition the company will
  visibly hit inside six months.

## Rubrics — the artifact that makes the loop honest

A rubric is a written, per-stage document with (i) the
dimensions being assessed, (ii) a 1-4 or 1-5 scale for
each, (iii) short anchor descriptions for each score
level, and (iv) a decision rule for how the stage-level
scores roll up. The interviewer's job is to *record
evidence* against the rubric — quotes, code snippets,
approaches taken — rather than to record their
impression.

A minimum rubric for the technical screen (stage 2):

```
Dimension                              | 1 - No hire | 2 - Below bar | 3 - At bar | 4 - Above bar
---------------------------------------|-------------|---------------|------------|--------------
Problem decomposition                  | ...         | ...           | ...        | ...
Data structure / algorithm choice      | ...         | ...           | ...        | ...
Reasoning about failure modes          | ...         | ...           | ...        | ...
Communication under push-back          | ...         | ...           | ...        | ...
```

Each cell needs a short *anchor description*: what does a
"3 — At bar" look like on this dimension? Anchors are
what stop interviewers from grading against their mood.
Fill them in *before* running the loop, not after the
first candidate.

The decision rule at stage 2 is typically: **any 1 is a
no-hire**; any two 2s is a no-hire; otherwise the
candidate advances. Write the rule down; do not vote on
it per candidate.

The two references worth reading before authoring rubrics:

- **Laszlo Bock — *Work Rules!*** —
  [worldcat.org — Work Rules!](https://search.worldcat.org/title/875999008)
  — Google's public account of how structured
  interviewing and hiring committees replaced founder-
  gut hiring at scale.
- **Winters, Manshreck, Wright (eds.) — *Software
  Engineering at Google*** —
  [abseil.io/resources/swe-book](https://abseil.io/resources/swe-book)
  — the hiring-committee chapter is a working
  description of a scaled interview-loop shape.

## Calibration — the process that keeps rubrics honest

A rubric that is written once and never re-examined
drifts. Calibration is the recurring process that keeps
the rubric — and the interviewers — honest.

- **New-interviewer shadowing.** Every new interviewer
  shadows two loops as a silent observer before running
  one, then is shadowed on their first two solo loops
  by an experienced interviewer. Feedback is against
  the rubric-use, not the outcome.
- **Weekly hiring debrief.** Every active loop is walked
  through in a 30-minute weekly meeting with all
  interviewers who ran a stage. The unit of discussion
  is the *evidence* the interviewer recorded, not the
  overall thumbs-up or thumbs-down. Disagreements are
  the whole point — they are how the interviewers
  align on what a "3" means.
- **Quarterly rubric review.** The rubric itself is
  re-read once a quarter, with the last quarter's
  loops as evidence. Anchors that turned out to be
  ambiguous get sharpened; dimensions that turned out
  to be non-predictive get dropped.
- **The hiring committee.** Once the team is past ~10
  engineers and the CTO can no longer sit in every
  debrief, a **hiring committee** of 3-5 senior
  engineers reviews every offer decision, using the
  interviewers' evidence packets. The committee is the
  bar-holder; the hiring manager owns the role and
  writes the offer, but does not unilaterally decide.
  The point is to prevent the "we're desperate, ship
  the offer" failure mode at scale.

## Failure modes

- **The founder-only loop that never scales.** The CTO
  is in every debrief; nobody else's opinion has weight.
  When the CTO's calendar is full, hiring stalls. Fix:
  the CTO writes the rubric, trains the first three
  interviewers, and steps out of the debrief as soon as
  the trained interviewers can carry it.
- **The unwritten rubric.** The debrief is a group vibe-
  check. The team defaults to hiring people who resemble
  the current team. Fix: write the rubric down, train
  interviewers to record evidence against it, and treat
  the rubric as the artifact discrimination-claim
  defensibility ultimately rests on.
- **The vetoing bar-raiser without a veto.** The bar-
  raiser role exists on paper, but hiring managers
  routinely override it when they like the candidate. The
  role does no work. Fix: the veto is real by
  construction, or the role should not exist. Amazon's
  original discipline (linked above) is the reference for
  what "real veto" looks like.
- **The take-home *and* pair-programming.** The team runs
  both because they cannot decide. The candidate loop is
  seven hours long; the debrief cannot compare the
  signals; strong candidates drop out mid-loop. Fix: pick
  one per role. Chapter 03's founding-engineer profile
  will tell you which one fits.
- **The "we hired for culture" rationalisation.** The
  loop had no values / bar-raiser stage, hires drifted
  toward "people we get along with", and now the team is
  three cousins of one archetype. Fix: bring back the
  bar-raiser stage, and audit the last N hires' rubric
  evidence to see where the drift started.
- **Interview theatre.** The loop includes a live-coding
  question so hard nobody has ever finished it, or a
  system-design question the interviewer themselves
  couldn't answer without prep. The candidate learns the
  team is not serious. Fix: every question in the loop
  should be *solvable, at a "3 — at bar" level, by a
  current engineer in the same role*. If not, cut it.

## Summary

- The interview loop the CTO authors once and the team
  runs many times is **five stages**: recruiter screen,
  technical screen, take-home OR pair-programming (pick
  one), values / bar-raiser interview, founder
  interview.
- The **take-home vs. pair-programming** trade-off is
  real. Take-home rewards deep-work archetypes and
  selects against caregivers; pair-programming rewards
  live-collaboration archetypes and selects against
  candidates who freeze under observation. Pick per
  role; do not mix within a role.
- **Rubrics** — dimensions, 1-4 or 1-5 anchor
  descriptions, and a written decision rule — are the
  artifact that keeps the loop honest and defensible.
  Fill anchors *before* the first candidate.
- **Calibration** — new-interviewer shadowing, weekly
  debriefs against evidence not vibes, quarterly rubric
  review, and (past ~10 engineers) a hiring committee
  — is what keeps rubrics from drifting.
- The **bar-raiser** (Amazon's naming) exists to
  protect the long-term bar against the hiring
  manager's short-term need. If the veto is not real by
  construction, the role does no work.
- The failure modes to avoid are the founder-only loop,
  the unwritten rubric, the paper-only bar-raiser, the
  double take-home + pair, culture-code-as-cousins
  hiring, and interview theatre.

The chapter's paired exercise —
[`exercise-02-interview-loop-and-rubrics-authoring.md`](exercises/exercise-02-interview-loop-and-rubrics-authoring.md)
— walks the authoring of a full loop for one open role,
including the take-home vs. pair decision, the five
rubrics, and the calibration protocol. Chapter 03
describes the specific candidate archetype the founding-
engineer loop is filtering for.
