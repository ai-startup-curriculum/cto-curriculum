# mod-108 — The CTO↔CEO Relationship, Board Communication, and Technical Due Diligence

> The engineering-leadership craft of the *founder seat
> next to the CEO* — how the CTO and CEO share
> decisions, how the board hears about technical
> progress and technical risk, and how a technical due-
> diligence data room survives contact with a serious
> buyer or Series-B lead. The honest reckoning
> underneath the module: an unresolved cofounder
> disagreement, a board memo that hides the real risk,
> or a data room that cannot answer the buyer's
> architectural questions can each on its own kill a
> round, cost the company a discount, or end a
> founding partnership — and each is defended against
> by *artifacts that exist before the crisis*, not by
> mid-crisis diplomacy.

**Planned time:** 16 hours (7 chapters + 6 exercises +
1 lab + 1 quiz)
**Track:** [`cto-curriculum`](../../README.md) —
Co-Founder / CTO, level 25
**Prerequisites:** [`mod-101`](../mod-101-cto-role-and-ownership-map/README.md)
(the CTO ladder — the decision-rights map in chapter 01
sits on top of the ownership map from that module),
[`mod-102`](../mod-102-architecture-under-uncertainty/README.md)
(the ADR discipline the board-decision-log format
reuses; the C4 / evolutionary-architecture vocabulary
the DD architecture overview reuses),
[`mod-104`](../mod-104-first-engineering-hires-and-team-topology/README.md)
(the hiring plan the board is briefed against and the
key-person-risk register in chapter 06 draws from),
[`mod-105`](../mod-105-technical-debt-as-business-decision/README.md)
(the technical-debt portfolio the DD data room presents
and the board is briefed on), and
[`mod-107`](../mod-107-founder-scope-security-and-compliance/README.md)
(the security-posture packet that lands directly in the
technical-DD data room in chapter 04 and is a recurring
board pre-read line item from chapter 03).

## Learning objectives

- Design a **synchronised decision cadence** with the
  CEO — a weekly 1:1 with a stable agenda, a decision-
  rights map that names who decides what (unilaterally,
  with input, or by consensus), an explicit tie-breaker
  mechanism, and an escalation path to the board or a
  board observer.
- Establish a **cofounder-dispute mechanic before you
  need it** — vesting, decision-tie-breaker, a cofounder-
  relationship agreement, and a mediation route — and
  know that legal opinion on any of the underlying
  instruments (equity, vesting, IP assignment, voting
  agreements) is routed to counsel rather than
  authored by the CTO.
- **Brief the board on technical progress** in a format
  the board can act on — a pre-read deck (progress
  against the roadmap, technical risks, hiring status,
  security posture, key technical decisions since last
  board), a decision log (what the board is being asked
  to decide), and a defensible narrative that ties
  technical progress to the CEO's fundraising narrative.
- **Run technical due diligence for a fundraise or
  acquisition** — prepare a data room with the
  architecture overview, security-posture packet (SOC 2
  attest or readiness report, penetration-test summary,
  incident history, dependency inventory), IP hygiene
  evidence (contributor agreements, OSS licence audit,
  employment-agreement IP assignment), and a defensible
  answers-file for common diligence questions.
- **Handle a hostile technical due-diligence session** —
  where the buyer's technical DD lead is looking for
  architectural risk, key-person risk, or hidden
  compliance debt to justify a price cut — with
  prepared evidence rather than defensive posture.
- Author the **risk-engineering slice of a board-ready
  technical narrative** — recognising which technical
  risks the board actually needs to be told about
  (existential vulnerabilities, key-person risk, un-
  scoped compliance obligations) vs. which live inside
  the engineering org.
- Cite the boundary to
  [`founder-ceo-curriculum`](https://github.com/ai-startup-curriculum/founder-ceo-curriculum)
  on deep CEO-craft (fundraising narrative
  construction, board management as CEO, hiring
  executives, capital allocation) and to
  `startup-exit-curriculum` (level 40) on deep M&A,
  integration planning, and secondary-transaction depth.

## Chapters

1. [The CTO↔CEO Decision Cadence — Weekly 1:1, Decision-Rights Map, Tie-Breaker, Escalation](01-cto-ceo-decision-cadence.md) — the stable weekly 1:1 agenda; the four-column decision-rights map (CEO unilateral / CTO unilateral / consensus / board); the tie-breaker mechanism; the escalation path to a lead director or board observer.
2. [The Cofounder-Dispute Mechanic — Vesting, Tie-Breaker, Relationship Agreement, Mediation](02-cofounder-dispute-mechanic.md) — the mechanics you install *before* a disagreement; vesting with acceleration and cliff; the cofounder-relationship agreement (values, roles, decision rights, exit); the mediation route; the strict boundary to counsel on every underlying instrument.
3. [Briefing the Board on Technical Progress — Pre-Read, Decision Log, Roadmap Ties](03-board-pre-read.md) — the standing pre-read structure; the decision log the board acts on; progress against the roadmap; technical risks; hiring status; security posture; the narrative that ties engineering to the fundraising story.
4. [Technical Due-Diligence Data Room — Architecture, Security, IP, Answers-File](04-technical-due-diligence-data-room.md) — the six-folder DD data-room layout; the architecture overview; the security-posture packet (SOC 2 attest or readiness, pen-test summary, incident history, dependency inventory); the IP-hygiene evidence (contributor agreements, OSS licence audit, employment-agreement IP assignment); the answers-file for the recurring diligence questions.
5. [The Hostile Technical DD Session — When the Buyer Is Hunting for a Discount](05-hostile-technical-dd-session.md) — the three angles a hostile technical DD lead attacks from (architectural risk, key-person risk, hidden compliance debt); the evidence that pre-empts each; the "don't argue, produce the artifact" reflex; the escalation to the CEO when a DD finding needs a commercial rather than a technical response.
6. [The Board-Ready Technical Risk Narrative — What Rises to the Board vs. What Stays in Engineering](06-board-ready-technical-risk-narrative.md) — the three risk classes the board needs to hear about (existential vulnerabilities, key-person risk, un-scoped compliance obligations); the risks that live inside the engineering org; the narrative arc that ties the risk register to the CEO's fundraising narrative without either alarming the board or hiding the real exposure.
7. [Boundaries to `founder-ceo-curriculum` and `startup-exit-curriculum`](07-boundaries-founder-ceo-and-startup-exit.md) — deep CEO-craft (fundraising narrative construction, board management, exec hiring, capital allocation) lives in [`founder-ceo-curriculum`](https://github.com/ai-startup-curriculum/founder-ceo-curriculum); deep M&A, integration planning, and secondary-transaction depth live in `startup-exit-curriculum` (level 40); the CTO's job is to feed those tracks a defensible technical package, not to author their deliverables.

## Exercises

1. [CTO↔CEO Decision-Rights Map](exercises/exercise-01-cto-ceo-decision-rights-map.md) — ~2 hours. Author the four-column decision-rights map for your CTO / CEO pair, agree the tie-breaker mechanism, and name the escalation path.
2. [Cofounder-Dispute Mechanic Drill](exercises/exercise-02-cofounder-dispute-mechanic-drill.md) — ~2 hours. Audit the cofounder-dispute mechanics you actually have installed against the checklist in chapter 02 and produce a gap list routed to counsel.
3. [Board Pre-Read Authoring](exercises/exercise-03-board-pre-read-authoring.md) — ~3 hours. Author a real (or reference-startup) board pre-read using the standing structure from chapter 03 — progress, risks, hiring, security posture, decision log.
4. [Technical Due-Diligence Data Room Scaffold](exercises/exercise-04-technical-due-diligence-data-room-scaffold.md) — ~3 hours. Scaffold the six-folder DD data room with the folder-by-folder inventory of artifacts you own today, artifacts on the roadmap with a date, and the answers-file for the recurring questions.
5. [Hostile Tech-DD Response Drill](exercises/exercise-05-hostile-tech-dd-response-drill.md) — ~2 hours. Run the three-angle attack (architectural risk / key-person risk / hidden compliance debt) against your own data room and produce the pre-empting evidence artifact for each finding.
6. [Board-Ready Technical Narrative Authoring](exercises/exercise-06-board-ready-technical-narrative-authoring.md) — ~2 hours. Author the risk-engineering slice of your next board deck — the three-class risk register, the *what belongs on the board slide vs. what stays in engineering* decision, and the narrative tie to the CEO's fundraising story.

## Lab

- `lab-01-publish-a-cto-founder-communication-package`
  (~2 hours) — planned. Consolidates the six exercise
  outputs into a single `docs/founder-comms/` sub-tree
  in the working repo: the decision-rights map, the
  cofounder-dispute-mechanic audit and gap list, the
  board pre-read, the DD data room, the hostile-DD
  response drill, and the board-ready technical
  narrative. This sub-tree is the single artifact that
  answers *"how does the CTO show up next to the CEO
  and to the board?"* and is the direct input to
  capstone
  [`project-103`](../../projects/project-103-scaling-plan-from-five-to-fifty-engineers).

## Quiz

- One quiz (~30 min) covering: the four-column
  decision-rights map and the tie-breaker mechanism;
  what belongs in a cofounder-relationship agreement
  vs. what belongs in equity / vesting / voting
  instruments (counsel-drafted); the standing board
  pre-read structure and the decision log; the six-
  folder DD data-room layout and the answers-file
  discipline; the three angles a hostile technical DD
  lead attacks from and the pre-empting evidence for
  each; the three risk classes that rise to the board
  vs. the risks that stay in engineering; the boundary
  to
  [`founder-ceo-curriculum`](https://github.com/ai-startup-curriculum/founder-ceo-curriculum)
  and to `startup-exit-curriculum` (level 40).

## Resources

See [`resources.md`](resources.md) for the module's
primary references. Full citations for the whole
curriculum are in
[`.aicg/job-requirements.json`](../../.aicg/job-requirements.json)
under `authoritative_references`.

## What comes next

This is the final lecture module in the
`cto-curriculum` spine. Once you have completed the
exercises here, the natural next step is capstone
[`project-103`](../../projects/project-103-scaling-plan-from-five-to-fifty-engineers)
(*Scaling Plan From 5 → 15 → 40 Engineers*), which
integrates mod-103, 104, 105, 106, and 108 — the
board-ready narrative from this module is the vehicle
in which that capstone is *presented* to the board and
to a Series-A lead.

Beyond the CTO track, the two adjacent tracks this
module explicitly cites boundaries to are
[`founder-ceo-curriculum`](https://github.com/ai-startup-curriculum/founder-ceo-curriculum)
(deep CEO-craft: fundraising narrative construction,
board management as CEO, hiring executives, capital
allocation) and `startup-exit-curriculum` (level 40 —
deep M&A, integration planning, secondary-transaction
depth). Both consume the artifacts produced here.
