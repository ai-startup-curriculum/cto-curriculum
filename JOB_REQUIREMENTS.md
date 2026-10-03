# Job Requirements — Co-Founder / CTO

<!-- aicg:site-banner -->
> 🎓 Part of the free, open-source **AI Career Curriculum** ecosystem — [Infrastructure](https://github.com/ai-infra-curriculum) · [ML Engineering](https://github.com/ml-engineering-curriculum) · [AI Engineering](https://github.com/ai-engineering-curriculum) · [Governance](https://github.com/ai-governance-curriculum) · [Startup](https://github.com/ai-startup-curriculum). Live cohorts &amp; team programs: **[ai-infra-curriculum.github.io](https://ai-infra-curriculum.github.io/)**.
<!-- /aicg:site-banner -->

> Human-readable summary of [`.aicg/job-requirements.json`](./.aicg/job-requirements.json). The JSON is the source of truth; this document mirrors it in table form for reviewers, hiring managers, and learners deciding whether the curriculum fits their real role.

## Status — 2026-10 cycle merged 40 postings (26 carried forward + 14 fresh)

Merged corpus of 40 real postings in the 2026-07-05 → 2026-10-03 window (last 90 days). The cycle is a continuity top-up: 26 postings from the 2026-09 cycle still sit inside the current 90-day window and are carried forward; 14 fresh postings were sampled 2026-09-04 → 2026-10-03 to clear the ≥25 bar and probe for theme drift. 13 postings aged out of window (post-11, 12, 14, 15, 22, 23, 24, 27, 28, 29, 30, 31, 34) and are archived in [`.aicg/research/runs/cto-2026-09/postings.raw.json`](./.aicg/research/runs/cto-2026-09/postings.raw.json).

Distribution:

- **Sources**: Wellfound 24, ycombinator.com company pages 11, Welcome to the Jungle / Otta 7, Techstars 2.
- **Titles**: Technical Co-Founder / Founding CTO variants 25, Founding Engineer / Founding AI Engineer variants 13, Head of Engineering (startup) 2, VP Engineering (startup) 0.
- **Stage**: pre-seed 25, seed 15, series-a 0 (both 2026-09 Series-A postings aged out and no new Series-A postings were sampled — next cycle should re-prioritise Series-A sourcing).
- **AI-native mix**: true 29, false 11 (~73% AI-native, up ~6pp from 2026-09).
- **Geo**: US (SF, NY, Boston, Chicago, LA, Philadelphia, Palo Alto, Toronto), EU (Berlin, Paris, Amsterdam, London, Cologne, Düsseldorf, Aachen), MENA (Doha), India (Hyderabad, Pune), Africa (Lagos, Nairobi), Australia (Sydney). GBP@1.30 and EUR@1.10 conversion applied.
- **Sources attempted but gated**: workatastartup.com continues to 403 headless fetches (represented via canonical ycombinator.com company job permalinks), jobs.techstars.com Ada IQ founding-CTO detail 404'd on fetch, Welcome to the Jungle EU founding-engineer listings in the Sept-Oct window were mostly already closed/expired, WorkInStartups.com detail gated by auth, LinkedIn returned auth-walled search shells. No fabricated data.
- **Exclusions applied**: fractional / interim CTO postings and post-Series-B / growth-stage / public-company CTO postings, per the ownership rule.

**Tagging-consistency caveat**: the 2026-10 top-up sub-agent tagged T01 (CTO role framing), T26 (founder identity), and T28 (0-to-1 shipping velocity) more aggressively than the 2026-09 sub-agent — T01 lifted 0.26 → 0.48, T26 lifted 0.20 → 0.43, T28 lifted 0.26 → 0.43 on the merged sample. Reading the verbatim quotes, part of the lift is real (Sept-Oct 2026 pre-seed listings do carry heavier 'genuine co-founder' and 'ship in weeks' framing than June 2026 listings) and part is tagger-criterion drift (the top-up tagged any pre-seed 4-year-vest / 1-year-cliff posting with T26, whereas 2026-09 required explicit 'not CTO-in-name' language). Under a tagging-strict reading, T26 and T28 would sit at ~0.20-0.25, still below the ≥0.30 threshold. Either reading, **every ≥0.30 theme already has an owner** — this cycle's lift signals existing-coverage reinforcement, not a net-new content need.

**Delta this cycle**: no net-new curriculum modules, exercises, or projects. All ≥0.30 themes already have an owner. See [`.aicg/curriculum-plan-delta.json`](./.aicg/curriculum-plan-delta.json) for the empty-additions rationale, [`.aicg/job-requirements.json`](./.aicg/job-requirements.json) for the per-theme evidence, [`.aicg/research/runs/cto-2026-10/postings.compact.json`](./.aicg/research/runs/cto-2026-10/postings.compact.json) for the Sept-Oct top-up sample, and [`.aicg/research/runs/cto-2026-09/`](./.aicg/research/runs/cto-2026-09/) for the carried-forward 2026-09 raw sample.

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

**Defers sideways** on engineering-craft depth to `ai-infra-team-lead` (level 30 — day-two engineering-management craft), `ai-infra-mlops` and `ai-infra-ml-platform` (level 25-30 — MLOps / platform depth for AI-native startups, including the *hands-on shipping* of LLM/agent product features surfaced at 0.51 this cycle), and `ai-risk-engineer` (level 25 — AI-safety hygiene the AI-native CTO consumes before hiring a dedicated risk engineer).

**Defers up** to `ai-infra-senior-architect` (level 45), `ai-infra-principal-engineer` (level 50), `ai-infra-principal-architect` (level 55) for post-Series-B scale-up architectural depth, and to `chief-ai-officer` (level 70) for AI-org executive scope at C-suite.

**Out of scope**: legal opinion (CTO briefs counsel, consumes counsel's opinion), external audit attestation (CTO owns readiness and evidence, not the attest opinion), and specialist advisor scope (patent, immigration, tax).

## Requirement themes

Coverage abbreviations:

- **mod-1XX** — a numbered module in this curriculum
- **peer** — deferred to a peer track (deep depth linked out)
- **prereq** — assumed prerequisite (documented in [`PREREQUISITES.md`](./PREREQUISITES.md))
- **up** — deferred up to a higher-level track

Frequency is `posting_count / 40`. The ≥0.30 net-new-content threshold requires ≥12 postings.

| # | Theme | Owner | Coverage | Frequency (n=40, 2026-10) | Δ vs 2026-09 |
|---|---|---|---|---|---|
| 01 | CTO role position on the ladder, stage-by-stage self-development plan | `cto` | mod-101 | **0.48 (19)** ✓§ | +0.22 |
| 02 | Architecture under uncertainty — ADRs, C4, monolith-first, evolutionary architecture, ISO/IEC 25010 trade-offs | `cto` | mod-102 | **0.58 (23)** ✓ | +0.07 |
| 03 | Build-vs-buy and platform choices — cloud economics, vendor selection, AI-stack decisions | `cto` | mod-103 | 0.23 (9) | — |
| 04 | First engineering hires and team topology — hiring plan, interview loop, Team Topologies patterns | `cto` | mod-104 | **0.43 (17)** ✓ | +0.06 |
| 05 | Technical debt as a business decision — portfolio, cost-to-carry, refactor budget, deprecation vs. StranglerFig rewrite | `cto` | mod-105 | 0.05 (2)† | — |
| 06 | Scaling the org and the stack — 0 → 5 → 15 → 50 → 150 engineers transitions | `cto` | mod-106 | 0.18 (7) | -0.02 |
| 07 | Founder-scope security and compliance — SOC 2 Type I, GDPR / CCPA, HIPAA baseline, OWASP ASVS, SLSA, vendor DPA / BAA | `cto` | mod-107 | 0.20 (8) | +0.03 |
| 08 | CTO↔CEO relationship, board technical communication, technical due diligence | `cto` | mod-108 | 0.18 (7) | +0.04 |
| 09 | Python / TypeScript / cloud fluency at technical-co-founder depth | `ai-infra-junior-engineer` / `ai-infra-engineer` | prereq | **0.60 (24)** ✓ | +0.14 |
| 10 | Product discovery, roadmap, delivery-cadence fluency | `cpo-curriculum` | peer | **0.43 (17)** ✓ | +0.09 |
| 11 | CEO strategy, fundraising cadence, cap-table literacy | `founder-ceo-curriculum` | peer | 0.13 (5) | +0.04 |
| 12 | HR / people-ops / compensation / performance-management basics | `startup-operations-governance-curriculum` | peer | 0.28 (11)¶ | +0.08 |
| 13 | Finance / runway / unit-economics basics | `startup-finance-fundraising-curriculum` | peer | 0.00 (0)‡ | — |
| 14 | GTM / enterprise-sales-motion basics | `startup-product-gtm-curriculum` | peer | 0.15 (6) | +0.01 |
| 15 | Delivery cadence, DORA four-key signals, blameless post-mortems | `cto` | mod-106 (slice) | 0.10 (4) | -0.01 |
| 16 | Day-two engineering-management craft (1:1s, career ladders, performance-management) | `ai-infra-team-lead` | peer | 0.15 (6) | +0.01 |
| 17 | Deep platform, distributed-systems, multi-region architecture beyond ~50 engineers | `ai-infra-senior-architect` / `ai-infra-principal-architect` | up | 0.08 (3) | -0.03 |
| 18 | AI-native platform decisions — foundation-model API vs. self-host, RAG / fine-tune / tool-use, inference cost economics | `cto` | mod-103 (AI-native slice) | **0.58 (23)** ✓ | +0.01 |
| 19 | Hands-on shipping of production LLM / agent product features (not demos) | `cto` (build-vs-buy) + `ai-infra-mlops` / `ai-infra-ml-platform` / `applied-ai-engineer` for shipping craft | mod-103 (AI-native slice) + peer | **0.53 (21)** ✓ | +0.02 |
| 20 | MLOps / model-lifecycle basics — evaluation, guardrails, fallbacks, monitoring, human-review paths | `ai-infra-mlops` | peer | 0.23 (9) | +0.09 |
| 21 | AI safety / responsible-AI hygiene at founder scale | `ai-risk-engineer` | peer + mod-107 slice | 0.13 (5) | +0.04 |
| 22 | Data privacy for AI — multi-tenant isolation, PII in prompts / logs, retention with foundation-model vendors | `cto` | mod-107 (privacy slice) + mod-103 (multi-tenancy) | 0.25 (10) | +0.11 |
| 23 | Enterprise-readiness — SSO / SAML / OIDC, SCIM, audit logs, ISO 27001 / SOC 2 as GTM enabler | `cto` | mod-103 (auth build-vs-buy) + mod-107 (compliance) + peer product-gtm | 0.10 (4) | -0.01 |

✓ = crosses the ≥0.30 net-new-content threshold — every one already has an owner (this repo or a peer track).
§ = T01 lift partly reflects tagger-criterion drift between 2026-09 and 2026-10 (see Status section). mod-101 ownership unaffected.
† = mod-105 retained despite low posting frequency because CTO Craft, Fournier, Larson, and Fowler all treat technical-debt framing as core CTO craft; the low frequency reflects JD blind spot, not curriculum irrelevance.
‡ = zero verbatim hits across two cycles reflects a known JD blind spot (founders/CEOs rarely name runway/unit-economics in the CTO JD even where the CTO opines on it), not curriculum irrelevance. Keep peer-linked.
¶ = T12 (HR / people-ops basics) climbed from 0.20 to 0.28 and is now just below threshold — monitor next cycle; coverage already peer-owned.

## Emerging themes (threshold-crossing watch + below-threshold)

Second-cycle re-sampling confirmed every theme already has a home. Two themes (founder-identity, 0-to-1 shipping velocity) technically crossed the 0.30 threshold on the merged sample — both are flagged for watch under the Status section's tagging-consistency caveat and both already have explicit hooks in existing modules. See [`.aicg/job-requirements.json`](./.aicg/job-requirements.json) `emerging_themes_below_threshold` for full evidence per theme.

| Theme | 2026-10 Frequency (n=40) | 2026-09 Frequency (n=39) | Current coverage / recommendation |
|---|---|---|---|
| **Founder identity / equal-ownership expectation** — postings explicitly reject "CTO-in-name" or "senior hire" framing and demand a genuine co-founder | 0.43 (17) ⚠ | 0.20 (7) | mod-101 lesson 01 (`cto-ladder-pre-seed-to-series-b.md`) + exercise-04 (`curriculum-scope-and-deferral-contract.md`) already teach the co-founder-vs-hire distinction. ⚠ Crossing is partly tagger-criterion drift (see Status). **No new module or exercise this cycle.** If this holds under consistent tagging next cycle, add a targeted mod-101 exercise that forces learners to diagnose a verbatim JD. |
| **0-to-1 shipping velocity / MVP-in-weeks** | 0.43 (17) ⚠ | 0.26 (9) | mod-102 (spikes with kill criteria) + mod-106 lesson 01 (`01-zero-to-five-first-process.md`) + exercise-01 (`exercise-01-zero-to-five-first-process-drill.md`) already teach the discipline. ⚠ Crossing is partly tagger-criterion drift (see Status). **No new module or exercise this cycle.** If this holds under consistent tagging next cycle, add a targeted mod-106 exercise that forces learners to defend a 2-4 week MVP cadence against founder six-month pressure. |
| **AI-native engineering workflow fluency** — Claude Code, Cursor, Codex, MCP tools in daily hands-on use | 0.15 (6) | 0.11 (4) | Prereq-owned by ai-infra-engineer. Track in PREREQUISITES.md; expand only if frequency lifts above 0.30 next cycle. |
| **Cost / FinOps for GPU / inference workloads** | 0.05 (2) | 0.03 (1) | Adjacent to mod-103 AI-native slice. Reference; do not expand. |
| **Open-source strategy as moat** | 0.03 (1) | 0.03 (1) | Adjacent to mod-103 and mod-108. Reference; do not expand. |
| **Fractional CTO / CTO-as-a-service** | 0.00 (0) | 0.00 (0) | Excluded on exclusion filter; separate market segment. Not covered. |
| **CTO community-of-practice membership** (CTO Craft, CTO Connection) | N/A | N/A | Not a JD-observable requirement. Documented in references; informational. |

## Authoritative references (grounding for canon-level material)

Grouped by kind. Full citations with `use` notes are in [`.aicg/job-requirements.json`](./.aicg/job-requirements.json) → `authoritative_references`.

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

## Salary evidence (2026-10 cycle, n=40)

Cash disclosed on 15 postings; equity disclosed on 34 postings. USD conversion applied to GBP@1.30 and EUR@1.10.

**Deliberately not aggregated across stages** — the Co-Founder / CTO market is bimodal (pre-funded technical co-founders with founder equity and near-zero cash vs. post-Series-A CTOs with market-rate cash and smaller equity), so a single aggregate would obscure both distributions.

| Stage | Cash-disclosed n | Cash range (USD) | Cash representative band | Equity notes |
|---|---|---|---|---|
| pre-seed | 2 | $70K–$180K spread | **sample too small** (n=2 — most 2026-10 top-up pre-seed postings offered equity-only, not cash+equity). Treat the 2026-09 cycle's ~$90K-$180K USD pre-seed band as informational until next cycle re-samples. | Co-founder equity continues to dominate — 23 of 25 pre-seed postings disclose equity, bimodal: genuine co-founder 10-50% (17 postings) vs. senior founding-hire 0.5-1.5% (3 postings). Several explicit equity-only / cash-at-revenue-milestones offers (Malkolm, LongRun, Anise 50%). |
| seed | 13 | $80K–$270K spread | ~$150K–$225K USD (stable vs. 2026-09) | Founding-engineer / early-CTO-hire equity typically 0.10-2.00%. YC / Otta seed cluster ~0.5-1.0%; AI-native pre-Series-A seed rounds go higher (Ochre 2.0-4.0%). |
| series-a | 0 | N/A | **N=0 THIS CYCLE** — both 2026-09 Series-A postings aged out and no new Series-A CTO postings were sampled. Next cycle should re-prioritise Series-A sourcing. Treat the pre-existing $180K-$300K US Series-A CTO band as informational only. | No Series-A equity data in this cycle (n=0). |

Full ranges (verbatim, USD) in [`.aicg/job-requirements.json`](./.aicg/job-requirements.json) `salary_evidence.per_stage_ranges`.

---

<!-- aicg:maintained-by -->
Maintained by [VeriSwarm.ai](https://veriswarm.ai)
