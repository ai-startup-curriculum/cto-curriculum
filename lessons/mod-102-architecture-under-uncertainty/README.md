# mod-102 — Architecture Under Uncertainty

> How to make load-bearing architectural decisions at a stage
> when product-market fit is still unproven, every component
> must remain cheap to change, and no one on the team has
> earned the right to be sure yet.

**Planned time:** 20 hours (6 chapters + 6 exercises + 1 lab +
1 quiz)
**Track:** [`cto-curriculum`](../../README.md) — Co-Founder /
CTO, level 25
**Prerequisites:** [`mod-101`](../mod-101-cto-role-and-ownership-map/README.md)
(especially chapter 05 on the shared reading vocabulary), and
the engineering-craft prerequisites in
[`PREREQUISITES.md`](../../PREREQUISITES.md).

## Learning objectives

- Design a startup's first architecture with the working
  assumption that product-market fit is unproven and every
  load-bearing component must remain cheap to change —
  MonolithFirst, StranglerFig-later, and evolutionary
  architecture with explicit fitness functions.
- Author Architecture Decision Records (ADRs, Nygard) as the
  primary technical-strategy artifact — one per meaningful
  decision, versioned in the repo, referenced from the
  roadmap.
- Diagram the system with the C4 model (System Context →
  Container → Component → Code) at the depth stakeholders
  actually consume — an investor / board member reads the
  System Context diagram, a new engineer reads Container and
  Component.
- Reason about non-functional trade-offs (ISO/IEC 25010
  quality attributes — reliability, performance, security,
  maintainability, portability, and their peers) explicitly
  rather than by default, and document the trade-off in the
  ADR.
- Choose between monolith / modular monolith / service
  extraction as a *staged* decision — not a religious one;
  understand the CAP theorem and eventual-consistency
  vocabulary well enough to defend the persistence choice
  in an ADR and to a technical due-diligence reviewer.
- Use spikes and time-boxed experiments as the primary
  risk-reduction mechanism when architecture is uncertain —
  with an explicit success / kill criterion agreed *before*
  the spike starts.
- Cite the boundary to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) and
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55) on the deep multi-region / multi-tenant /
  high-scale architectural depth that lives above this
  level.

## Chapters

1. [MonolithFirst and Evolutionary Architecture](01-monolith-first-and-evolutionary-architecture.md) — the default architecture at pre-seed / seed, and why *cheap to change* beats *right first time*.
2. [Architecture Decision Records — the Primary Strategy Artifact](02-adrs-the-primary-strategy-artifact.md) — Nygard-style ADRs, one per meaningful decision, versioned in the repo.
3. [The C4 Model at Stakeholder-Appropriate Depth](03-c4-model-at-stakeholder-appropriate-depth.md) — System Context → Container → Component → Code, and who reads which.
4. [ISO/IEC 25010 Quality-Attribute Trade-offs](04-iso-25010-quality-attribute-trade-offs.md) — non-functional requirements as explicit choices, documented in the ADR.
5. [Monolith → Modular Monolith → Services, and the CAP Vocabulary](05-monolith-modular-monolith-services-and-cap.md) — the staged extraction decision and the persistence-model trade-off.
6. [Spikes with Kill Criteria — Risk-Reduction under Uncertainty](06-spikes-and-kill-criteria.md) — time-boxed experiments as the primary tool when the ADR is not yet writable.

## Exercises

1. [Monolith First vs. Services Decision Drill](exercises/exercise-01-monolith-first-vs-services-decision-drill.md) — ~2 hours. Six ambiguous starting-architecture scenarios; explicit monolith / modular monolith / services call for each, with the trade-off named.
2. [ADR Authoring for Three Real Decisions](exercises/exercise-02-adr-authoring-for-three-real-decisions.md) — ~3 hours. Author three Nygard-format ADRs for real decisions your (or a real reference) startup faces this quarter.
3. [C4 Diagram Set for One Startup](exercises/exercise-03-c4-diagram-set-for-one-startup.md) — ~3 hours. System Context + Container + Component diagrams for one startup, at the depth each stakeholder audience actually consumes.
4. [ISO/IEC 25010 Quality-Attribute Trade-off Map](exercises/exercise-04-iso-25010-quality-attribute-trade-off-map.md) — ~2 hours. Rank the ISO/IEC 25010 characteristics for your startup and identify the two you are actively trading away.
5. [Evolutionary-Architecture Fitness-Function Drill](exercises/exercise-05-evolutionary-architecture-fitness-function-drill.md) — ~2 hours. Three executable fitness functions that guard the load-bearing invariants you can't afford to lose.
6. [Spike Charter and Kill Criteria](exercises/exercise-06-spike-charter-and-kill-criteria.md) — ~2 hours. Author a one-page spike charter for a real open architectural question, including the kill criterion.

## Lab

- `lab-01-architecture-package-for-your-startup` (~3 hours) —
  planned. Bundles the C4 diagrams (exercise 03), the three
  ADRs (exercise 02), and the trade-off map (exercise 04)
  into a single reviewable *architecture package* the CTO
  can walk a technical advisor, a first engineering hire, or
  a technical due-diligence reviewer through. Scaffold this
  lab from the exercise outputs once the paired prompt is
  authored.

## Quiz

- One quiz (~1 hour) covering: MonolithFirst and the
  StranglerFig pattern, the four ADR sections, the four C4
  levels and their audiences, the eight ISO/IEC 25010
  quality characteristics, the CAP theorem statement, and
  the shape of a well-formed spike charter.

## Resources

See [`resources.md`](resources.md) for the module's primary
references. Full citations for the whole curriculum are in
[`.aicg/job-requirements.json`](../../.aicg/job-requirements.json)
under `authoritative_references`.

## What comes next

Once you have completed the exercises here, mod-103
(*Build-vs-Buy, Vendor Selection, and Platform Economics*)
is the natural next module — every ADR you author in this
module has a build-vs-buy component (which auth vendor, which
cloud, which foundation-model API), and mod-103 is where the
economics side of that trade-off is worked. The three ADRs
from exercise 02 and the trade-off map from exercise 04 both
feed directly into mod-103's vendor-selection scorecard.
