# Exercise 04 — Team Topologies Mapping for Three Stages

**Module:** `mod-104-first-engineering-hires-and-team-topology`
**Planned time:** ~2.5 hours
**Chapter this builds on:** [`04-team-topologies-at-startup-scale.md`](../04-team-topologies-at-startup-scale.md)

## Problem statement

Draw **three team-topology diagrams** for your (or a
real reference) startup — one at **5 engineers**, one
at **15 engineers**, one at **25 engineers** — with
each team labelled by its Team Topologies type
(**stream-aligned**, **platform**, **enabling**,
**complicated-subsystem**) and each pair of teams
labelled by its interaction mode (**Collaboration**,
**X-as-a-Service**, **Facilitating**).

The point is not to guess your future org shape
perfectly. It is to force yourself to reason about the
*shape* of the org at each stage before you make the
next specific hire, and to notice where the current
plan (exercise 01) would produce a topology that
Conway's-Laws itself into a shape the roadmap does not
want.

## Requirements

Produce a `docs/org/topology-map.md` (or the equivalent
in your repo) with three sections — one per stage —
and a short **transitions paragraph** between the
sections.

### For each stage (5, 15, 25):

- A **diagram** — Mermaid, ASCII, or an embedded
  image — that shows every team, every team's
  members-count, every team's type label, and every
  inter-team relationship.
- A **team-by-team table** with columns:
  - `Team name` — a descriptive noun the team would
    use itself.
  - `Type` — stream-aligned / platform / enabling /
    complicated-subsystem.
  - `Members (count + composition)` — e.g. "4
    engineers: 1 EM, 1 tech lead, 2 senior ICs".
  - `Owns` — a one-line description of what this
    team ships end-to-end.
  - `Does not own` — a one-line note on the
    responsibility this team is often mistakenly
    handed, and where it actually belongs.
  - `Interaction with` — a list of the other teams
    at this stage and the interaction mode for each
    pair.
- A **short justification paragraph** (100-200
  words) on:
  - Why *this* shape at this stage — anchored in
    chapter 04's guidance.
  - Why *not* the alternative shape you rejected
    (e.g. "why not a platform team at 15?").
  - The **cognitive-load check** — is any single
    team above ~8 people? Any tech lead / EM with
    more than 8 direct reports? If so, name the
    split you would make.

### The transitions paragraph

Between the 5→15 and the 15→25 stages, write a
**200-400 word transitions paragraph** each. Each
transition paragraph must answer:

- **What is the trigger** that moves the org from
  the earlier shape to the later shape? — a
  headcount threshold, a topology cognitive-load
  signal (per chapter 04), a specific hire, a
  specific product launch.
- **What is the *first* topology change** — is it a
  team split, an enabling role, a new tech lead, or
  the creation of the platform team?
- **What could go wrong** — one specific failure
  mode from chapter 04 that this transition is
  particularly susceptible to, and how you would
  detect it.

### Cross-links required

- Link each stream-aligned team to the customer
  segment or product surface it serves.
- Link the platform team (at 25) to the specific
  stream-aligned teams that would pull from it.
  Name the first three capabilities you would
  expect stream-aligned teams to voluntarily adopt
  — the "earning its keep" signal from chapter 04.
- If a **complicated-subsystem team** appears
  earlier than 25 (e.g. for AI-native startups with
  an ML pipeline as moat — see the chapter-04
  section on this), name the subsystem and the
  interface it exposes.

## Starter guidance

- **Do not use the technical-layer split.** "Front-
  end team" and "back-end team" is Conway's Law
  writing your architecture. Split along product /
  customer streams so each team is end-to-end.
- **Do not create a platform team before 25.** The
  urge is real; chapter 04 walks why it fails. If
  your reasoning requires a platform team at 15,
  interrogate what capabilities you are trying to
  centralise. Usually the answer is "one enabling
  role", not "a permanent platform team".
- **Name the interaction mode for every team-pair.**
  Failing to name it defaults to Collaboration —
  which is the "everyone meets with everyone about
  everything" failure mode.
- **The enabling team is temporary by design.**
  Chapter 04's "permanent enabling team" is a
  platform team hiding — either the capability
  transfers out to stream-aligned teams (and the
  enabling team is disbanded or re-scoped) or the
  team is re-chartered as a platform team with a
  self-service surface.
- **The AI-native complicated-subsystem exception**
  applies if your moat is a specific ML pipeline
  (per [`mod-103` chapter 01](../../mod-103-build-vs-buy-and-platform-economics/01-build-vs-buy-as-portfolio-decision.md)
  "domain ML pipeline — Build" row). Note it
  explicitly.
- **The 25-engineer stage is where the platform team
  earns its keep** *only* if stream-aligned teams
  voluntarily adopt its capabilities. Name three
  specific capabilities you expect adoption of, and
  the signal that would tell you the platform is
  paying for itself.
- **The Conway's Law reference.** Cite Conway 1968
  ([melconway.com/Home/Committees_Paper.html](https://www.melconway.com/Home/Committees_Paper.html))
  when justifying the topology's shape against the
  intended architecture. Reference the *Team
  Topologies* book ([teamtopologies.com/book](https://teamtopologies.com/book))
  for the vocabulary.
- **Diagrams should be one page each.** If your
  15-engineer diagram is spilling to two pages, you
  are drawing an HR org chart, not a topology map.
  The topology map shows *teams* (usually 2-6 at
  this scale), not people.

## Acceptance criteria

The topology map is complete when:

- A reader can compare the three stages side by
  side and see the *evolution* of the org shape —
  which team split, when the platform team appears,
  when the first EM lands, when a complicated
  subsystem is broken out.
- Every team at every stage is labelled by type and
  has an owns / does-not-own line.
- Every team-pair has a named interaction mode
  (Collaboration / X-as-a-Service / Facilitating).
- The cognitive-load check at each stage is
  answered — no single team above ~8, no single
  lead with more than ~8 direct reports, and where
  the check fails you have named the split.
- The 5→15 and 15→25 transition paragraphs each
  answer the trigger / first change / failure-mode
  questions from the Requirements section.
- The 25-engineer diagram names the platform team's
  first three expected capabilities and the earning-
  its-keep signal.
- If your product has an AI-native complicated
  subsystem, it appears in the diagrams and its
  interface is named.

The output of this exercise feeds directly into:

- Exercise 01 — the topology tells you which team
  each hire in the plan belongs to.
- Exercise 05 — the topology tells you when the
  first EM / first tech lead / first VP Eng
  triggers actually fire.
- Exercise 06 — the topology is one of the three
  artifacts (org chart, ladder v0, comp band) that
  chapter 06's package requires.
- The lab and capstones
  [`project-101`](../../../projects/project-101-first-year-technical-strategy-for-one-seed-startup)
  and
  [`project-103`](../../../projects/project-103-scaling-plan-from-five-to-fifty-engineers).
