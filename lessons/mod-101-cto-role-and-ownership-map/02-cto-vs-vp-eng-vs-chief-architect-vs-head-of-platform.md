# CTO vs. VP Engineering vs. Chief Architect vs. Head of Platform

## Motivation

At pre-seed and early seed, the CTO owns all four jobs below.
Somewhere between the first EM hire and Series-B, most of them start
to split off into separate people. Which one splits off first — and
when — is one of the most consequential org-shape decisions the CTO
will make. Getting it wrong burns a hire, a quarter, and often a
co-founder relationship.

The industry has published enough noise on "what a CTO is" that the
distinctions have become blurry. This chapter uses the definitions
Camille Fournier draws in *The Manager's Path* (CTO chapter,
[O'Reilly](https://www.oreilly.com/library/view/the-managers-path/9781491973882/))
and Will Larson draws in *An Elegant Puzzle* and *Staff Engineer*
([lethain.com](https://lethain.com/), [staffeng.com](https://staffeng.com/))
because those are the definitions the rest of this curriculum builds
on.

## The four roles, side by side

| Role | Primary loop | Owns | Does *not* own by default |
|---|---|---|---|
| **CTO** | Technical strategy ↔ business strategy | Where the technology is going, why it matters to the business, how it de-risks the fundraising story | Day-to-day delivery of features; deep architectural depth at scale |
| **VP Engineering** | People + delivery | Hiring, performance, career ladders, on-call, delivery cadence, engineering-org happiness, DORA-flavoured delivery signals | External technical narrative; deep architectural authority |
| **Chief Architect** | System design across teams | Cross-team architectural coherence, standards, ADR review, technical fitness functions | People management; hiring plan; delivery cadence |
| **Head of Platform** | Internal developer platform | The platform team charter, self-service tooling, developer-experience investment, platform-vs-stream-aligned boundary | External technical narrative; product-facing engineering delivery |

None of these are mutually exclusive at pre-seed. The founding CTO
is playing all four hats. The question is *when the hats separate*.

## When each role earns its own seat

### The VP Engineering split

The VP Eng is usually the **first** split. It happens when:

- Headcount is roughly 20-30 engineers and 2-4 EMs report up through
  the CTO. The CTO's calendar is now dominated by 1:1s, performance
  conversations, and hiring-loop calibrations they are not enjoying
  and are not the best at.
- The CEO is asking for a technical partner who can also carry
  external narrative — investor updates, customer executive
  briefings, analyst calls — and the CTO cannot do both that and
  the internal people-management job.
- The engineering-org's DORA signals or attrition are drifting and
  no one owns the delivery-cadence remediation full-time.

The VP Eng typically owns hiring, performance management, delivery
cadence (see mod-106), and on-call. The CTO retains external
technical narrative, board / investor work, technical strategy,
and — if the CTO is still in the *player-coach* rung — some
architectural authority.

Camille Fournier's chapter is explicit that this split is *not*
demotion in either direction — VP Eng is not "junior CTO" and CTO
is not "senior VP Eng". The two seats are two different jobs and
the healthiest orgs treat them as peers reporting to the CEO.

### The Chief Architect split

The Chief Architect (or **Principal Architect**, or the *Staff+
architect archetype* from Larson's *Staff Engineer*) is usually
the **second** split, and it splits from the *CTO* seat rather
than from the VP Eng seat. It happens when:

- The engineering org has grown past ~40-60 engineers with 4+
  teams making architectural decisions in parallel, and no single
  person has the load bandwidth to keep them coherent.
- The stack has grown past what any one person can hold in their
  head — multiple persistence stores, multiple deploy targets,
  cross-cutting concerns like auth, billing, or the ML platform
  that need a single owner.
- The CTO is no longer the fastest technical decision-maker in
  every room and — critically — knows it.

The Chief Architect owns cross-team architectural coherence,
standards, the ADR-review lane (see mod-102), and technical
fitness functions from *Building Evolutionary Architectures*
(Ford, Parsons, Kua). They do **not** own people management,
hiring plan, or delivery cadence — those stay with VP Eng.

Note: the *title* varies. Some orgs use "Chief Architect", some
use "Principal Engineer", some use "Distinguished Engineer", and
some — following Larson's *Staff Engineer* archetypes — use
"Staff Engineer, Architect archetype". The distinction that
matters is *individual-contributor at the highest technical
altitude, cross-team scope, no direct reports*.

Below the ~40-60 engineer scale the Chief Architect role usually
lives inside the CTO seat, not as a separate person. Hiring a
Chief Architect too early is a common early-scale mistake — see
the "when NOT to split" section below.

### The Head of Platform split

The Head of Platform is usually the **third** split. It happens
when the platform team crosses the Team Topologies "earn its keep"
test (Skelton & Pais, [teamtopologies.com](https://teamtopologies.com/book))
— which typically requires roughly 15-25 engineers in the wider
org so that a 2-4 person platform team is unblocking enough
stream-aligned teams to justify its own cost.

The Head of Platform owns:

- The platform team charter — what the platform team is / is not
  responsible for.
- Internal-developer-experience investment — self-service tooling,
  CI/CD ergonomics, deploy-and-rollback UX, observability defaults.
- The platform-vs-stream-aligned boundary — resisting the drift
  where the platform team becomes a shared-services team that
  every stream-aligned team throws work over the wall to.

They do **not** own external technical narrative, hiring plan for
non-platform engineers, or cross-team architectural coherence
(that belongs to the Chief Architect if the split has happened,
otherwise to the CTO).

Below the platform-earn-its-keep threshold, "Head of Platform" is
a role a stream-aligned tech lead wears part-time on a rotating
basis. Making it a full-time role too early creates the classic
anti-pattern where the platform team ships internal-tooling
features that no one asks for while the stream-aligned teams
route around it.

## When the CTO is still doing all four jobs

At pre-seed and early seed — the (a) and (b) rungs from chapter 01
— the CTO **is** the VP Eng, the Chief Architect, and the Head of
Platform, because there is no one else. Three important consequences:

1. The CTO's calendar in this stage will feel schizophrenic —
   Monday is architecture, Tuesday is a hiring loop, Wednesday is
   a production incident, Thursday is a board pre-read, Friday is
   catching up on the code that has drifted while all of the
   above was happening. This is normal. It is not a signal that
   the CTO is failing — it is a signal that the company has not
   yet grown into the split.
2. The CTO must be honest about which of the four jobs they are
   *worst* at, because that is the one the org will pay for first.
   A CTO whose weakest hat is people management should be
   preparing the ground for a VP Eng hire before the wheels come
   off attrition or delivery cadence — even if that hire is still
   two quarters away.
3. Documenting the split *in advance* — even as an aspirational
   org chart 12-18 months out — is a mod-104 exercise (see also
   the mod-108 chapter on the CTO ↔ CEO decision-rights map).
   The alternative is discovering the split under crisis
   pressure, which is much more expensive.

## When *not* to split

Two common early-scale mistakes:

### Hiring a VP Eng too early

Below ~15 engineers, a VP Eng often has too little to do. The
result is one of two failure modes: (i) the VP Eng invents
process the org does not need yet, adding meeting overhead and
slowing delivery; or (ii) the VP Eng drifts into IC work,
becoming a very expensive senior engineer whose title now
blocks the actual first-EM promotion path.

The signal that the split is *ready* is usually: 2-4 EMs or
tech leads already reporting to the CTO, and the CTO is
consistently the constraint on hiring-loop throughput or
performance-management follow-through.

### Hiring a Chief Architect too early

Below ~30-40 engineers with fewer than ~3 teams, the Chief
Architect has too few decisions to arbitrate and can slow the
whole org down by inserting a review lane where none was needed.
The signal that the split is ready is usually: multiple teams
are making architectural decisions in parallel that other teams
have to live with, and there is no single ADR-review lane that
keeps them coherent (see mod-102).

Below this scale, the *pattern* the Chief Architect brings —
ADRs, C4 diagrams, fitness functions — belongs to the CTO's
own workflow. It is the *dedicated seat* for that pattern that
is premature, not the pattern itself.

### Hiring a Head of Platform without stream-aligned teams to serve

The Team Topologies test is that a platform team exists to
reduce cognitive load on stream-aligned teams. If there are
only 1-2 stream-aligned teams, the cognitive-load saving does
not justify the platform team's cost, and the platform team
inevitably starts inventing work.

Below this threshold, platform work is a rotating slice of the
stream-aligned tech leads' calendars, coordinated by the CTO.

## Summary

- Four roles, three splits: VP Eng first (~20-30 engineers),
  Chief Architect second (~40-60 engineers), Head of Platform
  third (typically after ~15-25 engineers, gated by the Team
  Topologies "earn its keep" test).
- At pre-seed and early seed, the CTO is playing all four hats.
  This is normal, not a failure signal.
- Splitting a role too early is more expensive than splitting it
  slightly late — a premature split adds a hire with too little
  to do who then creates work to justify the seat.
- The CTO should know, honestly, which of the four hats they are
  *worst* at, and prepare the split-hire ground for that one
  first.

The exercise for this chapter —
`exercise-02-cto-vs-vp-eng-vs-chief-architect-decision-drill.md`
— walks a set of ambiguous cases and asks which role owns each
decision, forcing an explicit split judgement.
