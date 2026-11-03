# Job Requirements — Co-Founder / CTO

<!-- aicg:site-banner -->
> 🎓 Part of the free, open-source **AI Career Curriculum** ecosystem — [Infrastructure](https://github.com/ai-infra-curriculum) · [ML Engineering](https://github.com/ml-engineering-curriculum) · [AI Engineering](https://github.com/ai-engineering-curriculum) · [Governance](https://github.com/ai-governance-curriculum) · [Startup](https://github.com/ai-startup-curriculum) · [Workforce](https://github.com/ai-workforce-curriculum). Start at **[ai-curriculum-project.github.io](https://ai-curriculum-project.github.io/)**.
<!-- /aicg:site-banner -->

> Human-readable summary of [`.aicg/job-requirements.json`](./.aicg/job-requirements.json). The JSON is the source of truth; this document mirrors it in table form for reviewers, hiring managers, and learners deciding whether the curriculum fits their real role.

## Status — 2026-11 cycle merged 41 postings (29 carried forward + 12 fresh)

Merged corpus of 41 real postings in the 2026-08-05 → 2026-11-03 window (last 90 days). The cycle is a third continuity top-up: 29 postings from the 2026-10 merged corpus (15 of the original 2026-09 batch + all 14 from the 2026-10 Sept-Oct top-up) still sit inside the current 90-day window and are carried forward; 12 fresh postings were sampled 2026-10-04 → 2026-11-03 (13 raw minus 1 duplicate URL — LuminOne wellfound /jobs/4779217 appeared again and was de-duplicated against 2026-10 post-A06). 11 postings aged out of window (post-06, 08, 09, 10, 16, 18, 19, 20, 21, 25, 35) and are archived in [`.aicg/research/runs/cto-2026-09/postings.raw.json`](./.aicg/research/runs/cto-2026-09/postings.raw.json).

Distribution:

- **Sources**: Wellfound 25, ycombinator.com company pages 10, Welcome to the Jungle / Otta 4, Techstars 2.
- **Titles**: Technical Co-Founder / Founding CTO variants 29, Founding Engineer / Founding AI Engineer variants 10, Head of Engineering (startup) 2, VP Engineering (startup) 0.
- **Stage**: pre-seed 30, seed 11, series-a 0 (Series-A gap persists for the second consecutive cycle — no fresh Series-A postings sampled in either the 2026-10 or 2026-11 top-up windows; next cycle MUST actively re-prioritise Series-A sourcing).
- **AI-native mix**: true 25, false 16 (~61% AI-native, down ~12pp from 2026-10 as the Oct-Nov top-up pulled more non-AI regulated-domain postings — MedTech FDA, consumer e-commerce, fintech regulated-broker API, physical surf simulator).
- **Geo**: US (SF, NY, Boston, LA, Palo Alto, Philadelphia, Toronto, remote-US), EU (Berlin, Paris, Amsterdam, London, Cologne, Düsseldorf, Aachen, Turin, Birmingham, Stockholm), MENA (Doha), India (Hyderabad, Pune, Mumbai, Jaipur), APAC (Tokyo + Asia-remote), Africa (Lagos, Nairobi), Australia (Sydney). GBP@1.30 and EUR@1.10 conversion applied.
- **Sources attempted but gated**: workatastartup.com continues to 403 headless fetches (represented via canonical ycombinator.com company job permalinks), app.welcometothejungle.com returned landing-page shells in the Oct-Nov window (most EU founding-engineer listings surfaced from Sept had already closed), jobs.techstars.com surfaced no fresh founding-track titles in-window, WorkInStartups.com detail gated by auth, LinkedIn returned auth-walled search shells. No fabricated data.
- **Exclusions applied**: fractional / interim CTO postings and post-Series-B / growth-stage / public-company CTO postings, per the ownership rule. One LuminOne wellfound posting (/jobs/4779217-co-founder-cto) surfaced again in the top-up window and was de-duplicated on URL match against 2026-10 post-A06.

**Tagging-consistency reconciliation**: the 2026-11 top-up sub-agent was prompted with the explicit strict-tagging rubric that 2026-10 flagged as a gap (T01 only on explicit stage/ladder framing, T26 only on explicit 'not CTO-in-name' / 'genuine co-founder' rejection language, T28 only on explicit week-level MVP deadlines). Under this tighter rubric, T01 was 0 on the fresh batch (confirming the 2026-10 over-tagging suspicion), T26 was tagged on 8 of 12 fresh postings (real signal — explicit 'genuine cofounder opportunity, not a traditional developer position' / 'true co-founder role' / dynamic-equity framing), and T28 was tagged on 3 of 12 fresh postings (consistent with the 2026-09 criterion). On the merged corpus T01 holds at 0.44, T26 climbs to 0.56, T28 steadies at 0.44. **The T26 climb to 0.56 under strict tagging is a genuine market signal** — not tagger drift — and warrants a watch-item: if a next-cycle reviewer judges that mod-101 exercise-04 reads too generically against the fresh JD language, a targeted mod-101 exercise forcing learners to diagnose a verbatim JD would be the right proposal. For this cycle: mod-101 ownership of T26 unchanged, no net-new content.

**Delta this cycle**: no net-new curriculum modules, exercises, or projects. All nine ≥0.30 themes already have an owner (mod-101: T01, T26; mod-102: T02; mod-103 AI-native slice: T18, T19; mod-104: T04; mod-106: T28; prereq ladder: T09; peer cpo-curriculum: T10). See [`.aicg/curriculum-plan-delta.json`](./.aicg/curriculum-plan-delta.json) for the empty-additions rationale, [`.aicg/job-requirements.json`](./.aicg/job-requirements.json) for the per-theme evidence, [`.aicg/research/runs/cto-2026-11/postings.compact.json`](./.aicg/research/runs/cto-2026-11/postings.compact.json) for the Oct-Nov top-up sample, [`.aicg/research/runs/cto-2026-10/postings.compact.json`](./.aicg/research/runs/cto-2026-10/postings.compact.json) for the fully-carried-forward 2026-10 top-up, and [`.aicg/research/runs/cto-2026-09/`](./.aicg/research/runs/cto-2026-09/) for the 2026-09 raw sample (15 of 39 remain in-window).

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

Frequency is `posting_count / 41`. The ≥0.30 net-new-content threshold requires ≥13 postings.

| # | Theme | Owner | Coverage | Frequency (n=41, 2026-11) | Δ vs 2026-10 |
|---|---|---|---|---|---|
| 01 | CTO role position on the ladder, stage-by-stage self-development plan | `cto` | mod-101 | **0.44 (18)** ✓ | -0.04 |
| 02 | Architecture under uncertainty — ADRs, C4, monolith-first, evolutionary architecture, ISO/IEC 25010 trade-offs | `cto` | mod-102 | **0.71 (29)** ✓ | +0.13 |
| 03 | Build-vs-buy and platform choices — cloud economics, vendor selection, AI-stack decisions | `cto` | mod-103 | 0.20 (8) | -0.03 |
| 04 | First engineering hires and team topology — hiring plan, interview loop, Team Topologies patterns | `cto` | mod-104 | **0.54 (22)** ✓ | +0.11 |
| 05 | Technical debt as a business decision — portfolio, cost-to-carry, refactor budget, deprecation vs. StranglerFig rewrite | `cto` | mod-105 | 0.05 (2)† | — |
| 06 | Scaling the org and the stack — 0 → 5 → 15 → 50 → 150 engineers transitions | `cto` | mod-106 | 0.12 (5) | -0.06 |
| 07 | Founder-scope security and compliance — SOC 2 Type I, GDPR / CCPA, HIPAA baseline, OWASP ASVS, SLSA, vendor DPA / BAA | `cto` | mod-107 | 0.24 (10)§ | +0.04 |
| 08 | CTO↔CEO relationship, board technical communication, technical due diligence | `cto` | mod-108 | 0.17 (7) | -0.01 |
| 09 | Python / TypeScript / cloud fluency at technical-co-founder depth | `ai-infra-junior-engineer` / `ai-infra-engineer` | prereq | **0.68 (28)** ✓ | +0.08 |
| 10 | Product discovery, roadmap, delivery-cadence fluency | `cpo-curriculum` | peer | **0.37 (15)** ✓ | -0.06 |
| 11 | CEO strategy, fundraising cadence, cap-table literacy | `founder-ceo-curriculum` | peer | 0.17 (7) | +0.04 |
| 12 | HR / people-ops / compensation / performance-management basics | `startup-operations-governance-curriculum` | peer | 0.24 (10) | -0.04 |
| 13 | Finance / runway / unit-economics basics | `startup-finance-fundraising-curriculum` | peer | 0.00 (0)‡ | — |
| 14 | GTM / enterprise-sales-motion basics | `startup-product-gtm-curriculum` | peer | 0.10 (4) | -0.05 |
| 15 | Delivery cadence, DORA four-key signals, blameless post-mortems | `cto` | mod-106 (slice) | 0.10 (4) | — |
| 16 | Day-two engineering-management craft (1:1s, career ladders, performance-management) | `ai-infra-team-lead` | peer | 0.05 (2) | -0.10 |
| 17 | Deep platform, distributed-systems, multi-region architecture beyond ~50 engineers | `ai-infra-senior-architect` / `ai-infra-principal-architect` | up | 0.02 (1) | -0.06 |
| 18 | AI-native platform decisions — foundation-model API vs. self-host, RAG / fine-tune / tool-use, inference cost economics | `cto` | mod-103 (AI-native slice) | **0.56 (23)** ✓ | -0.02 |
| 19 | Hands-on shipping of production LLM / agent product features (not demos) | `cto` (build-vs-buy) + `ai-infra-mlops` / `ai-infra-ml-platform` / `applied-ai-engineer` for shipping craft | mod-103 (AI-native slice) + peer | **0.49 (20)** ✓ | -0.04 |
| 20 | MLOps / model-lifecycle basics — evaluation, guardrails, fallbacks, monitoring, human-review paths | `ai-infra-mlops` | peer | 0.20 (8) | -0.03 |
| 21 | AI safety / responsible-AI hygiene at founder scale | `ai-risk-engineer` | peer + mod-107 slice | 0.10 (4) | -0.03 |
| 22 | Data privacy for AI — multi-tenant isolation, PII in prompts / logs, retention with foundation-model vendors | `cto` | mod-107 (privacy slice) + mod-103 (multi-tenancy) | 0.22 (9) | -0.03 |
| 23 | Enterprise-readiness — SSO / SAML / OIDC, SCIM, audit logs, ISO 27001 / SOC 2 as GTM enabler | `cto` | mod-103 (auth build-vs-buy) + mod-107 (compliance) + peer product-gtm | 0.10 (4) | — |

✓ = crosses the ≥0.30 net-new-content threshold — every one already has an owner (this repo or a peer track).
§ = T07 climbed under strict tagging on fresh Oct-Nov postings (MedTech FDA/QMS, fintech regulated-broker API, enterprise audit trails, creative-platform infra security). Still below threshold; monitor next cycle.
† = mod-105 retained despite low posting frequency because CTO Craft, Fournier, Larson, and Fowler all treat technical-debt framing as core CTO craft; the low frequency reflects JD blind spot, not curriculum irrelevance.
‡ = zero verbatim hits across three cycles reflects a persistent JD blind spot (founders/CEOs rarely name runway/unit-economics in the CTO JD even where the CTO opines on it), not curriculum irrelevance. Keep peer-linked.

## Emerging themes (threshold-crossing watch + below-threshold)

Third-cycle re-sampling confirmed every ≥0.30 theme already has a home. Under the strict-tagging rubric adopted in 2026-11, T01 fell to 0 on the fresh batch (confirming the 2026-10 over-tagging suspicion) while T26 (founder identity) continued to climb — a genuine market signal under tight tagging, not drift. See [`.aicg/job-requirements.json`](./.aicg/job-requirements.json) `emerging_themes_below_threshold` for full evidence per theme.

| Theme | 2026-11 Frequency (n=41) | 2026-10 Frequency (n=40) | Current coverage / recommendation |
|---|---|---|---|
| **Founder identity / equal-ownership expectation** — postings explicitly reject "CTO-in-name" or "senior hire" framing and demand a genuine co-founder | **0.56 (23)** ✓ | 0.43 (17) ⚠ | mod-101 lesson 01 (`cto-ladder-pre-seed-to-series-b.md`) + exercise-04 (`curriculum-scope-and-deferral-contract.md`) already teach the co-founder-vs-hire distinction. The +0.13 climb under strict 2026-11 tagging is a genuine signal (8 of 12 fresh postings explicitly reject CTO-in-name framing — Noesia, Logo Clothing Shop, GV Correct). **No new module or exercise this cycle** per the 'prefer citing existing content' rule, but flagged as the strongest watch-item: if a next-cycle reviewer judges mod-101 exercise-04 reads too generically against this fresh JD vocabulary, a targeted mod-101 exercise forcing diagnosis of a verbatim JD is the right proposal. |
| **0-to-1 shipping velocity / MVP-in-weeks** | 0.44 (18) ✓ | 0.43 (17) ⚠ | mod-102 (spikes with kill criteria) + mod-106 lesson 01 (`01-zero-to-five-first-process.md`) + exercise-01 (`exercise-01-zero-to-five-first-process-drill.md`) already teach the discipline. Under 2026-11 strict tagging only 3 of 12 fresh postings qualify (B02 Wethos "AI-native development speed", B06 Noesia "move extremely fast", B08 Plenaria "Build the MVP and the closed beta") — consistent with the 2026-09 criterion. **No new module or exercise this cycle.** If a next-cycle reviewer judges mod-106 exercise-01 reads too abstractly against fresh JD language, add a targeted mod-106 exercise defending a 2-4 week MVP cadence. |
| **AI-native engineering workflow fluency** — Claude Code, Cursor, Codex, MCP tools in daily hands-on use | 0.10 (4) | 0.15 (6) | Prereq-owned by ai-infra-engineer. Eased marginally as 2026-09 postings naming this theme aged out. Track in PREREQUISITES.md; the Wethos "rebuild your development workflow around AI" framing is the fresh signal to watch. |
| **Cost / FinOps for GPU / inference workloads** | 0.05 (2) | 0.05 (2) | Adjacent to mod-103 AI-native slice. Steady at 2 postings (Nixora infra abstraction + Aurify consumer-AI token-cost framing). Reference; do not expand. |
| **Open-source strategy as moat** | 0.02 (1) | 0.03 (1) | Adjacent to mod-103 and mod-108. Reference; do not expand. |
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

## Salary evidence (2026-11 cycle, n=41)

Cash disclosed on 15 postings; equity disclosed on 36 postings. USD conversion applied to GBP@1.30 and EUR@1.10. One Japanese (Aurify) and one Indian (Zintellix) posting show local-market cash bands well below US/UK/EU and should not be averaged with Western figures.

**Deliberately not aggregated across stages** — the Co-Founder / CTO market is bimodal (pre-funded technical co-founders with founder equity and near-zero cash vs. post-Series-A CTOs with market-rate cash and smaller equity) AND geo-stratified (US / EU / UK bands differ sharply from Asia / India / Japan bands).

| Stage | Cash-disclosed n | Cash range (USD) | Cash representative band | Equity notes |
|---|---|---|---|---|
| pre-seed | 4 | $0–$100K spread | Pre-seed pre-funding cash remains near-zero to $80K USD when disclosed; the four 2026-11 disclosures (DropIn $0, Plenaria $44K-$55K EU, Lumetra $70K-$80K Doha, TestAutomate $70K-$100K) confirm the pre-seed market stays cash-light / equity-heavy. Treat the 2026-09 cycle's ~$90K-$180K USD US pre-seed band as the aspirational post-funding band. | Co-founder equity continues to dominate — 28 of 30 pre-seed postings disclose equity, bimodal: genuine co-founder 10-50% (21 postings, up from 17) vs. senior founding-hire 0.5-1.5% (3 postings, stable). Several explicit equity-only / cash-at-revenue-milestones offers (DropIn $0 deferred; Wethos dynamic equity model; Noesia ~49.99%; Malkolm; LongRun; Anise 50%). |
| seed | 11 | $14K–$270K spread | ~$150K–$225K USD US / EU seed CTO cash band (median across the 9 US/EU disclosures — stable vs. 2026-10). The two 2026-11 Asia postings (Zintellix $14K-$22K India, Aurify $40K-$70K Japan) sit well below the US/EU band and reflect local-market calibration; include in geo-stratified analysis but exclude when quoting a US CTO benchmark. | Founding-engineer / early-CTO-hire equity typically 0.10-2.00%. YC / Otta seed cluster ~0.5-1.0% (Skoon, Otter Studio, IronLedger). Asia seed postings open wider (Zintellix 1-10%, Vi3W 1-10%); Thera declines to publish bands. |
| series-a | 0 | N/A | **N=0 FOR THE SECOND CONSECUTIVE CYCLE** — both 2026-09 Series-A postings aged out in 2026-10 and no new Series-A CTO postings were sampled in either the 2026-10 or 2026-11 top-up windows. Treat the pre-existing $180K-$300K US Series-A CTO band as informational only. Next cycle MUST actively re-prioritise Series-A sourcing — try YC Series-A graduates, Lenny's startup board, Techstars Series-A tracks, First Round Review referenced companies. | No Series-A equity data for the second consecutive cycle (n=0). |

Full ranges (verbatim, USD) in [`.aicg/job-requirements.json`](./.aicg/job-requirements.json) `salary_evidence.per_stage_ranges`.

---

<!-- aicg:maintained-by -->
Maintained by [VeriSwarm.ai](https://veriswarm.ai)
