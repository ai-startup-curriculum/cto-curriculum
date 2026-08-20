# mod-106 — Scaling the Org and the Stack: 0 → 5 → 15 → 50 → 150

> The four org-size transitions a startup CTO drives
> through in the first three to five years — 0→5, 5→15,
> 15→50, 50→150 — and the concrete process, platform,
> and leadership decisions each transition forces. The
> honest reckoning underneath the module: beyond ~50
> engineers the CTO's day job stops being individual
> technical decisions and becomes cross-team coordination,
> and the artifacts that survive the transitions are the
> ones designed with that shift already priced in.

**Planned time:** 22 hours (7 chapters + 7 exercises +
1 lab + 1 quiz)
**Track:** [`cto-curriculum`](../../README.md) — Co-Founder
/ CTO, level 25
**Prerequisites:** [`mod-101`](../mod-101-cto-role-and-ownership-map/README.md)
(the CTO ladder — this module extends the ownership map
across stage transitions),
[`mod-102`](../mod-102-architecture-under-uncertainty/README.md)
(the evolutionary architecture posture the stage-transition
platform decisions extend),
[`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md)
(the earn-its-keep test the "first platform team" decision
in chapter 03 reuses),
[`mod-104`](../mod-104-first-engineering-hires-and-team-topology/README.md)
(hiring plan, Team Topologies, and the first EM / tech
lead / VP Eng framing — this module is the *staging*
overlay on top of that hiring plan), and
[`mod-105`](../mod-105-technical-debt-as-business-decision/README.md)
(the debt portfolio whose aggregate cost-to-carry
manifests as the DORA four-key symptoms this module
measures).

## Learning objectives

- Navigate the **0→5 engineer transition** — the pre-
  process phase where the CTO is IC-plus-founder,
  choosing the first repo layout, branching model
  (trunk-based vs. GitFlow vs. release-train), first CI
  pipeline, first dev-environment convention, and the
  first tests that actually run in CI — with an eye to
  which choices set unrecoverable defaults for the next
  three stages.
- Navigate the **5→15 engineer transition** — the first
  tech lead, first on-call rotation, first blameless
  post-mortem, first internal RFC process, first
  product-eng planning cadence, first engineering
  handbook. The transition from *"everyone in one
  channel"* to *"someone owns each thing and there is a
  written way to change it"*.
- Navigate the **15→50 engineer transition** — the first
  engineering manager (promote-vs-hire, referencing
  [`mod-104` chapter 05](../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md)),
  the first platform team (only if the earn-its-keep
  tests from [`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md)
  pass), career ladder v1, first budget cycle, first
  offsite, and the first voluntary departure and the
  culture-loss risk it carries.
- Navigate the **50→150 engineer transition** — the
  first VP Eng or first Head of Engineering, first
  governance council, first budget re-forecast under
  investor pressure, first cross-team dependency crisis,
  and the first re-org — with the honest reckoning that
  beyond ~50 the CTO's day job stops being individual
  technical decisions and becomes cross-team
  coordination.
- Adopt the **DORA four-key metrics** — Deployment
  Frequency, Lead Time for Changes, Change Failure
  Rate, and Mean Time to Restore — as a *signal, not a
  goal*: measured, reported to the team, tied to the
  delivery-cadence rituals, and defended against the
  three failure modes (goal-ification, single-metric
  fixation, cross-team benchmarking).
- Size the **platform investment** at each transition —
  test infra, deploy infra, observability, developer
  platform — so the team's velocity does not cliff at
  15 or 50 engineers. Explicit sizing per stage,
  derived from team size and delivery cadence rather
  than borrowed from a big-tech reference architecture.
- Ship a **delivery-cadence design** — weekly planning
  rhythm, kanban vs. sprint at 5-15 engineers, on-call
  rotation at the first customer scale, blameless
  post-mortems, and an incident-response playbook — as
  a written artifact the team executes without the CTO
  in the room.
- Cite the boundary to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) and
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55) on the deep platform, distributed-systems,
  and multi-region depth that lives beyond ~50 engineers
  and belongs to a senior architect the CTO has hired,
  not to the CTO themselves.

## Chapters

1. [The 0→5 Transition — First Repo, First CI, First Tests](01-zero-to-five-first-process.md) — the pre-process phase; the four decisions (repo layout, branching model, CI pipeline, dev env) that set unrecoverable defaults; DORA-as-baseline from day one; the two failure modes (no process, premature process).
2. [The 5→15 Transition — First Tech Lead, On-Call, RFCs, Handbook](02-five-to-fifteen-first-structure.md) — the first tech lead as the CTO's first *technical* delegation; first on-call rotation at first customer scale; blameless post-mortem practice; the RFC process as the written mechanism for changing shared decisions; the engineering handbook as the artifact that survives the founder's memory.
3. [The 15→50 Transition — First EM, Platform Team, Ladder, Budget, Departure](03-fifteen-to-fifty-first-management.md) — the first engineering manager (referencing [`mod-104` ch. 05](../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md)); the first platform team subject to the earn-its-keep tests from [`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md); the career ladder v1 that lets you close the loop on promotions; the first annual budget cycle; the first offsite; the first voluntary departure and the culture-loss reckoning.
4. [The 50→150 Transition — First VP Eng, Governance, Re-Org, Coordination as Day Job](04-fifty-to-onefifty-first-scale.md) — the first VP Eng or Head of Engineering hire; the governance council that replaces ad-hoc CTO calls; the first budget re-forecast under investor pressure; the first cross-team dependency crisis; the first re-org; and the honest reckoning that the CTO's day job has stopped being individual technical decisions and become cross-team coordination.
5. [DORA Four Keys as Signal, Not Goal](05-dora-four-keys-as-signal.md) — Deployment Frequency, Lead Time for Changes, Change Failure Rate, MTTR — the definitions from the DORA program and *Accelerate*; the elite/high/medium/low bands as a *situating* tool not a target; the three failure modes (goal-ification per Goodhart's Law, single-metric fixation, cross-team benchmarking); the ritual that ties the numbers to the delivery cadence.
6. [Platform Investment Sizing per Stage](06-platform-investment-sizing.md) — the four platform categories (test infra, deploy infra, observability, developer platform); the sizing heuristic per stage (0-5 / 5-15 / 15-50 / 50-150); why the platform team should not exist until the earn-its-keep tests pass; the deferral to `ai-infra-senior-architect` for the depth beyond ~50 engineers.
7. [Delivery Cadence, On-Call, and Incident Response](07-delivery-cadence-and-on-call.md) — the weekly rhythm; kanban vs. sprint at 5-15 engineers; the on-call rotation as it evolves from "the CTO's phone" to a follow-the-sun structure; the blameless post-mortem template (SRE book / Etsy); the incident-response playbook; the ritual that closes the loop from an incident back to the debt portfolio and the DORA numbers.

## Exercises

1. [Zero-to-Five First Process Drill](exercises/exercise-01-zero-to-five-first-process-drill.md) — ~2 hours. Author the four foundational decisions for a 0-5 team (repo layout, branching model, CI pipeline, dev-env convention) as a short ADR-per-decision set in the working repo, with the reason each choice will still make sense at 15 engineers.
2. [Five-to-Fifteen Transition Playbook](exercises/exercise-02-five-to-fifteen-transition-playbook.md) — ~3 hours. Author the six-artifact playbook (tech-lead role charter, on-call rotation v1, blameless post-mortem template, RFC process doc, planning-cadence spec, engineering handbook v0 outline) as a single `docs/eng-handbook/` sub-tree.
3. [Fifteen-to-Fifty — First EM and Platform Team](exercises/exercise-03-fifteen-to-fifty-first-em-and-platform-team.md) — ~3 hours. Author the first-EM role charter (promote-vs-hire decision explicit), the earn-its-keep test result for the first platform team, the career ladder v1 (three levels minimum), and the first-annual-budget outline.
4. [Fifty-to-Onefifty — First VP Eng Transition](exercises/exercise-04-fifty-to-onefifty-first-vp-eng-transition.md) — ~3 hours. Author the VP Eng or Head of Eng job spec, the governance-council charter, the first re-org proposal (or explicit non-re-org rationale), and the CTO-role delta memo that names what the CTO stops doing when the VP arrives.
5. [DORA Four-Key Measurement Plan](exercises/exercise-05-dora-four-key-measurement-plan.md) — ~2 hours. A measurement plan for each of the four keys (data source, collection frequency, reporting cadence, the-team-owns-the-number ritual), with an explicit anti-goal-ification section (how you will prevent the numbers becoming targets).
6. [Platform Investment Sizing per Stage](exercises/exercise-06-platform-investment-sizing-per-stage.md) — ~3 hours. Size the four platform categories (test infra, deploy infra, observability, developer platform) at each of the four stages (0-5 / 5-15 / 15-50 / 50-150), with per-stage investment rationale, the earn-its-keep test result, and the deferral list to `ai-infra-senior-architect`.
7. [Delivery Cadence and On-Call Design](exercises/exercise-07-delivery-cadence-and-on-call-design.md) — ~3 hours. A delivery-cadence spec (weekly rhythm, planning cadence, kanban-vs-sprint call), an on-call rotation v1 (page path, escalation, comp), a blameless post-mortem template, and an incident-response playbook — as a single `docs/on-call/` sub-tree in the working repo.

## Lab

- `lab-01-publish-a-stage-transition-runbook`
  (~2 hours) — planned. Turns the four stage-transition
  playbooks from exercises 01-04 into a durable
  `docs/scaling/` runbook in the working repo, with the
  cross-references to the DORA measurement plan
  (exercise 05), the platform-investment sizing
  (exercise 06), and the delivery-cadence design
  (exercise 07). Sets up the quarterly re-read as a
  standing calendar hold so the runbook does not
  degrade into a one-time deliverable.

## Quiz

- One quiz (~30 min) covering: the four stage
  transitions and their decision triggers; the two
  failure modes at each stage (no process /
  premature process, too-late lead / too-senior lead,
  premature platform team / velocity cliff, ad-hoc
  coordination / premature re-org); the DORA four-key
  definitions, the elite/high/medium/low bands, and
  the three failure modes of DORA as a KPI; the four
  platform-investment categories and the earn-its-
  keep test; the delivery-cadence spec elements
  (planning rhythm, kanban vs. sprint threshold,
  on-call rotation, blameless post-mortem template);
  the CTO-role delta at ~50 engineers and the
  boundary to
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
[`mod-107`](../mod-107-founder-scope-security-and-compliance)
(*Founder-Scope Security, Privacy, and Compliance*) is
the natural next module — the on-call rotation, the
incident-response playbook, and the blameless post-mortem
practice from this module are the operational substrate
the SOC 2 Type I readiness checks rely on.
[`mod-108`](../mod-108-cto-ceo-and-board-communication)
(*The CTO↔CEO Relationship, Board Communication, and
Technical Due Diligence*) is where the DORA numbers, the
delivery-cadence spec, and the stage-transition runbook
land in the board pre-read and the technical-DD data
room.

This module feeds directly into the capstone
[`project-103`](../../projects/project-103-scaling-plan-from-five-to-fifty-engineers)
(the 5→15→40 scaling plan), whose stage-transition
sections are authored in the format this module
establishes.
