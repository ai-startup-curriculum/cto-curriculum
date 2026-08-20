# Job Requirements — Co-Founder / CTO

<!-- aicg:site-banner -->
> 🎓 Part of the free, open-source **AI Career Curriculum** ecosystem — [Infrastructure](https://github.com/ai-infra-curriculum) · [ML Engineering](https://github.com/ml-engineering-curriculum) · [AI Engineering](https://github.com/ai-engineering-curriculum) · [Governance](https://github.com/ai-governance-curriculum) · [Startup](https://github.com/ai-startup-curriculum). Live cohorts &amp; team programs: **[ai-infra-curriculum.github.io](https://ai-infra-curriculum.github.io/)**.
<!-- /aicg:site-banner -->

> Human-readable summary of [`.aicg/job-requirements.json`](./.aicg/job-requirements.json). The JSON is the source of truth; this document mirrors it in table form for reviewers, hiring managers, and learners deciding whether the curriculum fits their real role.

## Status — bootstrap session, live postings deferred

This packet was **scaffolded** — not sampled from live job postings — because `WebSearch` and `WebFetch` are permission-gated in the bootstrap session and cannot be exercised by a delegated subagent either. The plan is grounded in **authoritative public references** (canonical books, essays, standards, official startup-school materials) rather than invented posting data. Every requirement below carries a `<!-- needs-research -->` marker in the frequency column and every posting-derived field is empty.

The next autonomous research cycle should widen `postings[]` to at least **25 in-window observations** (window: 2026-05-22 → 2026-08-20, 90 days). See `.aicg/job-requirements.json` → `research_status.needs_research_note` for the sampling guidance — in particular the filter for (a) technical co-founders at pre-seed / seed startups and (d) post-Series-A scale-up CTOs where the person still writes code sometimes, hires the first 5-30 engineers, and sits alone at the top of the engineering org, and the exclusion of fractional / interim CTO postings and post-Series-B / public-company CTO postings.

## Ownership rule

Assign primary coverage to the lowest-level role that genuinely requires the skill. Higher-level tracks link to that owner unless additional depth, architectural context, or leadership scope is required.

The **Co-Founder / CTO (level 25, Startup Leadership family)** sits at the top of the engineering org of a pre-seed → Series-A startup and owns the **engineering-leadership craft** of turning technology into a company capability:

- Technical strategy under uncertainty
- Build-vs-buy and platform choices
- First engineering hires and team topology
- Technical debt portfolio management
- Stage-by-stage org and stack scaling (0 → 5 → 50 engineers)
- Founder-scope security and compliance
- The CTO↔CEO / CTO↔board relationship, including technical due diligence

**Peer to** the other Startup Leadership tracks (see the pathway coverage table in [`CURRICULUM.md`](./CURRICULUM.md)) — `cpo-curriculum` (Product), `founder-ceo-curriculum` (Strategy / Fundraising / CEO), `startup-operations-governance-curriculum` (People / Governance), `startup-finance-fundraising-curriculum` (Finance), and `startup-product-gtm-curriculum` (GTM / Sales / Marketing).

**Defers down** to `startup-foundations` for the shared functional groundwork (company formation, stage vocabulary, unit-economics basics) and to the AI Infrastructure ladder for engineering-craft prerequisites (`ai-infra-junior-engineer` level 10, `ai-infra-engineer` level 20).

**Defers sideways** on engineering-craft depth to `ai-infra-team-lead` (level 30 — day-two engineering-management craft), `ai-infra-mlops` and `ai-infra-ml-platform` (level 25-30 — MLOps / platform depth for AI-native startups), and `ai-risk-engineer` (level 25 — AI-safety hygiene the AI-native CTO consumes before hiring a dedicated risk engineer).

**Defers up** to `ai-infra-senior-architect` (level 45), `ai-infra-principal-engineer` (level 50), `ai-infra-principal-architect` (level 55) for post-Series-B scale-up architectural depth, and to `chief-ai-officer` (level 70) for AI-org executive scope at C-suite.

**Out of scope**: legal opinion (CTO briefs counsel, consumes counsel's opinion), external audit attestation (CTO owns readiness and evidence, not the attest opinion), and specialist advisor scope (patent, immigration, tax).

## Requirement themes

Coverage abbreviations:

- **mod-1XX** — a numbered module in this curriculum
- **peer** — deferred to a peer track (deep depth linked out)
- **prereq** — assumed prerequisite (documented in [`PREREQUISITES.md`](./PREREQUISITES.md))
- **up** — deferred up to a higher-level track

| # | Theme | Owner | Coverage | Frequency |
|---|---|---|---|---|
| 01 | CTO role position on the ladder, stage-by-stage self-development plan | `cto` | mod-101 | <!-- needs-research --> |
| 02 | Architecture under uncertainty — ADRs, C4, monolith-first, evolutionary architecture, ISO/IEC 25010 trade-offs | `cto` | mod-102 | <!-- needs-research --> |
| 03 | Build-vs-buy and platform choices — cloud economics, vendor selection, AI-stack decisions | `cto` | mod-103 | <!-- needs-research --> |
| 04 | First engineering hires and team topology — hiring plan, interview loop, Team Topologies patterns | `cto` | mod-104 | <!-- needs-research --> |
| 05 | Technical debt as a business decision — portfolio, cost-to-carry, refactor budget, deprecation vs. StranglerFig rewrite | `cto` | mod-105 | <!-- needs-research --> |
| 06 | Scaling the org and the stack — 0 → 5 → 15 → 50 → 150 engineers transitions | `cto` | mod-106 | <!-- needs-research --> |
| 07 | Founder-scope security and compliance — SOC 2 Type I, GDPR / CCPA, HIPAA baseline, OWASP ASVS, SLSA, vendor DPA / BAA | `cto` | mod-107 | <!-- needs-research --> |
| 08 | CTO↔CEO relationship, board technical communication, technical due diligence | `cto` | mod-108 | <!-- needs-research --> |
| 09 | Python / TypeScript / cloud fluency at technical-co-founder depth | `ai-infra-junior-engineer` / `ai-infra-engineer` | prereq | <!-- needs-research --> |
| 10 | Product discovery, roadmap, delivery-cadence fluency | `cpo-curriculum` | peer | <!-- needs-research --> |
| 11 | CEO strategy, fundraising cadence, cap-table literacy | `founder-ceo-curriculum` | peer | <!-- needs-research --> |
| 12 | HR / people-ops / compensation / performance-management basics | `startup-operations-governance-curriculum` | peer | <!-- needs-research --> |
| 13 | Finance / runway / unit-economics basics | `startup-finance-fundraising-curriculum` | peer | <!-- needs-research --> |
| 14 | GTM / enterprise-sales-motion basics | `startup-product-gtm-curriculum` | peer | <!-- needs-research --> |
| 15 | Delivery cadence, DORA four-key signals, blameless post-mortems | `cto` | mod-106 (slice) | <!-- needs-research --> |
| 16 | Day-two engineering-management craft (1:1s, career ladders, performance-management) | `ai-infra-team-lead` | peer | <!-- needs-research --> |
| 17 | Deep platform, distributed-systems, multi-region architecture beyond ~50 engineers | `ai-infra-senior-architect` / `ai-infra-principal-architect` | up | <!-- needs-research --> |
| 18 | AI-native platform decisions — foundation-model API vs. self-host, RAG / fine-tune / tool-use, inference cost economics | `cto` | mod-103 (AI-native slice) | <!-- needs-research --> |

## Authoritative references (grounding for scaffold-mode requirements)

Grouped by kind. Full citations with `use` notes are in `.aicg/job-requirements.json` → `authoritative_references`.

**Startup-track shared foundation**

- [`startup-foundations` — FUNCTIONAL_CURRICULA.md and STARTUP_STAGES.md](https://github.com/ai-startup-curriculum/startup-foundations)
- [Y Combinator — Startup School Library](https://www.startupschool.org/library) and [Work at a Startup](https://www.workatastartup.com/)
- [Stanford CS183F — 'How to Start a Startup' (Sam Altman lecture series)](https://startupclass.samaltman.com/)
- [Paul Graham — Essays](https://paulgraham.com/articles.html)
- [Y Combinator's `The Startup CTO's Handbook` (Zach Goldberg, open source)](https://github.com/ZachGoldberg/Startup-CTO-Handbook)
- [CTO Craft community resources](https://www.ctocraft.com/)

**Engineering leadership canon**

- [Camille Fournier — 'The Manager's Path'](https://www.oreilly.com/library/view/the-managers-path/9781491973882/)
- [Will Larson — 'An Elegant Puzzle: Systems of Engineering Management'](https://lethain.com/elegant-puzzle/)
- [Will Larson — 'Staff Engineer: Leadership Beyond the Management Track'](https://staffeng.com/book)
- [Ben Horowitz — 'The Hard Thing About Hard Things'](https://www.harpercollins.com/products/the-hard-thing-about-hard-things-ben-horowitz)
- [Elad Gil — 'High Growth Handbook'](https://growth.eladgil.com/)
- [Charity Majors — 'The Engineer/Manager Pendulum' and 'What is a CTO?' essays](https://charity.wtf/2019/01/04/engineering-management-the-pendulum-or-the-ladder/)
- [Michael Lopp — 'Managing Humans' / Rands in Repose](https://randsinrepose.com/)

**Architecture and quality**

- [Michael Nygard — 'Documenting Architecture Decisions' (ADRs)](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)
- [Simon Brown — C4 Model for visualising software architecture](https://c4model.com/)
- [Ford, Parsons, Kua — 'Building Evolutionary Architectures'](https://www.oreilly.com/library/view/building-evolutionary-architectures/9781491986356/)
- [Martin Fowler — 'StranglerFigApplication' and 'MonolithFirst'](https://martinfowler.com/bliki/StranglerFigApplication.html)
- [Sam Newman — 'Building Microservices' (2nd edition)](https://samnewman.io/books/building_microservices_2nd_edition/)
- [Martin Kleppmann — 'Designing Data-Intensive Applications'](https://dataintensive.net/)
- [Werner Vogels — 'Eventually Consistent'](https://www.allthingsdistributed.com/2008/12/eventually_consistent.html)
- [ISO/IEC 25010:2023 — SQuaRE Software Quality Model](https://www.iso.org/standard/78176.html)
- [Matthew Skelton and Manuel Pais — 'Team Topologies'](https://teamtopologies.com/book)

**Product management (for the CTO ↔ CPO handshake)**

- [Marty Cagan — 'Inspired'](https://www.svpg.com/books/)
- [Marty Cagan and Chris Jones — 'Empowered'](https://www.svpg.com/books/)

**Delivery cadence and DORA**

- [Forsgren, Humble, Kim — 'Accelerate' + DORA State of DevOps reports](https://dora.dev/)
- [Winters, Manshreck, Wright (eds.) — 'Software Engineering at Google'](https://abseil.io/resources/swe-book)

**Vendor / platform reference (for build-vs-buy)**

- [ThoughtWorks Technology Radar](https://www.thoughtworks.com/radar)
- [CNCF Landscape](https://landscape.cncf.io/)
- [OpenAI Enterprise Privacy / BAA and vendor DPA references](https://openai.com/enterprise-privacy)

**Security and compliance (founder scope)**

- [AICPA — SOC 2 Trust Services Criteria](https://www.aicpa-cima.com/topic/audit-assurance/audit-and-assurance-greater-than-soc-2)
- [ISO/IEC 27001:2022 — Information security management systems](https://www.iso.org/standard/27001)
- [NIST Cybersecurity Framework 2.0](https://www.nist.gov/cyberframework)
- [NIST SP 800-53 Rev. 5](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf)
- [GDPR (Regulation (EU) 2016/679)](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [CCPA / CPRA](https://oag.ca.gov/privacy/ccpa)
- [HIPAA Security Rule](https://www.hhs.gov/hipaa/for-professionals/security/index.html)
- [OWASP Application Security Verification Standard (ASVS)](https://owasp.org/www-project-application-security-verification-standard/)
- [OpenSSF SLSA](https://slsa.dev/)
- [OpenSSF Secure Software Development Fundamentals](https://openssf.org/education/)

**CTO ↔ CEO / board / technical due diligence**

- [Andreessen Horowitz — a16z operator library](https://a16z.com/library/) and [technical due-diligence checklist](https://a16z.com/tech-diligence-checklist/)
- [Sequoia Capital — Arc / Company Design library](https://www.sequoiacap.com/article/company-design-and-the-role-of-founders/)
- [First Round Review](https://review.firstround.com/)
- [Lenny's Newsletter — Engineering / CTO track](https://www.lennysnewsletter.com/)
- [NFX / Founders Fund founder content](https://www.nfx.com/)

**Foundational startup framing**

- [Eric Ries — 'The Lean Startup'](https://theleanstartup.com/)

## Emerging themes (below the coverage threshold this cycle)

- **Fractional CTO / CTO-as-a-service** — different economics, different scope. Not covered; revisit if a distinct market for fractional-CTO training emerges.
- **AI safety / responsible-AI at founder scale** — covered as a slice of mod-107. Deep engineering depth defers to `ai-risk-engineer-learning`.
- **Open-source strategy as moat** — referenced inside mod-103 and mod-108. Expand only if a future research cycle shows ≥0.30 frequency in postings.
- **CTO community-of-practice membership** (CTO Craft, CTO Connection) — documented as an ongoing peer-learning surface in the references.

## Salary evidence

<!-- needs-research --> Salary aggregates are deferred until the next research cycle collects ≥25 in-window postings with published ranges. The market is bimodal — pre-funded technical co-founders take founder equity and near-zero cash, while post-Series-A CTOs take market-rate cash comp plus meaningful equity — so a single aggregate would obscure both distributions. See `.aicg/job-requirements.json` → `salary_evidence` for the full note.

---

<!-- aicg:maintained-by -->
Maintained by [VeriSwarm.ai](https://veriswarm.ai)
