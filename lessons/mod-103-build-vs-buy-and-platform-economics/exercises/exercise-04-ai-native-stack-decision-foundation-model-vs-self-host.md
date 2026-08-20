# Exercise 04 — AI-Native Stack Decision: Foundation Model vs. Self-Host

**Module:** `mod-103-build-vs-buy-and-platform-economics`
**Planned time:** ~3 hours
**Chapter this builds on:** [`04-ai-native-stack-decisions.md`](../04-ai-native-stack-decisions.md)

## Problem statement

For your (or a real reference) AI-native seed-stage
product, resolve the **three coupled decisions** from
chapter 04:

- **Decision A — model layer** (frontier API vs.
  cloud-hosted frontier vs. open-weight self-host /
  specialist inference).
- **Decision B — architecture pattern** (prompt-only vs.
  RAG vs. tool-use vs. fine-tune, or composition).
- **Decision C — data posture** (DPA / BAA /
  data-residency / zero-retention / opt-out-of-training).

Land the three coupled decisions in a coherent set of
artifacts: an ADR that captures the coupled call, a
scorecard row that names the fallback path, and an ADR-
level reopening trigger tied to your unit-economics or
compliance surface.

The point of the drill is to force the three decisions to
be reasoned about as *coupled*, not as three separate
picks each optimised in isolation. A frontier-API choice
(A) with fine-tuning as the architecture (B) is
inconsistent unless the fine-tune is via the vendor's own
hosted API; a self-hosted-model choice (A) with weak
data-posture reasoning (C) is throwing away the main
reason to self-host.

## Requirements

Produce a **coherent artifact bundle**:

1. A **decision writeup** (roughly two pages) covering
   the three coupled decisions, their rationale, and
   their coupling.
2. A **Nygard-format ADR** in `docs/adr/` capturing the
   model-layer decision, with the coupled architecture
   and data-posture choices named in the Context /
   Decision / Consequences sections.
3. A **scorecard-shaped table** (mini-version of the
   chapter-06 scorecard) with 2-3 model-layer options,
   scored against your specific criteria including the
   switching-cost / vendor-trajectory / OSS-fallback
   columns.
4. A **provider-abstract-interface note** — one paragraph
   naming the abstraction layer (LangChain, LlamaIndex,
   direct OpenAI-compatible API, custom) that keeps the
   model layer swappable.
5. A **unit-economics reopening-trigger note** — the
   observable condition that would force the ADR to be
   revisited.

### Part 1 — the decision writeup

Structure it in three sub-sections mirroring chapter 04:

**A — Model layer.** Which layer did you pick, from among:

- Frontier API (OpenAI / Anthropic / Google Gemini).
- Cloud-hosted frontier (Azure OpenAI / AWS Bedrock /
  GCP Vertex).
- Open-weight self-host / specialist inference (vLLM /
  TGI / Together / Fireworks / Replicate).

Give the one-paragraph rationale grounded in your
specific product's needs: quality bar, latency budget,
volume shape, compliance envelope, team's operational
capacity.

**B — Architecture pattern.** Which pattern (or
composition of patterns) did you pick, from among:

- Prompt-only.
- RAG (retrieval-augmented generation).
- Tool-use / agentic.
- Fine-tune (SFT / LoRA / preference tuning).

Explain the coupling to Decision A. If you picked a
frontier API in A, fine-tuning in B is limited to what
the vendor's hosted fine-tune API supports; if you
picked open-weight in A, fine-tuning is native but comes
with the training-infrastructure cost.

**C — Data posture.** Which of the following did you
address, and how:

- DPA in place with the model vendor (chapter 04 links
  the frontier vendors' DPA pages).
- BAA in place, if you handle PHI. If BAA is required,
  which frontier / cloud-hosted options remain in scope?
- Data-residency commitment — which region does inference
  happen in?
- Zero-retention / opt-out-of-training — which tier of
  which vendor gives you the posture you claim to have?

Every enterprise sales cycle you plan to run over the
next 12 months touches this section. Be specific about
which contracts must be in place by which point.

### Part 2 — the ADR

Author a full Nygard-format ADR in `docs/adr/` covering
Decision A, with the coupled B and C decisions surfaced in
the Context / Decision / Consequences. Requirements:

- **Title.** "Use $MODEL_LAYER for the primary
  foundation-model layer" or equivalent imperative
  statement.
- **Context.** Cover the three sub-decisions' inputs;
  cite specific vendor documentation with retrieval
  dates.
- **Decision.** One paragraph on the model layer; separate
  short paragraphs on the coupled architecture pattern
  and data posture.
- **Consequences.** Positive / Negative / Deferred. At
  minimum name the vendor-trajectory exposure, the
  per-token cost trajectory, the operational burden
  taken on (if any), and the compliance surface
  unlocked (or gated).
- **Reopening trigger.** The observable condition that
  would force a re-decision. Common triggers include a
  per-user token cost crossing a modelled margin
  threshold, a customer requirement the current posture
  cannot serve, or a model release that materially
  changes quality-per-dollar.

### Part 3 — the mini-scorecard

A 2-3 option scorecard (subset of the full chapter-06
scorecard) evaluating your top model-layer candidates
against criteria that include:

- Fit-for-purpose quality on your workload (score
  against evals, or note the eval gap explicitly).
- Cost per unit-of-work at your expected 12-month volume
  (from the vendor's published pricing; model
  post-credit).
- DPA / BAA / residency posture as it stands today.
- Switching-cost — engineer-quarters to move off.
- Vendor-trajectory risk — 24-36 month horizon.
- OSS-fallback path — is there an open-weight family
  you would migrate to, and how well-understood is the
  migration?

Weights sum to 100%. Reasoning behind weights is stated
in a paragraph under the table.

### Part 4 — the provider-abstract-interface note

One paragraph. Which abstraction layer keeps the model
layer swappable? Common answers:

- The OpenAI-compatible chat API is a de-facto standard
  supported by many providers.
- LangChain ([langchain.com](https://www.langchain.com/))
  or LlamaIndex
  ([llamaindex.ai](https://www.llamaindex.ai/)) as a
  higher-level abstraction.
- A custom-in-house interface that speaks to one vendor
  today but is designed to be swappable — with the
  swap actually spike-tested at least once (per
  [`mod-102` chapter 06](../../mod-102-architecture-under-uncertainty/06-spikes-and-kill-criteria.md)).

Note if you *didn't* pick an abstraction layer — that's a
real choice with its own consequences (deeper vendor
lock-in in exchange for shallower integration cost),
and it should be named.

### Part 5 — the unit-economics reopening trigger

One paragraph naming the observable, measurable
condition under which the ADR is superseded. This is
usually one of:

- Per-user token cost exceeds N% of gross margin at
  observed usage.
- Model-layer bill exceeds X% of monthly revenue.
- A customer contract's data-posture requirement
  (residency, BAA, retention) forces a change.
- A new model release materially changes the
  quality-per-dollar landscape.

Name a concrete metric, not "when it gets expensive".

## Starter guidance

- **Do not invent evals numbers.** If you don't have an
  eval harness yet, name the gap explicitly. The
  chapter-04 deferral to
  [`ai-infra-mlops`](../../../ai-infra-mlops-learning)
  covers the depth on evals; for this exercise,
  articulate the intended eval design even if the
  harness is a follow-up.
- **Do not invent pricing.** Use the vendor's current
  pricing page and cite the retrieval date. Model
  post-credit pricing when checking unit economics.
- **Do not pick self-host for aesthetic reasons.** The
  frame from chapter 04 is unit economics + data
  sovereignty + fine-tune-native + operational
  bandwidth. If two of the four are absent, self-host
  is likely the wrong call.
- **Do not skip the data-posture section because
  "we're not selling to enterprise yet".** The DPA / BAA
  posture is a lead-time-heavy question. Enterprises
  won't sign without it, and getting it in place takes
  months. Reason about it now.
- **The provider-abstract interface is cheap now and
  expensive later.** Instrument to it early even if the
  first swap isn't for a year.

## Acceptance criteria

Your artifact bundle is complete when a reader (a
co-founder, a technical advisor, a lead investor with
technical background, a technical due-diligence reviewer,
a first ML-adjacent hire) can:

- Read the decision writeup and understand the three
  coupled decisions and *why they are coupled* — not
  three isolated picks.
- Read the ADR and follow the model-layer decision to
  its reopening trigger, with the coupled architecture
  and data-posture choices visible.
- Read the mini-scorecard and see that the choice was
  scored against your criteria (including switching-cost,
  vendor-trajectory, and OSS-fallback columns) rather
  than against generic vendor marketing.
- Read the provider-abstract-interface note and see
  the concrete mechanism by which the choice remains
  swappable.
- Read the reopening trigger and know the specific
  observable that would force revisitation.

The output of this exercise updates the model-layer row of
your build-vs-buy matrix (exercise 01), links to the
scorecard in exercise 05 if the model-layer decision is
the one that becomes the full scorecard, and feeds into
the AI-native strand of
[`project-101`](../../../projects/project-101-first-year-technical-strategy-for-one-seed-startup)
when the capstone is scaffolded.
