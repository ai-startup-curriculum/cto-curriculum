# The Startup-Track Pathway Coverage Map — Where This Packet Ends, Where Each Peer Track Begins

## Motivation

The Co-Founder / CTO job at a real startup is not shaped like a
neat set of engineering-leadership modules. On any given Tuesday
the CTO is asked about the pricing model (Product / GTM), the
runway model (Finance), the offer letter for the second engineer
(People), the board pre-read framing (CEO / Strategy), *and*
the choice of foundation-model API (Technical Leadership). No
single curriculum covers all of that at depth.

The AI Startup pathway is deliberately organised as **six peer
role-tracks over one shared foundation**, not as one giant
"startup curriculum". Each track owns one pillar of the job at
depth and links out to peer tracks for the pillars it does not
own. This chapter is the map — so you can defend, in a
conversation with a co-founder or an investor, where *this*
repo's coverage ends and where each of the peer tracks picks up.

The canonical version of this map lives in this repo's
[`CURRICULUM.md`](../../CURRICULUM.md) coverage table and in
[`JOB_REQUIREMENTS.md`](../../JOB_REQUIREMENTS.md) "Requirement
themes" section. This chapter walks it — and defends the
boundaries — so that the map becomes something the CTO can
*use*, not just something they've seen.

## The shared foundation

Every startup-track pathway assumes the reader has already been
through, or is actively working through,
[`startup-foundations`](https://github.com/ai-startup-curriculum/startup-foundations).
That repo owns:

- Company formation (US Delaware C-corp basics, other-jurisdiction
  pointers).
- The stage vocabulary (`IDEA → PRE-SEED → SEED → SERIES-A →
  GROWTH → MATURE`) that this curriculum uses on every page.
- The `FUNCTIONAL_CURRICULA.md` pillar map that assigns
  coverage percentages to each role-track.
- Unit-economics fundamentals (CAC, LTV, gross margin, contribution
  margin, payback period).

If any of the above is unfamiliar, work through the shared
foundation before continuing here — the material in mod-102
through mod-108 assumes it.

## The seven pillars and who owns which

Reproduced from [`CURRICULUM.md`](../../CURRICULUM.md) so this
chapter can walk it:

| Pillar | Coverage in this repo | Owning peer track |
|---|---|---|
| Foundations | 100% (via prereq) | [`startup-foundations`](https://github.com/ai-startup-curriculum/startup-foundations) |
| Technical Leadership | 100% | this repo |
| Product | 70% | [`cpo-curriculum`](https://github.com/ai-startup-curriculum/cpo-curriculum) |
| People | 70% | [`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum) |
| Strategy | 40% | [`founder-ceo-curriculum`](https://github.com/ai-startup-curriculum/founder-ceo-curriculum) |
| Finance | 30% | [`startup-finance-fundraising-curriculum`](https://github.com/ai-startup-curriculum/startup-finance-fundraising-curriculum) |
| GTM / Sales | 30% | [`startup-product-gtm-curriculum`](https://github.com/ai-startup-curriculum/startup-product-gtm-curriculum) |
| Governance | 30% | [`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum) |

Read the percentages as *"how much of this pillar this
role-track teaches at depth"* — not as "how much of this pillar
the CTO ignores". A CTO who ignores 70% of Finance will fail. A
CTO who *consumes* 70% of Finance from the finance track, and
learns from this repo the 30% they need to *own* (mostly:
runway-vs-hiring-plan and unit-economics-of-the-stack), is
correctly sequenced.

## Where this packet ends, per peer track

The four boundary walks below are the ones a CTO needs to be
able to defend in a real cofounder or investor conversation.

### CTO ↔ CPO (`cpo-curriculum`)

- **This repo owns** — the engineering-side of the delivery
  contract with Product: architecture that stays cheap to change
  (mod-102), the build-vs-buy call on each platform component
  (mod-103), the delivery cadence and DORA-flavoured measurement
  (mod-106), and the technical-debt portfolio that Product will
  either love or ignore (mod-105).
- **`cpo-curriculum` owns** — product discovery, roadmap
  authoring, prioritisation frameworks, experimentation craft,
  pricing and packaging strategy, and the day-two PM job.
  Cagan's *Inspired* and *Empowered* are the canonical
  references.
- **The seam** — the CTO ↔ CPO handshake is the weekly
  planning rhythm plus the roadmap-vs-architecture review. The
  CTO does not write the roadmap; the CPO does. The CTO does
  make each roadmap item architecturally realistic, and calls
  out when a proposed roadmap item is architecturally
  incompatible with what already exists.
- **Common failure mode** — CTO tries to own product too and
  crowds out the CPO; or CPO tries to own delivery too and
  crowds out the CTO. Both are visible in the calendar within
  two weeks.

### CTO ↔ CEO (`founder-ceo-curriculum`)

- **This repo owns** — the CTO's *end* of the relationship:
  decision-rights map (mod-108), board pre-read authoring
  (mod-108), technical narrative that ties into the CEO's
  fundraising story (mod-108), technical due-diligence data
  room preparation (mod-108), and the co-founder dispute
  mechanic before it is needed (mod-108).
- **`founder-ceo-curriculum` owns** — the CEO's *end*: the
  fundraising narrative construction, cap-table strategy, term
  sheet negotiation, board management as CEO, hiring
  executives, capital allocation, and the CEO's version of the
  weekly-1:1 with the CTO.
- **The seam** — the mod-108 decision-rights map is authored
  jointly and reviewed quarterly. The CTO cannot draft the CEO's
  half; the CEO cannot draft the CTO's half; both are stronger
  when the two tracks are read side-by-side.

### CTO ↔ Head of People / Ops (`startup-operations-governance-curriculum`)

- **This repo owns** — the CTO's first hiring decisions
  (mod-104: hiring plan against roadmap and runway, interview
  loop, founding-engineer profile, career-ladder v0), Team
  Topologies for engineering (mod-104), and the engineering-org
  security-and-compliance posture (mod-107).
- **`startup-operations-governance-curriculum` owns** — HR /
  people-ops depth (leveling and comp philosophy across the
  whole company, benefits, performance-management processes,
  employee handbook, immigration where relevant), corporate
  governance (equity plan administration, board resolutions,
  cap-table hygiene from the Secretary's-office side), and the
  day-two "how do we handle the difficult conversation the
  first-time EM does not know how to handle" craft.
- **The seam** — the CTO owns the *first* eng-org shape (roles,
  interview loop, career ladder v0). Ops owns the *company-wide*
  people-ops function once it justifies its own hire. The
  handoff is the moment the company hires its first non-CTO
  people function; both tracks should be read alongside for
  that transition.

### CTO ↔ CFO / Head of GTM (`startup-finance-fundraising-curriculum`, `startup-product-gtm-curriculum`)

- **This repo owns** — the *engineering-cost-model* slice of
  finance (runway-informed hiring plan in mod-104, cost-to-carry
  sizing in mod-105, cloud economics in mod-103), and the
  *technical-hygiene-that-unlocks-enterprise-deals* slice of
  GTM (SOC 2 Type I readiness, vendor DPA / BAA acquisition,
  security-review response in mod-107).
- **`startup-finance-fundraising-curriculum` owns** — the
  full FP&A craft (financial model, cap table, SAFE / priced-
  round mechanics, budget cycle, unit-economics deep-dive),
  the fundraising process from the finance angle, and the CFO
  seat's contribution to board work.
- **`startup-product-gtm-curriculum` owns** — the sales-motion
  craft (PLG vs. enterprise, ICP definition, sales-cycle
  design, pricing strategy, deal-desk mechanics), marketing,
  and demand-gen.
- **The seam** — the CTO consumes both tracks *shallowly* and
  routes any real depth-question to the owning track's owner
  (or, at pre-seed, back to the CEO who is wearing both hats).

## Where higher-level tracks pick up

At Series-B+ (rung (d) from chapter 01), the CTO's problem set
graduates *upwards* — the deep architectural, principal-engineer,
and executive-scope material lives in higher-level tracks.
Chapter 04 walks the exact sequencing; the map at a glance:

- Deep multi-region / multi-tenant / high-scale architecture →
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) and
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55).
- Principal-engineer craft (individual-contributor at the highest
  altitude) →
  [`ai-infra-principal-engineer`](../../../ai-infra-principal-engineer-learning)
  (level 50).
- AI-org executive scope at C-suite →
  [`chief-ai-officer`](../../../chief-ai-officer-learning)
  (level 70).
- Deep M&A / integration / secondary-transaction scope →
  `startup-exit-curriculum` (level 40).

## Where sideways engineering tracks pick up

The AI-native CTO consumes several peer engineering tracks at
depth *without* owning them:

- Day-two engineering-management craft (1:1s, feedback loops,
  performance management, difficult conversations) →
  [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (level 30). The CTO hires or promotes into this craft rather
  than living inside it long-term.
- MLOps / ML platform depth for AI-native startups →
  [`ai-infra-mlops`](../../../ai-infra-mlops-learning) (level 25)
  and [`ai-infra-ml-platform`](../../../ai-infra-ml-platform-learning)
  (level 30). The CTO makes the build-vs-buy and platform-selection
  calls (mod-103); those tracks own the depth.
- AI safety / risk engineering the AI-native CTO adopts at
  founder scope → `ai-risk-engineer-learning` (level 25, AI
  Governance family). Mod-107 covers only the founder-scope
  hygiene slice.

## Out of scope for the entire startup-track pathway

Three things the whole pathway defers to specialist advisors,
not to a peer track:

- **Legal opinion** — the CTO (and every other role in the
  pathway) briefs counsel with a defensible package. Counsel
  delivers the legal opinion.
- **External audit attestation** — the CTO owns SOC 2 /
  ISO 27001 *readiness and evidence*. The CPA firm delivers
  the attest opinion (see mod-107).
- **Specialist advisor scope** — patent strategy, immigration,
  tax, PR crisis, and executive coaching all live outside the
  curriculum and route to specialists.

## Summary

- Six peer role-tracks + one shared foundation. This repo
  owns 100% of Technical Leadership and consumes shallow
  slices of the other pillars from the peer tracks.
- The four boundary walks — CTO ↔ CPO, CTO ↔ CEO, CTO ↔
  Ops, CTO ↔ CFO / Head of GTM — are the ones a CTO must
  be able to defend in a real cofounder or investor
  conversation.
- Higher-level tracks (`ai-infra-senior-architect`,
  `ai-infra-principal-architect`, `chief-ai-officer`,
  `startup-exit-curriculum`) pick up the Series-B+ scope
  this repo does not own. Sideways tracks
  (`ai-infra-team-lead`, `ai-infra-mlops`, `ai-infra-ml-platform`,
  `ai-risk-engineer`) own depth the AI-native CTO consumes.
- Legal opinion, external audit attestation, and specialist
  advisor scope live outside the whole pathway and route to
  specialists.

The exercise for this chapter —
`exercise-04-curriculum-scope-and-deferral-contract.md` —
asks you to draft the deferral contract for your own startup:
a one-page document naming which peer / higher-level tracks
your company's other people (co-founder, first hires, board
members) should be reading, and which questions you will
route out of the CTO seat rather than answering yourself.
