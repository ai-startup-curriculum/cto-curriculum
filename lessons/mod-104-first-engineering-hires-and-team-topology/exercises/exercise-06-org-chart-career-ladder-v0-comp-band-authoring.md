# Exercise 06 — Org Chart, Career-Ladder v0, and Comp-Band Authoring

**Module:** `mod-104-first-engineering-hires-and-team-topology`
**Planned time:** ~3.5 hours
**Chapter this builds on:** [`06-org-chart-career-ladder-and-comp-band.md`](../06-org-chart-career-ladder-and-comp-band.md)

## Problem statement

Author the **three artifacts** that chapter 06 names —
the **org chart**, the **career-ladder v0**, and the
**compensation band** — for your (or a real reference)
startup, wired together as a single reviewable package
that a first-round investor's technical due-diligence
reviewer could read in fifteen minutes.

The point of the drill is not to draft polished HR
paperwork. It is to force the CTO to make the specific
decisions the artifacts *encode* — who reports to whom
at your current stage, what "senior" actually means on
your team, and what the company pays a level 2 engineer
in your target geography — and to have written them
down before the first calibration cycle, the first
compensation-review conversation, or the first
technical-DD reviewer forces the question.

## Requirements

Produce **three files** in a `docs/org/` directory (or
the equivalent in your repo), cross-linked from a
short `docs/org/README.md` index:

- `docs/org/org-chart.md` — the one-page org chart.
- `docs/org/career-ladder-v0.md` — the ladder v0.
- `docs/org/comp-band.md` — the compensation band.

Every file has a **version and date** at the top and a
`Next review:` date one to twelve months out per
chapter 06's re-run rhythm. A v0 without a version and
a review cadence is a v0 that will not survive contact
with the next stage transition.

### Artifact 1 — the org chart

Author a **one-page** org chart, Mermaid or ASCII (do
not use an HR-tool export; chapter 06 is direct on
why). It must show, for the *current* headcount at your
startup:

- Every current person, by role — names OK if the file
  is internal-only; otherwise archetypes ("Senior FE
  engineer #1"). Do **not** include personally
  identifying information in a file that will be shared
  beyond a private founder audience.
- Every open requisition from your exercise 01 hiring
  plan, marked `TBD — <role>`, positioned in the team
  it will join.
- The reporting lines — including the CTO's own direct
  reports, and any temporary reporting lines (an
  enabling engineer embedded with a stream-aligned
  team, an IC on a temporary rotation).
- The **team-type label** for each team — stream-
  aligned / platform / enabling / complicated-subsystem
  — per exercise 04's topology map. If your exercise 04
  output covers three stages, this file uses the stage
  closest to your *current* headcount as the canonical
  chart, and links to the 15 / 25 diagrams as
  successors.
- The **version and date** in the header. A chart
  without a version is one nobody trusts is current.

Below the diagram, write a **short caption paragraph**
(100-200 words) that answers:

- Which topology stage (from exercise 04) does this
  chart correspond to?
- Which reporting line is the one you are *least sure
  about* — and what would tell you it is wrong?
- Where does the CTO's own IC time land on the chart —
  named team, or "player-coach across teams"?

### Artifact 2 — the career-ladder v0

Author a **ladder v0** with **two tracks** — engineering
IC and engineering management — and **three or four
levels per track** (chapter 06's compression bar). More
levels at v0 is over-fitting; fewer than three is
under-specified.

For each level on each track, fill in the **four
dimensions** with **two-to-four short behavioural
anchors** each:

- **Scope** — how large is the surface this person
  owns? How ambiguous can the surface be?
- **Impact** — the size of outcome this level is
  responsible for.
- **Behaviour** — how they work with others; mentoring,
  feedback, disagreement, collaboration.
- **Craft** — technical depth expected (IC track) or
  management craft expected (EM track).

**Anchors must reference your actual systems and
teams.** Chapter 06's guidance is that copying anchors
from a public ladder produces a document that describes
a company you are not. Do not copy the anchors from
[Rent the Runway](https://dresscode.renttherunway.com/blog/ladder),
[CircleCI](https://github.com/circleci/engineering-competency-matrix),
or any of the ladders on
[progression.fyi](https://www.progression.fyi/); read at
least two of them *for structure*, then rewrite the
anchors against the subsystems and product surfaces
your team actually has.

**Explicit "v0" header.** The file must open with a
statement of what the ladder is and is not — v0, not
final; expected rewrite at the first-EM trigger, and
again at Series-B; describes what levels *are* and not
what an individual engineer must accomplish to be
promoted; maps to but is not the same as the
compensation band. Chapter 06's "what the ladder v0 is
*not*" list is the source for this section.

### Artifact 3 — the compensation band

Author the compensation band for the levels in your
ladder v0, with:

- **Base salary band** — low / mid / high per level,
  per geography tier (or as a single number if you have
  a location-independent policy). Publish the tier
  definition or the location-independent policy
  explicitly.
- **Equity grant band** — low / mid / high per level,
  expressed as **percent of the current cap table**
  (with the current-round implied dollar value included
  as a *snapshot*, not a promise).
- **Non-cash benefits band** — the health plan tier,
  the 401(k) match rate, the parental leave policy, the
  equipment budget. A single canonical description per
  band — not a bullet per benefit copied from the
  vendor.
- **Geography rule** — explicitly *one* of:
  location-adjusted (with tier definition) or location-
  independent. "We'll negotiate per candidate" is *not*
  a geography rule and is the failure mode chapter 06
  is written against.
- **Reference footnote** — cite the public references
  the band is calibrated against. At minimum:
  [Levels.fyi](https://www.levels.fyi/), the [Index
  Ventures Option Plan](https://www.indexventures.com/optionplan/),
  and either [Pave](https://www.pave.com/) (if you or
  your People lead subscribes) or the [Carta State of
  Startup Compensation](https://carta.com/blog/) posts
  for equity bands by stage.

**Do not invent numbers you cannot verify.** If your
company has not benchmarked against a paid survey yet,
mark the affected cells `<comp: pending Pave / Radford
benchmark; using Levels.fyi seed row as placeholder>`
and cite the placeholder. Chapter 06's failure mode
"the comp band without a geography rule" and the
sibling failure mode "the comp band with fabricated
numbers" both start with a CTO who guessed rather than
annotated.

### The index — `docs/org/README.md`

A short (200-400 word) file that:

- Links to the three artifacts.
- Names the **stage transition** that will trigger the
  v0 → v1 rewrite of the ladder, per chapter 06 (first-
  EM trigger, VP-Eng trigger, Series-B).
- Names the **hand-off boundary** to the two peer
  tracks: [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (day-two management craft) and
  [`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum)
  (People pillar). State explicitly what the CTO owns
  in these files, and what the two peer tracks own that
  the CTO consumes.
- Names the **annual re-run rhythm** for each artifact
  — org chart at every topology change, ladder at every
  calibration cycle (~6 months) and at each stage
  transition, comp band annually and at each material
  hiring-plan shift.
- Includes the two-sentence answer to the meta-question
  below.

### The meta-question

At the bottom of the index file, answer in 200-400
words:

- Which of the three artifacts was **hardest to write
  down**, and why? (Common honest answers: "the ladder,
  because we don't have a shared vocabulary yet"; "the
  comp band, because I don't want the team to see the
  low end of the range".)
- Which failure mode from chapter 06 is your v0 **most
  susceptible to** — the unwritten ladder, the copied
  ladder, the geography-free comp band, the untrusted
  org chart, or the v0-that-was-v-final? Name the one,
  and name the specific counter-measure you built into
  the artifact against it.
- Which line in your ladder v0 do you expect to **argue
  hardest about** in the first calibration cycle
  (typically 6 months out)? Name it now, so future-you
  is not surprised.

## Starter guidance

- **Read at least two public ladders for structure —
  do not copy anchors.** The starting set:
  [progression.fyi](https://www.progression.fyi/),
  [Rent the Runway](https://dresscode.renttherunway.com/blog/ladder)
  (Camille Fournier's open-sourced ladder — the one
  *The Manager's Path* references), and the [CircleCI
  Engineering Competency Matrix](https://github.com/circleci/engineering-competency-matrix).
  Structure travels; anchors do not.
- **Wire the three artifacts together.** The org chart
  references the ladder for level (the "Senior FE
  engineer" node on the chart is a specific level on
  the ladder); the ladder references the comp band per
  level; the comp band references the geography of the
  ladder's assumed employees. A package where the three
  artifacts don't reference each other is three
  documents, not a package.
- **Cross-link the topology (exercise 04) and the plan
  (exercise 01).** The org chart's teams are exercise
  04's teams; the open requisitions on the org chart
  are exercise 01's plan rows. If the chart and the
  plan disagree, one is wrong; do not paper over the
  disagreement.
- **Cross-link the first-EM decision (exercise 05).**
  If the promote-vs-hire memo landed on "promote", the
  org chart must show the promoted person in the EM
  role and note the change to their IC responsibilities.
  If it landed on "hire", the chart shows the open EM
  requisition with a `TBD` name and a hiring-manager
  attribution.
- **Publish the comp band internally.** Chapter 06 is
  direct: a band that is only ever quoted as the
  outcome of a negotiation does not do the equity work
  a band is supposed to do. Note in the file whether
  the band is (a) fully published to the team, (b)
  shared with a specific audience (the founding team +
  first EM), or (c) still CTO-only — and if it is not
  (a), name the trigger that would move it to (a).
- **Name what you consume from the peer tracks.** The
  boundary sentences from chapter 06 are the specific
  language:
  [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (level 30) for day-two management craft (1:1s,
  feedback, performance-management, difficult
  conversations); [`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum)
  (People pillar) for HR / people-ops / compensation
  depth. Do not re-teach either.
- **Do not invent numbers.** If a comp cell needs a
  benchmark you have not run, annotate the cell and
  leave a placeholder — the annotation is the artifact,
  not the guess.
- **Cite the readings.** At minimum: Fournier's *The
  Manager's Path*
  ([oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/))
  for the ladder-as-artifact framing; Larson's *Staff
  Engineer* ([staffeng.com/book](https://staffeng.com/book))
  for the L3 IC-track archetypes; and the Index
  Ventures Option Plan
  ([indexventures.com/optionplan](https://www.indexventures.com/optionplan/))
  for the equity band.

## Acceptance criteria

Your three-artifact package is complete when a reader
(co-founder, first EM, first-round investor's
technical-DD reviewer) can, in **fifteen minutes**:

- Look at the **org chart** and know every person's
  team and reporting line, the open requisitions, and
  the team-type labels. See a version and a date.
- Read the **ladder v0** and see, for every level on
  both tracks, what the level *is* on scope / impact /
  behaviour / craft — with anchors that reference *your*
  systems, not somebody else's. See the explicit "v0,
  expected rewrite at <trigger>" header.
- Read the **compensation band** and see, per level and
  per geography tier (or per the location-independent
  policy), a base range, an equity range, and a
  benefits summary. See at least three cited public
  references and any placeholder annotations.
- Read the **index** and see the three artifacts
  cross-linked, the annual re-run rhythm named, and the
  boundary to the two peer tracks
  ([`ai-infra-team-lead`](../../../ai-infra-team-lead-learning),
  [`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum))
  stated explicitly.
- Read the **meta-question** answer and see that the
  CTO has identified where the v0 is weakest and the
  failure mode it is most susceptible to.

The package is not complete if:

- The three artifacts do not reference each other
  (three documents, not a package).
- The ladder's anchors are pasted from a public
  reference (a copied ladder, per chapter 06).
- The comp band has no geography rule ("we'll negotiate
  per candidate" is the failure mode).
- The org chart shows people but no team-type labels
  and no open requisitions.
- The index does not name a review cadence for each
  artifact.

The output of this exercise is one of the six
artifacts bundled by the module lab
(`lab-01-first-year-hiring-and-org-package-for-your-startup`)
and is a load-bearing artifact in both capstones
[`project-101`](../../../projects/project-101-first-year-technical-strategy-for-one-seed-startup)
(the first-year technical-strategy package) and
[`project-103`](../../../projects/project-103-scaling-plan-from-five-to-fifty-engineers)
(the 5 → 50 scaling plan, which uses this v0 as the
baseline the 50-engineer ladder is a rewrite of).
