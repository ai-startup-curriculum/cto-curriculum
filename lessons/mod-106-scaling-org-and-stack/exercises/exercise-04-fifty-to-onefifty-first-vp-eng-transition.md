# Exercise 04 — Fifty-to-Onefifty: First VP Eng Transition

**Module:** `mod-106-scaling-org-and-stack`
**Planned time:** ~3 hours
**Chapter this builds on:** [`04-fifty-to-onefifty-first-scale.md`](../04-fifty-to-onefifty-first-scale.md),
supported by [`mod-104` chapter 05 on VP Eng
promote-vs-hire](../../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md),
[`mod-102` chapter 02 on the ADR discipline](../../mod-102-architecture-under-uncertainty/README.md),
and [`mod-108`](../../mod-108-cto-ceo-and-board-communication/README.md)
for the CTO/CEO conversation shape that the CTO-role
delta memo lands into.

## Problem statement

Author the **four 50-to-150 executive-infrastructure
artifacts** as a `docs/scaling/50-to-150/` sub-tree in
the working repo:

1. **VP Eng (or Head of Engineering) job specification**
   — one to two pages.
2. **Governance-council charter** — one page (plus a
   short members / rotation file and a decision-log
   convention).
3. **First re-org proposal** — one to two pages, OR an
   explicit **non-re-org rationale** if the honest
   answer is "the boundaries still fit".
4. **CTO-role delta memo** — one page. What the CTO
   stops doing when the VP arrives, what the CTO
   starts doing, and what they do together.

The purpose is to force the CTO to make the four 50-to-
150 executive-infrastructure decisions *in writing*, in
the format the CEO, the board, the incoming VP, and
the engineering org can read on day one of the
transition. Every one of these artifacts has a
well-documented failure mode (chapter 04) that the
exercise is designed to surface — the VP who is hired
but never handed the job, the council that becomes a
bottleneck, the re-org that becomes an annual ritual,
the CTO who works eighty-hour weeks because they
never re-negotiated their own job.

## Requirements

Directory shape:

```
docs/scaling/50-to-150/
  README.md                 # index across the four artifacts
  vp-eng-job-spec.md        # artifact 1
  governance-council/
    README.md               # charter (artifact 2)
    members.md              # named members and rotation
    decision-log/
      README.md             # decision-log convention (empty archive)
  re-org-proposal.md        # artifact 3 (proposal OR non-re-org rationale)
  cto-role-delta.md         # artifact 4
```

### Artifact 1 — VP Eng job specification

`vp-eng-job-spec.md` — one to two pages. Sections:

- **Title and level.** VP Eng, Head of Engineering, SVP
  Eng, or Director of Engineering. Name the specific
  title and the reason (see chapter 04 on the vocabulary
  distinction). Comp band and level should be reference-
  able against the career-ladder v1 from
  [exercise 03](exercise-03-fifteen-to-fifty-first-em-and-platform-team.md).
- **Reports to.** Named — usually the CTO, sometimes
  the CEO. Chapter 04 assumes CTO. If your rationale
  is CEO, name why.
- **Scope of ownership.** 5-8 bullet points. Cover: the
  EM tier reporting into the VP, the delivery cadence
  at the engineering-org level, the hiring pipeline
  ownership, the operational-execution interface with
  the CEO, the on-call / incident-response executive
  ownership, the engineering budget execution
  (planning is CTO+VP+CFO, execution is VP).
- **Success criteria at 90 / 180 / 365 days.** 3-5
  bullets per checkpoint. Concrete and measurable
  where possible. Read Lara Hogan's *"first 90 days"*
  playbook at
  [larahogan.me](https://larahogan.me/) as a shape
  reference; do not import wholesale.
- **Promote-vs-hire decision.** A paragraph naming the
  decision and the reasoning against the two-column
  checklist in
  [`mod-104` chapter 05](../../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md).
  If promoting, name the internal candidate (or the
  profile), the ramp-plan, and the peers who will
  need to shift interaction shape. If hiring, name
  the target-company / target-title bands, the
  search timeline, the interim plan, and the search
  firm (or the reason you are not using one).
- **What the VP is NOT.** 3-5 bullets. Cover: the
  CTO (they are peers on execution vs. strategy),
  the CEO's chief-of-staff, a technical-decision
  authority above the ARB (see artifact 2), a
  replacement for the CTO (unless that is the
  deliberate path — see chapter 04's transition-out
  note and defer to
  [`mod-108`](../../mod-108-cto-ceo-and-board-communication/README.md)
  for the CEO conversation shape).
- **References** — Camille Fournier — *The Manager's
  Path* CTO / VP-Eng chapters
  ([oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/));
  Will Larson — *An Elegant Puzzle* on executive
  work ([lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/));
  the *Staff Engineer* companion at
  [staffeng.com/book](https://staffeng.com/book) for
  the IC-tier counterpart shape.

### Artifact 2 — Governance-council charter

`governance-council/README.md` — one page. Sections:

- **Purpose.** One paragraph on why the council exists
  (the ad-hoc-CTO-call substrate from chapter 04
  artifact 2). Name the two shapes — ARB / architecture
  guild and technical steering committee — and pick
  one shape (or explicitly both) for your first
  council.
- **Scope of decisions.** 4-6 bullets on what the
  council decides on. Cross-team architecture
  proposals; shared-infrastructure changes;
  security-standard changes; platform-team charters.
  Name the *out-of-scope* explicitly (individual-team
  technical decisions, individual hiring decisions,
  engineering-budget allocation).
- **Decision rights.** *Decide with a written
  exception path for the CTO to override*, or
  *recommend, CTO decides*. Chapter 04's default is
  *decide-with-CTO-override*. Name your choice and
  defend it in one paragraph. Reference the Amazon
  *disagree and commit* framing at
  [aws.amazon.com/executive-insights/content/leadership-principles-have-backbone-disagree-and-commit](https://aws.amazon.com/executive-insights/content/leadership-principles-have-backbone-disagree-and-commit/).
- **Cadence and format.** Weekly or every-other-week
  meeting, 60-90 minutes. Async-review-first rule:
  RFCs (see [exercise 02 artifact 4](exercise-02-five-to-fifteen-transition-playbook.md))
  are reviewed async in the RFC repo, and the
  meeting only discusses items someone has flagged
  for discussion. Otherwise the council becomes a
  bottleneck (chapter 04 failure mode 1).
- **Decision log.** Points at
  `governance-council/decision-log/`. One file per
  decision, Nygard-ADR-shape (see
  [`mod-102` chapter 02](../../mod-102-architecture-under-uncertainty/README.md)),
  publicly searchable.
- **Public-vs-private.** The default is *public* — the
  discussion, the rationale, and the decision are
  posted to the engineering org. Name any
  well-scoped exception (people-related items,
  security-sensitive items).

`governance-council/members.md` — one page:

- **Standing seats.** CTO and VP Eng (both
  permanent). Head of Product (if the council reaches
  into product-technical decisions).
- **Rotating seats.** 3-5 senior engineers (staff or
  principal). Name them, and name the rotation
  cycle (chapter 04 default: 6-12 months).
- **Ex-officio / invited.** Security lead, platform-
  team lead, other domain leads pulled in for
  specific items.
- **Quorum and voting.** How many need to attend for
  a decision to stand. How ties are broken (usually
  the CTO's override path).

`governance-council/decision-log/README.md` — a short
convention document:

- File naming — `YYYY-MM-DD-short-slug.md`.
- One paragraph on the Nygard-ADR shape (context /
  decision / consequences / status).
- A note on cross-linking — every decision links back
  to the RFC or ARB proposal it resolves.

### Artifact 3 — First re-org proposal (or non-re-org rationale)

`re-org-proposal.md` — one to two pages. **You author
one or the other; both paths are valid.**

**If your working-repo scenario has 50-150 engineers
and a real re-org trigger** (a stream-aligned team
that has grown past 10-12 engineers; a capability
that crosses three teams and needs its own team; a
misalignment between team boundaries and the
dependency map), author the re-org proposal:

- **The trigger.** Named. One paragraph on the
  specific signal — from the dependency map, the
  team-size threshold, the recurring cross-team
  crisis — that motivated the proposal.
- **The current state.** Team names, sizes, reporting
  lines, and the primary work each team owns
  (borrow from the org-chart artifact in
  [`mod-104` chapter 06](../../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md)).
- **The proposed state.** Named. New team names,
  sizes, and reporting lines. The Team-Topologies
  vocabulary
  ([teamtopologies.com](https://teamtopologies.com/))
  — stream-aligned, enabling, complicated-subsystem,
  platform — should be visible in the naming. Draw
  the before/after as a simple ASCII / mermaid diagram
  if useful.
- **What changes for each affected engineer.** Named
  by role (not necessarily by person if the exercise
  is a reference scenario). Who moves teams? Who
  changes managers? Who takes on a new tech-lead
  role or gives one up?
- **Announcement plan.** The written document that
  will be posted to the eng org, the timing
  (usually paired with a Q-planning cycle), the
  1:1s that happen before the announcement, the
  all-hands agenda. Cite Larson's *An Elegant Puzzle*
  ([lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/))
  on re-org mechanics.
- **Settling period.** The quarter (minimum) after
  which the re-org will be assessed. Name the
  criteria — dependency-map conflicts resolved,
  team-level DORA numbers within their prior band,
  no attrition traceable to the re-org.
- **The rolling-adjustment alternative.** One
  paragraph on why a bigger single re-org is the
  right call here rather than the rolling
  team-boundary adjustments chapter 04 usually
  prefers. If you cannot write this paragraph
  honestly, the answer is probably rolling
  adjustments — see the non-re-org rationale.

**If your working-repo scenario does NOT have a real
re-org trigger**, author the **non-re-org rationale**
in the same file. Sections:

- **The trigger you would need to see.** What signal
  would move you to propose a re-org? Cite the
  dependency map (chapter 04 artifact 4), the
  team-size thresholds, or a specific class of
  recurring cross-team crisis.
- **Why the current shape still fits.** One paragraph
  against the same Team-Topologies vocabulary.
- **The rolling adjustments already underway.** The
  smaller team-boundary changes — a service moved
  between teams, a tech-lead swapped, a hiring plan
  weighted toward one team — that are absorbing the
  pressure that would otherwise force a re-org.
- **The re-check date.** Concrete — a quarterly or
  half-yearly check to re-evaluate. If your
  non-re-org rationale is *"we might need one
  eventually"*, name when you will look again.

Both paths are valid; the exercise's discipline is
that you have made and written down the decision,
not that you have proposed a re-org.

### Artifact 4 — CTO-role delta memo

`cto-role-delta.md` — one page. This is the memo
chapter 04 calls the *CTO / VP boundary memo*, plus
the CTO-role delta — read together as the CTO's
honest re-negotiation of their own job. Sections:

- **What the CTO STOPS doing.** 5-8 bullets. Cover:
  primary technical decision-making on a specific
  slice (delegated to the tech leads and the ARB);
  primary management of any engineer below the VP
  tier (delegated to the VP and the EMs); chairing
  the weekly engineering staff meeting (delegated to
  the VP); direct 1:1s with every EM (drops to the
  VP tier plus deliberate skip-levels); the initial
  hiring-loop coordination (delegated to the VP and
  the recruiting partner).
- **What the CTO STARTS doing.** 5-8 bullets. Cover:
  primary owner of company-wide technical strategy;
  primary interface to the board on technical
  questions (see
  [`mod-108`](../../mod-108-cto-ceo-and-board-communication/README.md));
  three-year technical direction ownership;
  make-vs-buy calls at the platform-team level;
  build-vs-hire calls at the leadership level;
  external technical narrative (developer relations,
  hiring brand, industry-conference presence at the
  CTO level).
- **What the CTO and VP do TOGETHER.** 4-6 bullets.
  Cover: hiring senior-IC and EM roles; the
  quarterly planning readout to the CEO; the
  annual engineering budget (planning is joint,
  execution is VP-owned); post-mortem review for
  the largest incidents; the technical-narrative
  slice of the board pre-read.
- **The CTO / VP interaction cadence.** 1:1 weekly
  (60 minutes). A shared decision-log or planning
  doc that both maintain. An explicit escalation
  path for the VP when they need the CTO's
  arbitration.
- **The failure-mode watchlist.** 3-4 bullets on
  the anti-patterns the memo is guarding against:
  the CTO who hires a VP and keeps doing the VP
  job informally (chapter 04); the CTO who
  disappears from technical decisions entirely
  and leaves the VP with no strategic cover; the
  VP who is treated as a subordinate rather than
  a peer.
- **Re-negotiation cadence.** When the memo itself
  will be revisited — usually at 6 months and 12
  months after the VP starts.

## Starter guidance

- **The VP-Eng job spec should feel like a real
  job posting, not a role description.** Would a
  senior VP Eng at another company read it and want
  to apply? If not, the scope and success criteria
  are probably too generic. Read three or four
  current VP-Eng postings from companies in your
  stage / domain before authoring, and mine them
  for the shape of the "what you will do in the
  first 90 days" section.
- **The promote-vs-hire decision must be defended
  against the checklist, not against a preference.**
  See [`mod-104` chapter 05](../../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md).
  *"They have been here a long time"* is not a
  promote signal; *"they have already been operating
  at VP scope for two quarters, the team follows
  them, and the CEO trusts them"* is. Same on the
  hire side — *"we want outside experience"* is not
  a hire signal; *"we need a specific competence
  nobody internal has and cannot ramp into in the
  timeframe"* is.
- **The governance council's cadence should default
  to less-often, not more-often.** A weekly council
  that has nothing on the agenda in three of every
  four weeks trains the org to treat the council
  as noise. Every-other-week with a clear
  async-first rule is often the right first shape;
  scale up to weekly if the queue grows.
- **The decision-log convention is load-bearing.**
  Without it, the council decides in the meeting
  and nobody outside the room hears about it — the
  chapter 04 failure mode 2. The convention should
  be one paragraph, easy to follow. If the
  convention is complicated, nobody will follow it
  and the decisions will not be logged.
- **The re-org proposal is where CTOs over-reach.**
  A re-org that redraws every team boundary in one
  quarter costs the org a full quarter of settling
  time. If your proposal touches more than 30-40%
  of the reporting lines in one shot, sit with the
  rolling-adjustment alternative for another day
  before authoring. Read Larson's chapter on
  organisational debt at
  [lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/)
  before deciding.
- **The non-re-org rationale is a valid deliverable.**
  If every 50-to-150 exercise instance ended in
  *"yes, re-org proposed"*, the discipline is not
  real. The exercise is checking that you have made
  the decision honestly, not that you have proposed
  a re-org. Chapter 04's *annual re-org as a
  ritual* is the anti-pattern.
- **The CTO-role delta memo is where the exercise
  most-often stalls.** The stops-doing list is
  uncomfortable to write because it names things
  the CTO has been holding for the previous three
  years. Write the list anyway — the memo is the
  artifact that lets the transition happen. Read
  the CTO chapter of *The Manager's Path*
  ([oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/))
  before authoring; it is the load-bearing
  reference on what the CTO job actually is at this
  stage.

## Acceptance criteria

Your drill output is complete when:

- The `docs/scaling/50-to-150/` directory contains
  the four artifacts in the shape above.
- The VP Eng job spec names a specific title / level,
  a promote-vs-hire decision with reasoning against
  the [`mod-104` ch. 05](../../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md)
  checklist, and 90 / 180 / 365-day success criteria
  that are concrete and measurable where possible.
- The governance-council charter names decision
  rights (decide-with-override OR recommend), a
  cadence with an async-first rule, and a
  decision-log convention. The `members.md` names
  standing and rotating seats and a rotation cycle.
- The re-org proposal OR the non-re-org rationale
  names a trigger, references Team Topologies
  vocabulary, and names a settling period (or a
  re-check date). If a proposal, it references the
  rolling-adjustment alternative and defends the
  bigger re-org against it.
- The CTO-role delta memo names 5-8
  stops-doing items, 5-8 starts-doing items, 4-6
  done-together items, and a re-negotiation
  cadence. The stops-doing list is uncomfortable
  to write; if yours is not, revise.
- All four artifacts cross-reference each other:
  the VP spec references the governance council;
  the governance-council charter references the
  CTO-role delta; the re-org proposal references
  the VP's ownership of the new structure.
- The four artifacts together can be handed to the
  new VP on their first day, plus posted to the
  engineering org, without a follow-up round of
  ambiguity-resolution Slack threads.

## What this feeds into

- **Exercise 05** — the DORA measurement plan is
  the substrate the VP inherits at the
  engineering-org level; the per-team dashboards
  from the 50-150 ritual (chapter 05) are the VP's
  weekly reading.
- **Exercise 06** — the platform-investment sizing
  at 50-150 is the substrate the governance
  council authorises platform-team charters
  against.
- **Exercise 07** — the delivery-cadence and
  on-call design at 50-150 (per-team rotation,
  follow-the-sun, incident-command system) is the
  operational substrate the VP owns.
- **The lab** — the four artifacts are the 50-to-
  150 slice of the `docs/scaling/` runbook, and
  the CTO-role delta memo is the durable
  substrate for the mod-108 board-communication
  work.

The 50-to-150 exercise is where the CTO writes down
the honest re-negotiation of their own job. If any
of the four artifacts feels like *"the VP can figure
this out once they arrive"*, the exercise has not
yet forced the discipline; go back and finish it
before moving to exercise 05. The VP who arrives
without these four artifacts in hand spends the
first quarter reverse-engineering them from the
CTO, and the transition stalls.
