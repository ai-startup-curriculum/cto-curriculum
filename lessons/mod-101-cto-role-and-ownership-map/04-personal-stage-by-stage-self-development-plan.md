# Personal Stage-by-Stage Self-Development Plan

## Motivation

The eight modules of this curriculum add up to 270 planned hours.
Nobody consumes them in a straight-line January-to-December pass.
The material only *lands* when you consume it against the stage
your startup is actually at — running mod-106's 15→50 transition
playbook at month 3 of pre-seed will feel unmoored (as
[`PREREQUISITES.md`](../../PREREQUISITES.md) warns), and running
mod-102's ADR chapter for the first time when you're already at
Series-A with 15 engineers is late enough to be painful.

This chapter is the sequencing rule. It maps each stage of your
startup to (a) the modules that matter *now*, (b) the modules
that will matter at the *next* stage transition, and (c) the
peer tracks and higher-level tracks that inherit the next
chapter of the ladder once this repo's coverage runs out.

The output of this chapter is a personal plan you write for
yourself — an artifact you can share with a co-founder, an
executive coach, or a mentor. The exercise
`exercise-03-personal-stage-by-stage-development-plan.md`
walks the plan authoring.

## The four buckets you are sequencing across

You are building a plan across four buckets, in decreasing
urgency:

1. **Now** — modules that address a problem you have this
   quarter. Consume these depth-first.
2. **Next transition** — modules that address the next stage
   transition (a → b, b → c, or c → d from chapter 01).
   Consume these breadth-first as background reading.
3. **Peer tracks** — modules from the sibling role-tracks
   (`cpo-curriculum`, `founder-ceo-curriculum`, etc.) that
   your co-founders / first hires / advisors should be reading
   *not you*. You are naming them so you know where to route
   questions.
4. **Higher-level tracks** — modules from `ai-infra-senior-architect`
   (level 45), `ai-infra-principal-architect` (level 55),
   `chief-ai-officer` (level 70), and `startup-exit-curriculum`
   (level 40) that will matter when you are past rung (d). You
   are *naming* them so you know what the ladder looks like
   past this repo; you are *not* studying them yet.

## Stage-by-stage sequencing

### If you are at rung (a) — technical co-founder / founding engineer, pre-seed

**Now (this quarter):**

- **This module** — locating yourself honestly on the ladder is
  a prerequisite for every other sequencing decision.
- **mod-102 (Architecture Under Uncertainty)** — every
  load-bearing architecture choice at pre-seed is being made
  under uncertainty; the ADR, C4, MonolithFirst, and evolutionary-
  architecture material lands hardest here.
- **mod-103 (Build-vs-Buy)** — the "which cloud, which auth
  vendor, which foundation-model API" decisions are all live
  at pre-seed. Get the vendor-selection scorecard and the AI-
  native stack decision framework in hand *before* you sign
  the annual commit.
- **mod-107 slice — founder-scope security posture only** —
  enough to not scare the first enterprise design partner and
  to avoid creating acquisition-risk debt.

**Next transition (before you cross into (b) at 3-5 engineers):**

- **mod-104 (First Engineering Hires)** — read the founding-
  engineer profile, interview loop, and hiring plan chapters
  before you post the first job. The material on Team Topologies
  is background reading at this rung — apply it lightly.
- **mod-106 slice — 0→5 transition only.**

**Peer tracks — your CEO / co-founder is reading:**

- Deep fundraising, cap-table, and CEO craft →
  [`founder-ceo-curriculum`](https://github.com/ai-startup-curriculum/founder-ceo-curriculum).
- Deep product discovery and pricing →
  [`cpo-curriculum`](https://github.com/ai-startup-curriculum/cpo-curriculum)
  (if you have a technical co-founder + non-technical CEO
  split; if you are wearing both hats, you may need to read a
  slice yourself).

**Higher-level tracks — not yet.**

### If you are at rung (b) — hands-on CTO, seed, 3-10 engineers

**Now:**

- **mod-104 (First Engineering Hires)** — you are living
  inside this module. Hiring plan, interview loop, first tech
  lead, and the founding-engineer profile are the day-to-day
  material.
- **mod-105 (Technical Debt as a Business Decision)** — start
  the debt portfolio *now*, not later. The Fowler-quadrant
  categorisation and cost-to-carry sizing are much cheaper to
  learn on a small codebase than a large one.
- **mod-106 (Scaling the Org and the Stack) — 0→5 and 5→15
  slices.** First tech lead, first on-call rotation, first
  blameless post-mortem, first RFC process are the milestones.
- **mod-107 — SOC 2 Type I readiness slice.** The first
  enterprise design partner will ask.

**Next transition (before you cross into (c) at ~10-15 engineers):**

- **mod-104 tail — first EM decision (promote vs. hire).**
- **mod-108 (CTO ↔ CEO / Board Communication)** — the
  decision-rights map and the board pre-read chapter start
  mattering the moment you have a seed board seat you need to
  brief.
- **mod-106 (15→50 slice) as background reading.**

**Peer tracks — your CEO / co-founder is reading:**

- CEO craft continues → `founder-ceo-curriculum`.
- The first non-founder people-ops thinking →
  [`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum).
- Product discovery → `cpo-curriculum` (still the CEO's job at
  seed unless there's a PM hire).

**Peer engineering tracks — your first hires are reading:**

- Engineering craft prerequisites →
  [`ai-infra-engineer`](../../../ai-infra-engineer-learning)
  (level 20).
- AI-native stack depth →
  [`ai-infra-mlops`](../../../ai-infra-mlops-learning)
  (level 25) if your first ML / AI engineer needs the depth.

**Higher-level tracks — not yet.**

### If you are at rung (c) — player-coach CTO, Series-A, 10-25 engineers

**Now:**

- **mod-104 (First Engineering Hires) — interview loop and
  org chart at multi-team scale.**
- **mod-106 (Scaling the Org and the Stack) — 15→50 slice.**
  This is the module for your day job.
- **mod-108 (CTO ↔ CEO / Board Communication)** — the board
  pre-read, decision-rights map, and technical due-diligence
  data room chapters. The Series-B fundraise will ask for the
  data room.
- **mod-105 (Technical Debt as a Business Decision) —
  portfolio decision-log discipline.** At this scale the
  portfolio genuinely needs discipline; without it, the
  "engineers keep asking for a rewrite" pattern will show up.
- **mod-107 — SOC 2 Type II observation window, HIPAA where
  applicable.**

**Next transition (before you cross into (d) at ~25-50 engineers):**

- **mod-106 (50→150 slice) as background reading.**
- **chapter 02 of this module (CTO vs. VP Eng vs. Chief
  Architect vs. Head of Platform)** — re-read. The splits are
  now imminent, not theoretical.

**Peer tracks — your CEO / peer executives are reading:**

- Full CEO craft → `founder-ceo-curriculum`.
- Full CPO craft → `cpo-curriculum` (there is likely a real PM
  hire by now).
- Full people-ops → `startup-operations-governance-curriculum`
  (there is likely a Head of People hire on the horizon).
- Full FP&A → `startup-finance-fundraising-curriculum` (there
  is likely a Head of Finance hire by Series-B).

**Peer engineering tracks — your first EMs / tech leads are reading:**

- Day-two engineering-management craft →
  [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (level 30).
- Staff-engineer craft for the ICs on the staff track →
  Larson's *Staff Engineer* and the
  [`ai-infra-senior-engineer`](../../../ai-infra-senior-engineer-learning)
  track.

**Higher-level tracks — begin scanning:**

- [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) — the deep architectural material that will
  matter as you cross 40-50 engineers.

### If you are at rung (d) — leadership-only CTO, Series-B+, 25+ engineers

**Now:**

- The remainder of **mod-106 (50→150 slice)** and **mod-108
  (technical due-diligence)** — this repo's last chapters.
- **Higher-level tracks — begin depth reading:**
  - [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
    (level 45) — for the multi-team architectural coherence
    problem you now own.
  - [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
    (level 55) — for the multi-region / multi-tenant depth if
    your product needs it.
  - [`chief-ai-officer`](../../../chief-ai-officer-learning)
    (level 70) — if you are the AI executive of an AI-native
    company at C-suite scale.
  - `startup-exit-curriculum` (level 40) — when M&A or exit
    conversations become concrete.

**Peer tracks — you now have peer executives at each seat.**
The tracks are their reading, not yours. Yours is knowing they
exist so you can route questions.

## Two anti-patterns to avoid

**"Read the whole thing chronologically."** This curriculum is
270 hours. Consuming it as a straight-line reading list without
matching to your stage will feel like drinking through a fire
hose and will not produce behaviour change. Consume the *Now*
bucket depth-first and the *Next* bucket as background reading.

**"Only read what applies today."** The reverse mistake. If you
are at rung (b) and never scan the 15→50 material in mod-106,
you will discover the 15→50 transition under crisis pressure.
Background-read the next transition's module even if you don't
apply it yet — one honest afternoon per quarter is enough.

## The 4-quadrant template

This is the template the `exercise-03` prompt asks you to fill
in for your own current situation:

| | This repo (`cto-curriculum`) | Peer tracks and higher-level tracks |
|---|---|---|
| **Now (this quarter)** | Modules you are consuming depth-first for a live problem | Peer-track modules your co-founder / first hires are consuming, that you are *routing* questions to |
| **Next transition** | Modules you are background-reading before the next stage transition | Higher-level-track modules you are *naming* (not yet studying) so you know what the ladder looks like past this repo |

Filling this in honestly — for your actual stage, not the stage
you wish you were at — is the load-bearing artifact of this
module.

## Cadence — re-plan when the stage shifts

The plan is not a one-time output. Re-author it whenever any of
the following change:

- Headcount crosses one of the transition thresholds (5, 15,
  50).
- Funding stage moves.
- Any of the four hats from chapter 02 (VP Eng, Chief
  Architect, Head of Platform) has been split into a
  separate hire.
- Your calendar has drifted more than one rung away from your
  stage (the A vs. B check from chapter 01).

A quarterly reminder in the CTO calendar to re-run the two-column
check from chapter 01 plus the four-quadrant template above is
usually the right cadence.

## Summary

- The 270 hours of this curriculum only land when consumed
  against the stage your startup is actually at.
- The 4-quadrant template — Now / Next × this repo / peer +
  higher-level tracks — is the plan authoring artifact.
- Peer tracks are for your *co-founders and first hires* to
  consume; you name them so you can route questions.
- Higher-level tracks are for *later*; you name them so you
  know what the ladder past this repo looks like.
- Re-author the plan quarterly and on every stage transition.

The exercise for this chapter —
`exercise-03-personal-stage-by-stage-development-plan.md` —
walks the plan authoring for your own current stage.
