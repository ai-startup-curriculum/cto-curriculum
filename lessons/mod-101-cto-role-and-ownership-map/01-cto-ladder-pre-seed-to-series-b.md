# The CTO Ladder — Pre-Seed to Series-B+

> "The job of a CTO is whatever the company needs it to be. That doesn't sound
> like a useful answer — but it's the only accurate one." — paraphrase of the
> line Charity Majors returns to repeatedly in *What is a CTO?*
> ([charity.wtf](https://charity.wtf/2019/09/16/wtf-is-a-cto-anyway/))

## Motivation

"CTO" is a single title covering four very different jobs. A technical
co-founder ten weeks after incorporation is doing almost nothing that
overlaps with a Series-B CTO of a 60-engineer org, and yet both people are
called "CTO" on their LinkedIn. If you conflate them, you either (a) act
like a hands-off executive when your company still needs you to ship the
build system this weekend, or (b) keep writing production code when your
company needs you to hire two engineering managers this quarter.

This module — and this chapter in particular — exists so you can locate
yourself, your company, and your next stage transition on the ladder
honestly, and choose the modules of this curriculum that actually apply
*now* rather than three stages from now.

## The four rungs

The rungs below are the archetype the rest of this curriculum uses. They
map to the funding-stage vocabulary from
[`startup-foundations`](https://github.com/ai-startup-curriculum/startup-foundations)
(`IDEA → PRE-SEED → SEED → SERIES-A → GROWTH → MATURE`). Every rung
description below states (i) headcount, (ii) what the CTO's calendar looks
like, (iii) what the CTO is on the hook for that a peer role isn't, and
(iv) the honest failure mode of that rung.

### (a) Technical co-founder / founding engineer — pre-seed

- **Headcount** — 1 to 3 engineers total, and the CTO is one of them.
- **Calendar** — >70% individual contributor time. The CTO writes the
  first line of production code, chooses the first framework, wires the
  first CI job, and takes the first support ticket.
- **On the hook for** — shipping the MVP to the first paying design
  partner, being the technical half of the fundraising pitch, and making
  every load-bearing architecture choice (see mod-102) knowing that
  product-market fit is still unproven.
- **Failure mode** — behaving like an executive. There is no one else to
  hand the ticket to. If you spend the week reading engineering-management
  books instead of merging PRs, the MVP slips and the runway shortens.
- **Curriculum focus** — this module, mod-102 (architecture under
  uncertainty), mod-103 (build-vs-buy at the level of "which auth vendor,
  which cloud, which foundation-model API"), mod-107 slice on the
  founder-scope security posture that does not scare off the first
  enterprise design partner.

### (b) Hands-on CTO — seed, 3 to 10 engineers

- **Headcount** — the founding engineer(s), plus 2-8 hires. Still no
  formal management layer.
- **Calendar** — ~50/50 IC and non-IC. Half the week is still code review,
  incident response, and technical decision-making; the other half is
  interviewing candidates, running the weekly planning rhythm, and being
  the technical partner to the CEO on the seed-to-Series-A story.
- **On the hook for** — the first tech lead (promote-vs-hire), the first
  on-call rotation, the first blameless post-mortem, the first RFC
  process, and the first hiring-plan-vs-runway conversation with the CEO
  and the seed board.
- **Failure mode** — the founder-CTO who keeps every technical decision
  routed through themselves. At 3 engineers this is fine; at 8 it becomes
  the bottleneck the whole team routes around.
- **Curriculum focus** — mod-104 (first hires + Team Topologies at
  5-engineer scale), mod-105 (starting the technical-debt portfolio
  early — see Fowler's original piece on the debt metaphor before it
  becomes a crisis), mod-106 slice on the 0→5 and 5→15 transitions,
  mod-107 for the SOC 2 Type I readiness the first enterprise design
  partner will ask about.

### (c) Player-coach CTO — Series-A, 10 to 25 engineers

- **Headcount** — 10-25 engineers, one or two engineering managers or
  tech leads, possibly a first platform engineer.
- **Calendar** — <30% IC. The bulk of the week is 1:1s with EMs / tech
  leads, cross-team planning, architecture review, hiring, and board
  work. IC time is usually a fixed slot ("Friday afternoons I merge PRs")
  or a specific initiative the CTO is deliberately keeping their hands on
  (a new platform decision, a security-sensitive change, a spike).
- **On the hook for** — the first VP Eng or Head of Engineering
  decision (see chapter 02 on when this is a separate hire), the
  15→50 org transition (see mod-106), Team Topologies at multi-team
  scale, the technical due-diligence data room for Series-B, and the
  CTO ↔ CEO decision-rights map (mod-108).
- **Failure mode** — clinging to the IC identity. The pendulum here
  swings hard: some CTOs at this rung effectively demote themselves back
  to staff engineer because coding is the part of the job they still
  enjoy, leaving the org headless on people, process, and platform
  decisions.
- **Curriculum focus** — mod-104 (interview loop, first EM), mod-106
  (15→50 transition, DORA measurement), mod-108 (board and CEO
  communication), and the tail of mod-107 (SOC 2 Type II observation
  window, HIPAA where applicable).

### (d) Leadership-only CTO — Series-B+, 25 engineers and up

- **Headcount** — 25 to 150+ engineers, a full engineering-management
  layer, potentially a VP Eng peer.
- **Calendar** — effectively 0% IC. The job is engineering-org design,
  technical strategy, cross-executive coordination (CTO ↔ CEO ↔ CPO ↔ CFO),
  external technical narrative (customers, analysts, press), and
  M&A / partnership technical evaluation.
- **On the hook for** — the org shape beyond ~50 engineers, technical
  strategy at the multi-quarter horizon, hiring the next tier of
  engineering leadership, and being the technical voice at the board.
- **Failure mode** — losing the technical altitude that made the CTO
  useful in the first place. This is where the *Engineer/Manager
  Pendulum* (Majors) becomes a career-shape question: some Series-B
  CTOs deliberately swing back to a staff-engineer or founder-in-residence
  seat rather than sitting in the leadership-only rung indefinitely.
- **Curriculum focus** — most of this curriculum has already been
  consumed by rung (d). This is the stage where deep architectural,
  principal-engineer, and executive scope defers *up* to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45),
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55), and
  [`chief-ai-officer`](../../../chief-ai-officer-learning) (level 70),
  and where exit / M&A work defers to `startup-exit-curriculum`
  (level 40). See chapter 04 for the sequencing.

## How to locate yourself on the ladder

Two things confuse the self-assessment. Both are worth naming.

**Confusion 1 — title inflation vs. stage reality.** A pre-seed technical
co-founder with the LinkedIn title "CTO and co-founder" is doing rung
(a) work. The title is a signal to investors and future hires, not a
description of the current job. Read your own rung off your calendar and
your org chart, not off your title.

**Confusion 2 — the "wrong rung for the stage" pathology.** Sometimes
the CTO is at rung (a) but the company is at Series-A: this is what
Ben Horowitz's *The Hard Thing About Hard Things* discusses under the
label of "founder-CEO who has not scaled" — except applied to the CTO
seat. The person shipping code at Series-A while 15 engineers wait for
architectural direction is not being helpful; they are being the
bottleneck. The reverse also happens — a hands-off executive at pre-seed
who cannot merge a PR is likewise mis-matched.

The two-column check that surfaces both pathologies:

| Column A — what the company needs at its stage | Column B — what your calendar / calendar-optional artifacts (Slack, PR history, GitHub activity) actually show |
|---|---|
| (write the rung the company is at from headcount + funding) | (write the rung your last 4 weeks of work would suggest) |

If A and B differ by more than one rung, the mismatch is the most
important thing to fix this quarter — usually before any of the other
mod-102 / mod-103 / mod-104 material starts landing.

## The stage-transition moments this curriculum is organised around

The rungs above are not evenly spaced. The three transitions between them
are the moments this curriculum's later modules are pointed at:

- **(a) → (b) at 3-5 engineers** — first non-founder hires, first
  hiring-plan conversation with a lead investor, first "the CTO cannot
  code everything themselves anymore" realisation. Covered by mod-104
  and the 0→5 slice of mod-106.
- **(b) → (c) at ~10-15 engineers** — first management layer (promote
  vs. hire), first platform-vs-stream-aligned tension, first "the CTO's
  calendar is 40% meetings whether they like it or not" realisation.
  Covered by mod-104, mod-106, and mod-108.
- **(c) → (d) at ~25-50 engineers** — first VP Eng (or first Head of
  Platform / first Chief Architect — see chapter 02 for when these are
  separate hires), first engineering-org re-design, first "the CTO is
  no longer the fastest technical decision-maker in every room"
  realisation. Covered by mod-106, mod-108, and — for the depth
  beyond this level — the higher-level tracks named in chapter 04.

## Summary

- Four rungs — technical co-founder (pre-seed), hands-on CTO (seed),
  player-coach CTO (Series-A), leadership-only CTO (Series-B+). Same
  title, four different jobs.
- Locate yourself against **calendar + org chart**, not against title.
- The A vs. B two-column check surfaces the "wrong rung for the stage"
  pathology — the pre-seed technical co-founder acting like an
  executive, or the Series-A CTO still trying to be the fastest
  IC on the team.
- The three transitions between rungs are where the rest of this
  curriculum's modules are pointed. Which ones matter *now* vs.
  *at the next transition* is the subject of chapter 04.

The exercise for this chapter — `exercise-01-cto-ladder-self-assessment.md`
— walks the two-column check for your own current situation.
