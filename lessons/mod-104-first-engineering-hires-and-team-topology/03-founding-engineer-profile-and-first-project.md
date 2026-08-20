# The Founding Engineer — Profile, Equity, First Project

> "The Right Hand acts as a force multiplier for a senior
> leader — with the trust, context, and judgment to make
> decisions on their behalf." — Will Larson describing one
> of the four staff-engineer archetypes in *Staff Engineer*
> ([staffeng.com/book](https://staffeng.com/book)). The
> founding engineer at pre-seed is closer to a **Right
> Hand + Tech Lead hybrid** than to any specialist
> archetype the CTO is likely to encounter later.

## Motivation

The first two or three engineering hires at a pre-seed /
seed startup are a categorically different decision from
every hire after them.

- **The equity grant is materially larger.** A founding
  engineer typically receives an equity band that
  overlaps the low end of the co-founder band, not the
  high end of the employee band — because they are
  taking on a significant amount of founder-shape
  personal and financial risk.
- **The scope is the whole product surface.** There is no
  team to hand a subsystem to. The founding engineer
  owns the build system on Monday, an incident on
  Tuesday, a customer-facing feature on Wednesday, and
  the pitch-deck demo on Friday.
- **The candidate is *also* hiring you.** The candidate
  is joining a company with two founders, no
  product-market fit, and a runway that ends. Their
  filter on you is at least as sharp as your filter on
  them, and they will walk if either the founders or
  the mission does not stand up.
- **The mis-hire is unusually expensive.** At founding-
  engineer scale, one bad hire is 25-33% of your
  engineering org for the six months it takes to
  recognise and resolve the mistake. There is no
  headcount cushion.

This chapter names the profile the founding-engineer
loop is filtering *for*, the equity band the offer sits
in, the founder-attachment questions the founder
interview (chapter 02 stage 5) needs answers to, and the
shape of the *first project* the founding engineer picks
up — the one artifact that turns a hire into a working
colleague rather than a frustrated new starter.

## The T-shaped generalist

The dominant profile the founding engineer needs to match
is what Valve's employee handbook popularised as the
**T-shape**: broad competence across most of the stack
(the top of the T), with real depth in at least one
area (the vertical stroke).

At pre-seed / seed the top of the T is broader than at
any other stage of the company. The founding engineer is
expected to be able to:

- Wire a CI pipeline from scratch and merge PRs to it.
- Deploy the production environment on the chosen cloud.
- Design and implement the first RDBMS schema, and know
  when to reach for Redis / a queue / a search index.
- Write both the back-end API and enough of the front-end
  to demo it to a customer.
- Debug the first production incident — including one
  where the observability stack has not yet been
  installed.
- Have an opinion on which vendors from mod-103's build-
  vs-buy matrix to install first, and defend it.

The vertical stroke — the deep specialism — matters,
but its specific *content* matters less than its
existence. A founding engineer with deep back-end depth
and passable-but-not-deep front-end skill works; a
founding engineer with deep ML-systems depth and
passable-but-not-deep back-end skill works; a founding
engineer with medium competence across everything and
no deep specialism *does not* work — the team has no one
who can go deep when a specific technical decision
requires depth.

The founder's own deep specialism informs which vertical
stroke the founding engineer must have. If the founder
CTO is a deep back-end engineer, the founding engineer
whose deep specialism is *also* back-end is a duplicated
capability with a hole where the front-end / infra /
data specialism should be. Chapter 04 will make this
explicit against the roadmap: hire founding engineers
whose deep specialisms *cover the gaps in the founding
team*, not the areas the founders are already deep in.

## Larson's staff archetypes at founding-engineer scale

Will Larson's *Staff Engineer*
([staffeng.com/book](https://staffeng.com/book)) names
four archetypes for staff-and-above IC engineers: **Tech
Lead**, **Architect**, **Solver**, and **Right Hand**.
At founding-engineer scale, the useful archetypes are a
subset — and typically hybridised.

- **Tech Lead** — leads a team's technical direction,
  owns the roadmap for a well-defined slice, and mentors
  the engineers in that slice. At founding-engineer
  scale there is no "team" to lead yet, but this
  archetype's *judgment about scoping and sequencing*
  is exactly what the CTO needs a peer on.
- **Architect** — sets direction for a critical area,
  authors the ADRs (see [`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md)),
  and thinks in longer time horizons. At founding-
  engineer scale this is often *shared with the CTO*
  rather than fully delegated.
- **Solver** — parachutes into the hardest technical
  problems and gets them unstuck; often works alone or
  with a small team. At founding-engineer scale this is
  effectively the on-call incident-responder role.
- **Right Hand** — operates as a trusted extension of a
  senior leader; makes decisions on their behalf.
  Rarely relevant at founding-engineer scale (the CTO
  can still make every decision), but it is the
  archetype the *first tech lead* (see chapter 05) is
  usually shaped to be.

The founding engineer at pre-seed / seed most often
matches a **Tech-Lead + Solver hybrid**: senior enough
to lead a slice's technical direction *when there is a
slice to lead*, and comfortable enough with unbounded
ambiguity to parachute into whichever fire is on today.
The **Architect** archetype starts to appear at hire #3
or #4; the **Right Hand** at rung (c) (Series-A) and
above (see [`mod-101` chapter 01](../mod-101-cto-role-and-ownership-map/01-cto-ladder-pre-seed-to-series-b.md)).

## The equity band

Equity at founding-engineer scale is the compensation
lever that does the most work.

The public reference points the CTO cites when
authoring the equity portion of the offer:

- **Y Combinator** — the historical YC founder-facing
  guidance on founding-engineer equity ranges (typically
  in the low-single-digit percent range for very early
  hires, dropping fast for later hires). Current
  guidance sits inside the YC startup school library
  ([startupschool.org/library](https://www.startupschool.org/library))
  and inside YC's Work at a Startup site
  ([workatastartup.com](https://www.workatastartup.com/)).
- **Carta State of Startup Compensation** — the aggregate
  cap-table data by stage; the equity-band by seniority
  and role table is a common CFO / People-lead reference.
  See [carta.com/blog](https://carta.com/blog/) for
  Carta's ongoing publications.
- **Index Ventures Option Plan** —
  [indexventures.com/optionplan](https://www.indexventures.com/optionplan/)
  — Index's public tool for benchmarking option grants
  by role, seniority, and stage. Widely cited by
  founders as a reference band.
- **Peter Thiel** — the classic advice in *Zero to One*
  is that founding-team compensation should skew *heavily*
  toward equity, and cash below a level where the hire is
  materially bought-in to the outcome rather than the
  paycheck. That advice is a heuristic, not a rule; the
  band the CTO offers still has to be a band the
  candidate can actually take-home enough to live on.

The vest shape at seed / Series-A stage is typically
**four-year vest with a one-year cliff**, sometimes
with an **acceleration clause** on a change-of-control
(single- or double-trigger). Founding-engineer offers
sometimes also include:

- **Early-exercise / 83(b) filing eligibility.** Allows
  the employee to exercise unvested options at the
  low strike price and file an 83(b) election within 30
  days. Meaningful US tax consequence for the employee
  when the equity later appreciates. The CTO should
  flag the option; the *tax advice* is not the CTO's to
  give — the employee consults a personal tax advisor.
- **Refresher grants at a defined cadence.** Some
  founding-engineer offers include an expected refresher
  grant on a two- or three-year cadence, so the
  engineer's future comp does not trail-off dramatically
  when the first grant fully vests.

The three failure modes to avoid on equity:

- **Under-granting a founding engineer.** Offering an
  employee-band grant to a candidate taking founder-
  shape risk. The candidate walks, or takes the offer
  and leaves in eighteen months when the reality of the
  grant sinks in.
- **Over-promising on future dilution.** Telling a
  candidate their grant will not be diluted, or
  hand-waving the dilution model. Every future raise
  dilutes; be honest about the shape.
- **Confusing % of the cap table with $ of expected
  value.** A 2% grant of a $2M pre-money is a very
  different offer from a 0.5% grant of a $200M
  post-Series-A cap table. Communicate both the % and
  the *most-recent-round implied value* of the grant,
  and be explicit that the implied value is a snapshot,
  not a promise.

## Founder-attachment interview questions

The founder interview (chapter 02 stage 5) at founding-
engineer scale is not a standard behavioural loop. Its
purpose is to test the specific attachment the candidate
would have to *this founding team and this mission* —
because a founding engineer who is joining "because it's
a startup" will churn out at the first stress event, and
"because it's a startup" is the default answer if you do
not ask the right questions.

A working question set for the founder interview:

- **"Why us specifically? What are the other three
  companies you're talking to, and what would tip you
  toward one of them over us?"** The candidate should be
  able to name specifics. Silence or generic answers
  here mean the candidate has not thought about
  attachment; the offer is at high risk of being used
  as a bargaining chip against another one.
- **"What would make you leave in six months?"** — the
  most useful founder question in the loop. The candidate
  answers honestly if the interviewer signals honest
  answers are safe. Common honest answers: "if the mission
  turns out not to be the mission you're pitching me now",
  "if the founders can't align on direction", "if I turn
  out to be a bad match for the customer segment". The
  CTO's follow-up question is whether the company is
  visibly on track to hit any of those inside six months.
- **"Tell me about a time you disagreed with a founder
  or CEO. What happened?"** Founding engineers must be
  able to disagree, in the room, without becoming toxic.
  Candidates who cannot cite a real disagreement have
  either not been in a position to disagree yet (a
  seniority mismatch signal) or are avoiding the
  question.
- **"What do you want me to be honest about that a
  careers page will not tell you?"** Asks the candidate
  to name the specific ambiguity or risk they want the
  CTO to disclose. Honest answers here: runway length,
  cofounder-dispute risk (see [`mod-108`](../mod-108-cto-ceo-and-board-communication/README.md)),
  the specific customer commitments the company is
  behind on, the specific vendor bet the team has made
  that could unwind. This is the founder's opportunity
  to be honest in return, and to see how the candidate
  reacts to honest answers.
- **"What are you not going to enjoy about this role?"**
  — surfaces the mismatch the candidate has already
  noticed but was going to accept quietly. Common
  answers: "I don't love the customer segment", "I've
  never enjoyed being on-call and this role has a lot
  of it", "I want to write more code than I'll get to
  write". The follow-up is whether the company can
  absorb the friction or whether it is a mismatch.

- **"How do you make decisions when you don't have
  enough information?"** — the specific pre-seed / seed
  competence. The answer must include a *bias to ship
  and revise* rather than a bias to wait for more data.

The interviewer's job is to *record the specific
answers*, not to grade the candidate on charisma. The
answers become the founder-interview evidence packet the
values / bar-raiser (chapter 02 stage 4) references in
calibration.

## The first-project design

The single most under-invested-in artifact for a founding
engineer's first thirty days is the **first project**.
The default — "figure it out and pick something up" — is
how strong hires quit inside sixty days.

A well-designed first project has four properties:

- **Scoped to complete in the first two weeks.** Long
  enough to demonstrate real production work, short
  enough that the engineer ships a visible result before
  their onboarding energy runs out. This is not a scope
  the CTO invents on day one; it is a scope the CTO has
  pre-planned before the offer went out.
- **Load-bearing but not on the critical path of a
  customer commitment.** The project should matter — the
  team should care about the result — but it must not be
  on the path of a demo-in-a-week or a compliance
  deadline. The engineer needs the freedom to make
  mistakes on the first project without production-level
  consequences.
- **Touches the areas the day-two role will spend most of
  its time in.** If the role is a back-end + on-call hire,
  the first project touches an incident-response tool, a
  deployment pipeline improvement, or a well-scoped API
  refactor. If the role is a full-stack product engineer,
  the first project ships an end-to-end feature slice
  behind a feature flag.
- **Ends in a written artifact.** The engineer writes an
  ADR (see [`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md))
  or a mini design doc for the change they shipped. This
  artifact both codifies the first-project decision and
  is the first evidence in the calibration loop for that
  engineer's design-doc craft.

Working examples of first-project shapes:

- **The observability first-project.** New engineer picks
  the observability capability that most needs
  attention — a missing dashboard, a noisy alert, a gap
  in the trace instrumentation for the highest-traffic
  path — and lands the improvement, with a short doc on
  what they changed and why.
- **The Chesterton's-Fence first-project.** New engineer
  picks a specific *seemingly-odd* choice in the codebase
  and writes a one-page doc explaining why it's there —
  which forces the engineer to read code and *ask*, and
  forces the team to be honest about what is intentional
  versus what has drifted. (Fowler on Chesterton's Fence
  in the codebase context is a reasonable reading here —
  [martinfowler.com/bliki/](https://martinfowler.com/bliki/).)
- **The vendor-swap first-project.** New engineer takes
  one row of the build-vs-buy matrix ([`mod-103` chapter
  01](../mod-103-build-vs-buy-and-platform-economics/01-build-vs-buy-as-portfolio-decision.md))
  and executes the swap — replaces a manual process
  with a managed vendor, or replaces a poorly-fitting
  vendor with an in-house version — and lands the ADR
  for the change.

The CTO writes the first-project brief *before the
candidate accepts the offer*, and shares it as part of
the offer packet ("here's what we're thinking your first
two weeks look like — is this the kind of work you were
hoping for?"). This is not just onboarding hygiene; it
is a **final honesty check on the fit** — a candidate
who is enthusiastic about the offer but flat on the
first-project brief is telling you something you should
listen to before the offer is signed.

## Failure modes

- **The mirror-image hire.** The CTO hires their own
  deep specialism twice, leaving a hole in the parts of
  the stack the founding team was already thin on. Fix:
  hire the founding engineer whose deep vertical stroke
  *covers a gap*, not one you already cover.
- **The reference-check-only hire.** The founding
  engineer comes from the CTO's network, everyone likes
  them, the loop is a formality. The rubric-based signal
  is absent; the hire's founder-attachment is untested;
  the mismatch surfaces in month six. Fix: run the full
  loop even when the candidate is a strong referral,
  and take the founder-attachment questions seriously.
- **The over-titled hire.** The offer letter says "VP
  Engineering" for the second engineering hire, because
  the candidate asked. The title mortgages the future
  org structure — the fourth hire cannot report to
  someone who does not have visible technical work under
  their belt. Fix: title conservatively at founding-
  engineer scale ("founding engineer" is a title the
  market recognises and does not lock the future org).
- **The equity-conversation-only-once hire.** Equity is
  discussed at the offer, then never mentioned again.
  Eighteen months later the founding engineer discovers
  the dilution model, the refresh cadence, or the
  strike-price implication for the first time, and the
  conversation is awkward and defensive. Fix: an annual
  equity-and-total-comp conversation for every founding
  engineer, with the same transparency the offer
  conversation had.
- **The no-first-project hire.** New hire arrives, is
  told to "poke around", and picks up a problem three
  weeks in that turns out to have organisational context
  they were not brought into. The hire concludes the
  team is disorganised. Fix: the first-project brief is
  written before the offer letter goes out.
- **The founder-interview-that-was-actually-a-sell.** The
  founder spent 45 minutes selling the mission and never
  asked the founder-attachment questions. The candidate
  liked the sell; the founder learned nothing about the
  candidate. Fix: budget the founder interview 60/40 to
  questions vs. sell, or 70/30. There will be time for
  the sell after the offer.

## Summary

- The founding engineer profile is a **T-shaped
  generalist** with real depth in at least one area,
  where the *area* covers a gap in the founding team,
  not a duplicate. The archetypes from Will Larson's
  *Staff Engineer*
  ([staffeng.com/book](https://staffeng.com/book))
  that fit best are a **Tech Lead + Solver hybrid**.
- The **equity band** for a founding-engineer offer
  overlaps the low end of the co-founder band and is
  the compensation lever that does the most work. The
  public references — YC guidance, Carta State of
  Startup Compensation, Index Ventures Option Plan
  ([indexventures.com/optionplan](https://www.indexventures.com/optionplan/))
  — are the ones the CTO cites in the offer conversation.
  Communicate both % and implied $ value; be honest
  about dilution.
- The **founder-attachment interview** asks specific
  questions the candidate has to answer honestly: why us
  specifically, what would make you leave in six
  months, tell me about a founder disagreement, what do
  you want me to be honest about. The interviewer
  records the answers as evidence, not vibes.
- The **first project** is scoped to two weeks, load-
  bearing but not on any customer-critical path, touches
  the day-two role's real territory, and ends in a
  written artifact. Author the brief *before* the offer
  goes out.
- Failure modes to avoid: mirror-image hiring, network-
  reference-only hiring, over-titling, equity as a
  one-time conversation, missing first-project brief,
  founder interview as a sell.

The chapter's paired exercise —
[`exercise-03-founding-engineer-profile-and-first-project.md`](exercises/exercise-03-founding-engineer-profile-and-first-project.md)
— walks the authoring of the profile, the founder-
attachment interview kit, and the first-project brief.
Chapter 04 sets the team-topology context that shapes the
next hires; chapter 05 covers the promote-vs-hire
question for the first EM.
