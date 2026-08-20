# Co-Founder / CTO Curriculum — Role Pathway

> **How do I turn technology into a scalable company capability?**

A role *pathway* over the shared functional curricula — not a separate body of
knowledge. Start with [startup-foundations](https://github.com/ai-startup-curriculum/startup-foundations),
then work the pillars below in dependency order at your stage.

## Target coverage

| Pillar | Target | Owning curriculum |
|---|----|----|
| Foundations | 100% | [startup-foundations](https://github.com/ai-startup-curriculum/startup-foundations) |
| Technical Leadership | 100% | this repo |
| Product | 70% | [cpo-curriculum](https://github.com/ai-startup-curriculum/cpo-curriculum) |
| People | 70% | [operations & governance](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum) |
| Strategy | 40% | [founder-ceo](https://github.com/ai-startup-curriculum/founder-ceo-curriculum) |
| Finance | 30% | [finance & fundraising](https://github.com/ai-startup-curriculum/startup-finance-fundraising-curriculum) |
| GTM / Sales | 30% | [product & GTM](https://github.com/ai-startup-curriculum/startup-product-gtm-curriculum) |
| Governance | 30% | [operations & governance](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum) |

## Technical Leadership modules (this repo owns)

Level-25 track — total planned scope **270 hours** (140h modules + 130h
projects). Full plan in [`.aicg/curriculum-plan.json`](./.aicg/curriculum-plan.json);
requirement themes and ownership rule in
[`JOB_REQUIREMENTS.md`](./JOB_REQUIREMENTS.md).

| Module | Hours | Focus |
|---|---|---|
| [mod-101 The Co-Founder / CTO Role and the Ownership Map](./lessons/mod-101-cto-role-and-ownership-map) | 10 | Stage-by-stage self-development plan; CTO vs. VP Eng vs. Chief Architect; where this repo ends and each peer track begins |
| [mod-102 Architecture Under Uncertainty](./lessons/mod-102-architecture-under-uncertainty) | 20 | ADRs, C4 diagrams, MonolithFirst / StranglerFig, ISO/IEC 25010 quality-attribute trade-offs, evolutionary architecture, spikes with kill criteria |
| [mod-103 Build-vs-Buy, Vendor Selection, and Platform Economics](./lessons/mod-103-build-vs-buy-and-platform-economics) | 18 | Cloud economics, managed vs. self-hosted for the classic categories, AI-native stack (foundation-model API vs. self-host, RAG / fine-tune / tool-use), vendor-selection scorecard |
| [mod-104 First Engineering Hires and Team Topology](./lessons/mod-104-first-engineering-hires-and-team-topology) | 20 | Hiring plan against roadmap + runway, interview loop and rubrics, founding-engineer profile, Team Topologies at 5-25 engineers, first EM / tech lead / VP Eng decisions, career-ladder v0 |
| [mod-105 Technical Debt as a Business Decision](./lessons/mod-105-technical-debt-as-business-decision) | 16 | Fowler quadrants, cost-to-carry sizing, refactor budget tied to the roadmap, deprecate vs. rewrite (Chesterton's Fence + StranglerFig) vs. leave, portfolio decision-log |
| [mod-106 Scaling the Org and the Stack: 0 → 5 → 15 → 50 → 150](./lessons/mod-106-scaling-org-and-stack) | 22 | Stage-transition playbooks, DORA four-key measurement, platform-investment sizing per stage, delivery cadence and on-call design |
| [mod-107 Founder-Scope Security, Privacy, and Compliance](./lessons/mod-107-founder-scope-security-and-compliance) | 18 | SOC 2 Type I readiness, ISO/IEC 27001 posture, GDPR / CCPA baseline, HIPAA BAA path, OWASP ASVS, SLSA build-provenance, vendor DPA / BAA acquisition |
| [mod-108 The CTO↔CEO Relationship, Board Communication, and Technical Due Diligence](./lessons/mod-108-cto-ceo-and-board-communication) | 16 | CEO decision-rights map, cofounder-dispute mechanic, board pre-read, technical-DD data room, board-ready technical narrative |

### Capstone projects

| Project | Hours | Integrates |
|---|---|---|
| [project-101 First-Year Technical Strategy for One Seed-Stage Startup](./projects/project-101-first-year-technical-strategy-for-one-seed-startup) | 35 | mod-101, 102, 103, 104 |
| [project-102 SOC 2 Type I Readiness and Founder-Scope Compliance Package](./projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package) | 35 | mod-105, 107 |
| [project-103 Scaling Plan From 5 → 15 → 40 Engineers](./projects/project-103-scaling-plan-from-five-to-fifty-engineers) | 60 | mod-103, 104, 105, 106, 108 |

## Ownership rule

Assign primary coverage to the lowest-level role that genuinely requires the
skill. Higher-level tracks link to that owner unless additional depth,
architectural context, or leadership scope is required.

- **This repo owns** the *engineering-leadership craft* of the Co-Founder / CTO
  position at pre-seed → Series-A scale (see the modules above).
- **Peer to** `cpo-curriculum` (Product), `founder-ceo-curriculum` (Strategy /
  Fundraising / CEO), `startup-operations-governance-curriculum` (People /
  Governance), `startup-finance-fundraising-curriculum` (Finance), and
  `startup-product-gtm-curriculum` (GTM / Sales / Marketing) — deep depth in
  each pillar defers to its owning peer track.
- **Peer to** `ai-infra-team-lead` (level 30) on day-two engineering-management
  craft; **peer to** `ai-infra-mlops` (level 25) and `ai-infra-ml-platform`
  (level 30) on MLOps / platform depth for AI-native startups; **peer to**
  `ai-risk-engineer` (level 25, AI Governance family) on AI-safety hygiene the
  AI-native CTO consumes.
- **Defers up** to `ai-infra-senior-architect` (level 45),
  `ai-infra-principal-engineer` (level 50), `ai-infra-principal-architect`
  (level 55), `chief-ai-officer` (level 70), and `startup-exit-curriculum`
  (level 40) for post-Series-B / >50-engineer / exit-track scope.
- **Defers down** to `startup-foundations` for shared functional groundwork
  and to `ai-infra-junior-engineer` (level 10) / `ai-infra-engineer` (level 20)
  for engineering-craft prerequisites.
- **Out of scope**: legal opinion (the CTO briefs counsel), external audit
  attestation itself (the CTO owns readiness and evidence), specialist advisor
  scope (patent, immigration, tax).

Full ownership rule and requirement-theme map in
[`JOB_REQUIREMENTS.md`](./JOB_REQUIREMENTS.md) and
[`.aicg/job-requirements.json`](./.aicg/job-requirements.json).

## Status

Plan authored (level-25, 270h) and lesson / project directories reserved. Module
lessons and worked exemplars are authored by the autonomous
research→author pipeline (oldest-gap-first). Coverage %s are the canonical
targets from
[FUNCTIONAL_CURRICULA.md](https://github.com/ai-startup-curriculum/startup-foundations/blob/main/FUNCTIONAL_CURRICULA.md).
Live-postings sampling was deferred in the bootstrap session — see
[`JOB_REQUIREMENTS.md`](./JOB_REQUIREMENTS.md) `Status` section for the
sampling guidance the next research cycle should apply.

---

<!-- aicg:maintained-by -->
Maintained by [VeriSwarm.ai](https://veriswarm.ai)
