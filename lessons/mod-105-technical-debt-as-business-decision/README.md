# mod-105 — Technical Debt as a Business Decision

> How the pre-seed / seed / Series-A CTO turns a
> pile of *"the engineers keep asking for a rewrite"*
> conversations into a **six-item portfolio**, a
> **carry cost**, and a **per-item plan** a board
> member or an incoming VP Eng can read on day one —
> instead of a permanent political fight between
> feature work and refactor work that neither side
> wins.

**Planned time:** 16 hours (6 chapters + 5 exercises +
1 lab + 1 quiz)
**Track:** [`cto-curriculum`](../../README.md) — Co-Founder
/ CTO, level 25
**Prerequisites:** [`mod-101`](../mod-101-cto-role-and-ownership-map/README.md)
(the CTO ladder and the shared reading vocabulary that
the debt conversation runs on top of),
[`mod-102`](../mod-102-architecture-under-uncertainty/README.md)
(especially chapter 04 on ISO/IEC 25010 quality-
attribute trade-offs — the vocabulary this module's
quality-attribute-debt family reuses, and chapter 01 on
the evolutionary / monolith-first posture the debt
metaphor lives inside), and
[`mod-104`](../mod-104-first-engineering-hires-and-team-topology/README.md)
(the hiring plan and the topology the refactor budget
interacts with — every debt item's depreciation curve
is a function of team size, and every rewrite has a
staffing consequence).

## Learning objectives

- Categorise technical debt using **Fowler's
  quadrants** (Deliberate vs. Inadvertent × Prudent
  vs. Reckless) and **Ward Cunningham's original
  financial-debt metaphor** — as portfolio
  management, not moral failing.
- Distinguish **quality-attribute debt** (reliability /
  performance / security / maintainability
  regressions per ISO/IEC 25010:2023) from
  **structural debt** (architecture misfit, wrong
  abstraction, coupling, missing seam).
- Size the **cost-to-carry** — engineering-hours per
  week spent working around a piece of debt — and
  the **depreciation schedule** — how the cost-to-
  carry compounds as the codebase and team grow
  (team-size / codebase-size / turnover / adjacent-
  decision compounders).
- Allocate a **defensible refactor budget** (the
  "20% rule" as one shape, not a law), *derived
  from* the portfolio's aggregate carry cost, and
  tied explicitly to the roadmap — so the debt work
  has a **business owner**, not just an engineering
  owner.
- Choose between three responses per debt item —
  **Deprecate** the feature, **Rewrite** (with a
  Chesterton's-Fence check + StranglerFig
  incremental replacement), or **Leave** it and pay
  the carry cost — and defend the choice on business
  terms.
- Author a **technical-debt inventory** and a
  **portfolio decision log** a board member or an
  incoming VP Eng can read — the format that turns
  *"the engineers keep asking for a rewrite"* into
  *"here's the six-item portfolio, here's the carry
  cost, here's the plan for each item, here's the
  two items that need your sign-off, here's the four
  we're just handling."*
- Cite the boundary to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) and
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55) on the *technical* mechanics of large
  refactors and system extractions at post-Series-B
  scale — the pre-Series-A CTO recognises them,
  labels them in the inventory, and does not attempt
  them alone.

## Chapters

1. [The Cunningham Metaphor and the Fowler Quadrants](01-cunningham-metaphor-and-fowler-quadrants.md) — Ward Cunningham's 1992 OOPSLA framing of debt as a *deliberate* financial instrument (principal / interest / repayment / default) and Martin Fowler's 2009 2×2 (Deliberate-Prudent, Deliberate-Reckless, Inadvertent-Prudent, Inadvertent-Reckless); why debt is portfolio management, not moral failing.
2. [Quality-Attribute Debt vs. Structural Debt](02-quality-attribute-vs-structural-debt.md) — the two families of debt (ISO/IEC 25010 quality-attribute regressions vs. domain-shape structural misfit), why they have different fix costs and different responses, and the two edge cases (quality-attribute regression that is actually structural; structural debt that is actually a business pivot).
3. [Cost-to-Carry and the Depreciation Schedule](03-cost-to-carry-and-depreciation-schedule.md) — the six sources of cost-to-carry (workaround, on-call, onboarding, lead-time per DORA, feature-slip, morale/attrition), the median-of-three protocol, the four compounders that make the interest rate rise (team-size, codebase-size, turnover, adjacent-decision), and the two things NOT to publish (dollar figures, precise fix-ROI).
4. [The Refactor Budget Tied to the Roadmap](04-refactor-budget-tied-to-roadmap.md) — deriving the budget from the portfolio math rather than importing a number; why the "20% rule" is a shape not a law; why every line item needs a **business owner** who is not the CTO; the two artifacts the budget is authored against (roadmap, hiring plan); why it is a *rate* not a *project*.
5. [Deprecate, Rewrite, or Leave — the Three Responses](05-deprecate-rewrite-or-leave.md) — the five-question decision tree; why *Deprecate* is the cheapest-and-most-underused response; the Chesterton's Fence check that must pass before any rewrite; the StranglerFig pattern for incremental, reversible rewrites (never big-bang); the discipline of *Leave* as a time-boxed, explicit-carry-cost choice; the boundary to `ai-infra-senior-architect` for multi-quarter / multi-team / multi-region rewrites.
6. [The Debt Inventory and the Portfolio Decision Log](06-debt-inventory-and-portfolio-decision-log.md) — the eleven-column inventory row format; the Nygard-ADR-shape decision log with debt-specific sections (Chesterton's Fence check, business-owner sign-off, review cadence); the one-page portfolio summary the CEO cites at the board; the weekly / monthly / quarterly / annual cadence; the boundary column that names every deferral up to `ai-infra-senior-architect` (level 45) / `ai-infra-principal-architect` (level 55).

## Exercises

1. [Fowler Quadrant Categorisation Drill](exercises/exercise-01-fowler-quadrant-categorisation-drill.md) — ~2 hours. Ten real debt items categorised by Fowler quadrant AND family (with ISO/IEC 25010 characteristic or structural shape named); a two-engineer walkthrough per item; a four-paragraph diagnostic on the quadrant distribution, the family split, the categorisation surprises, and which cell is filling up.
2. [Cost-to-Carry Sizing for Five Debt Items](exercises/exercise-02-cost-to-carry-sizing-for-five-debt-items.md) — ~3 hours. Five items sized against the six sources (workaround / on-call / onboarding / lead-time / feature-slip / morale-attrition), using the median-of-three protocol; the depreciation projection with the dominant compounder named per item; a summary table with the portfolio-band label.
3. [Refactor Budget Tied to Roadmap Drill](exercises/exercise-03-refactor-budget-tied-to-roadmap-drill.md) — ~3 hours. Next-quarter budget as a percentage of engineering time, *derived* from the portfolio's aggregate carry-cost plus the planned principal repayment; per-item allocation with named business owners; the roadmap trade-offs (feature moves, hiring-plan interactions) the budget forces; a 150-300 word board-facing paragraph.
4. [Deprecate vs. Rewrite vs. Leave Decision Drill](exercises/exercise-04-deprecate-vs-rewrite-vs-leave-decision-drill.md) — ~3 hours. Five items walked through chapter 05's five-question decision tree; per-item response memos with Chesterton's Fence check for rewrites, StranglerFig migration sketch for rewrites, sunset schedule for deprecations, explicit carry cost + revisit date for leaves; a roll-up paragraph on response mix, least-sure-item, and the item needing CEO sign-off.
5. [Technical Debt Inventory Authoring](exercises/exercise-05-technical-debt-inventory-authoring.md) — ~3 hours. The full inventory (6-12 rows in the chapter 06 eleven-column format), one sample decision-log entry in the Nygard-ADR-plus-debt-sections shape, and the one-page portfolio summary the CEO drops into the board pre-read. The capstone artifact of the module.

## Lab

- `lab-01-publish-a-technical-debt-portfolio-decision-log`
  (~2 hours) — planned. Turns the exercise-05
  inventory + decision log into a durable, versioned,
  quarterly-reviewed artifact in the working repo:
  the `docs/tech-debt/` directory with the inventory,
  the decision-log directory, the README with cadence
  stated, and a scheduled quarterly review calendar
  invite. Also stands up the monthly-with-CEO and
  quarterly-with-board review shape so the artifact
  does not degrade into a one-time deliverable.

## Quiz

- One quiz (~30 min) covering: the Fowler quadrant
  vocabulary and the four-cell distribution's
  diagnostic reading; the quality-attribute vs.
  structural family split and the two edge cases; the
  six sources of cost-to-carry and the four
  compounders in the depreciation schedule; the
  refactor-budget derivation and the "20% is a shape,
  not a law" framing; the five-question deprecate-vs-
  rewrite-vs-leave decision tree; the Chesterton's
  Fence check and the StranglerFig pattern; the
  eleven-column inventory row and the Nygard-ADR-
  shape decision log; the boundary to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  and
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning).

## Resources

See [`resources.md`](resources.md) for the module's
primary references. Full citations for the whole
curriculum are in
[`.aicg/job-requirements.json`](../../.aicg/job-requirements.json)
under `authoritative_references`.

## What comes next

Once you have completed the exercises here,
[`mod-106`](../mod-106-scaling-org-and-stack)
(*Scaling the Org and the Stack: 0 → 5 → 15 → 50 →
150*) is the natural next module — the debt portfolio
becomes an input to the stage-transition playbooks,
and DORA metrics (Deployment Frequency, Lead Time,
Change Failure Rate, MTTR) become the org-level
symptoms the debt portfolio's aggregate cost-to-carry
manifests as.
[`mod-108`](../mod-108-cto-ceo-and-board-communication)
(*The CTO↔CEO Relationship, Board Communication, and
Technical Due Diligence*) is where the one-page
portfolio summary from this module lands in the board
pre-read and the technical-DD data room.

This module also feeds directly into the capstones
[`project-102`](../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package)
(the SOC 2 Type I + compliance-debt package, which
reuses the inventory format for the security /
compliance debt slice) and
[`project-103`](../../projects/project-103-scaling-plan-from-five-to-fifty-engineers)
(the 5-to-40 scaling plan, whose debt-portfolio
section uses this module's inventory format across
the four planned stages).
