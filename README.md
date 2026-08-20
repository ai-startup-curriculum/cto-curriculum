# Ai Startup · Co-Founder / CTO — Curriculum

<!-- aicg:site-banner -->
> 🎓 Part of the free, open-source **AI Career Curriculum** ecosystem — [Infrastructure](https://github.com/ai-infra-curriculum) · [ML Engineering](https://github.com/ml-engineering-curriculum) · [AI Engineering](https://github.com/ai-engineering-curriculum) · [Governance](https://github.com/ai-governance-curriculum) · [Startup](https://github.com/ai-startup-curriculum). Live cohorts &amp; team programs: **[ai-infra-curriculum.github.io](https://ai-infra-curriculum.github.io/)**.
<!-- /aicg:site-banner -->

> **How do I turn technology into a scalable company capability?**

The Co-Founder / CTO pathway through the [`ai-startup-curriculum`](https://github.com/ai-startup-curriculum)
— a role *pathway* over the shared functional curricula, not a separate body
of knowledge. Start with
**[startup-foundations](https://github.com/ai-startup-curriculum/startup-foundations)**,
then work the modules your stage calls for.

Level-25 track, **270 planned hours** (140h modules + 130h projects). Full
requirements, ownership rule, and references live in
[`JOB_REQUIREMENTS.md`](./JOB_REQUIREMENTS.md); the module and project spine
lives in [`CURRICULUM.md`](./CURRICULUM.md); the machine-readable plan lives
in [`.aicg/curriculum-plan.json`](./.aicg/curriculum-plan.json).

## What this repo owns

The **Technical Leadership** pillar at pre-seed → Series-A scale:

- The Co-Founder / CTO role and the ownership map — where you sit, where
  each peer track picks up
- Architecture under uncertainty — ADRs, C4, MonolithFirst /
  StranglerFig-later, ISO/IEC 25010 quality-attribute trade-offs
- Build-vs-buy, vendor selection, and platform economics — including the
  AI-native stack (foundation-model API vs. self-host)
- First engineering hires and team topology — hiring plan, interview loop,
  Team Topologies at 5-25 engineers
- Technical debt as a business decision — portfolio, cost-to-carry,
  refactor budget
- Scaling the org and the stack — 0 → 5 → 15 → 50 → 150 engineers
- Founder-scope security, privacy, and compliance — SOC 2 Type I readiness,
  GDPR / CCPA / HIPAA baselines, OWASP ASVS, SLSA, vendor DPA / BAA
- The CTO↔CEO relationship, board communication, and technical due
  diligence

Peer coverage of Product, People, Strategy, Finance, GTM, and Governance
defers to the four peer Startup Leadership tracks — see the coverage table
in [`CURRICULUM.md`](./CURRICULUM.md).

## Layout

```
cto-curriculum/
├── lessons/mod-XXX-*/        modules with lectures, exercises, labs, quizzes
├── exemplars/mod-XXX-*/      worked reference deliverables (not code solutions)
├── projects/project-XXX-*/   multi-module capstones
├── CURRICULUM.md             role-level coverage map + module spine
├── JOB_REQUIREMENTS.md       requirement themes + ownership rule + references
├── PREREQUISITES.md          assumed entry skills + deferrals
├── VERSIONS.md               release history
├── .aicg/                    machine-readable plan and reports
└── README.md                 this file
```

## Exemplars

This is a single-repo curriculum: worked reference deliverables live
in-repo under [`exemplars/`](./exemplars), not in a separate solutions repo.

## Status

Plan-authored scaffold (2026-08-20). Live-postings sampling deferred to
the next autonomous research cycle — see [`JOB_REQUIREMENTS.md`](./JOB_REQUIREMENTS.md)
`Status` section. Module lessons and worked exemplars are authored
oldest-gap-first by the autonomous research→author pipeline.

---

<!-- aicg:maintained-by -->
Maintained by [VeriSwarm.ai](https://veriswarm.ai)
