# AI-Native Stack Decisions — Foundation Model, Architecture, and Data Posture

> The AI-native seed-stage CTO is making three coupled
> decisions at once: **which foundation model layer to
> depend on** (frontier API vs. cloud-hosted vs. open-weight
> self-host), **which architecture pattern to use** (RAG,
> fine-tune, tool-use, or a composition), and **what data
> posture to sign into with the vendor** (DPA, BAA,
> zero-retention, data-residency). Get one wrong and the
> other two are often forced into worse defaults.

## Motivation

For an AI-native startup, the model layer is one of the top
one or two lines on the cost curve, one of the top three
lines on the customer-perceived-latency budget, and — via
the DPA / BAA / data-residency posture — the pivot on which
the enterprise sales cycle either opens or shuts. It is also
the fastest-moving vendor market on the stack, with new
model releases and pricing revisions on roughly a monthly
cadence.

The temptation is to defer the model-layer decision to
"whatever OpenAI has this week", or to over-invest in
self-hosted infrastructure before the product-market fit
justifies the fixed cost. Both are visible failure modes
this chapter is written to prevent.

The frame is deliberately narrow: **the seed-stage CTO's
job on the AI-native stack**, not the full MLOps or ML
platform depth. The MLOps depth (training pipelines,
experiment tracking, feature stores, model registries)
lives in
[`ai-infra-mlops`](../../../ai-infra-mlops-learning) at
level 25, and the ML platform depth (inference platform,
GPU orchestration, model-serving frameworks) lives in
[`ai-infra-ml-platform`](../../../ai-infra-ml-platform-learning)
at level 30. This chapter is the *build-vs-buy* view on the
AI-native stack; the deeper "how do we operate a model
platform" material defers there.

## The three coupled decisions

Before walking any specific vendor, name the three coupled
decisions.

- **Decision A — the model layer.** Which family and which
  hosting posture for the primary foundation model? Options
  span (i) a frontier-API vendor (OpenAI, Anthropic, Google
  Gemini), (ii) a frontier model exposed through a
  hyperscale-cloud gateway (Azure OpenAI, AWS Bedrock, GCP
  Vertex AI), and (iii) an open-weight model hosted either
  on a specialist inference vendor (Together AI, Fireworks,
  Replicate) or on your own infrastructure (Hugging Face
  Text Generation Inference, vLLM on a GPU fleet).
- **Decision B — the architecture pattern.** How is the
  model integrated into the product? Options span RAG
  (retrieval-augmented generation), fine-tuning (SFT or
  preference tuning of a base model on your data),
  tool-use / agentic architectures (the model calls typed
  functions the product provides), or compositions of the
  above.
- **Decision C — the data posture.** What contract have you
  signed with the model vendor about your data? Does the
  vendor train on your prompts? Is there a Data Processing
  Agreement in place for GDPR? A Business Associate
  Agreement for HIPAA-covered use? A data-residency
  commitment for regulated jurisdictions?

Each decision moves the other two. Choosing a frontier API
(A) makes RAG (B) the natural pattern because you cannot
retrain the model; it makes the DPA / BAA / zero-retention
posture (C) something you negotiate rather than something you
own. Choosing open-weight self-host (A) makes fine-tuning
(B) the natural pattern; it makes the data posture (C)
something you own entirely, at the cost of the operational
burden of running the inference stack. Choosing the cloud
gateway (A) inherits the compliance posture of the cloud
(C), often the fastest path to enterprise-grade paperwork.

The rest of the chapter walks each decision in turn, then
returns to how they compose.

## Decision A — the model-layer options

### Frontier APIs — OpenAI, Anthropic, Google

The dominant option at seed for most AI-native products.
Vendors:

- **OpenAI** — API docs
  [platform.openai.com/docs](https://platform.openai.com/docs),
  pricing
  [openai.com/pricing](https://openai.com/pricing). The
  incumbent-of-mindshare; broad model family (chat,
  embedding, image, audio, function-calling, structured
  outputs).
- **Anthropic** — API docs
  [docs.anthropic.com](https://docs.anthropic.com/), pricing
  [anthropic.com/pricing](https://www.anthropic.com/pricing).
  Claude model family; strong on tool-use and structured
  output; enterprise-focused compliance track (SOC 2,
  HIPAA availability under BAA
  [anthropic.com/legal/hipaa](https://www.anthropic.com/legal/hipaa)).
- **Google Gemini** — API docs
  [ai.google.dev](https://ai.google.dev/), pricing
  [ai.google.dev/pricing](https://ai.google.dev/pricing).
  Gemini family via the direct Google AI Studio surface or
  via Vertex AI on GCP.

Economic and strategic properties:

- **Per-token pricing**, published, changing on the order of
  months. The token cost of a prompt-plus-completion is
  the first-order variable cost of every user request.
- **Zero-ops on the model itself.** No GPUs to run, no
  scaling to worry about, no model-file distribution.
- **No fine-tuning on your proprietary data at seed**
  (except where the vendor exposes a hosted fine-tune API,
  which is limited to specific models and comes with its
  own economics). RAG or prompt-engineering is the
  integration pattern.
- **Rate limits and quota.** Every frontier API has both
  per-minute rate limits and account-level quotas that
  the team must plan against. Bursty workloads (evals,
  large-scale batch generations) need to be paced or
  submitted via batch APIs (both OpenAI and Anthropic
  publish batch APIs at reduced per-token cost) rather
  than fired at the real-time surface.

### Cloud-hosted frontier — Azure OpenAI, AWS Bedrock, GCP Vertex

The middle option: the same or overlapping model catalogues,
delivered through a hyperscale-cloud gateway, inheriting the
cloud's compliance and IAM story.

- **Azure OpenAI Service** —
  [azure.microsoft.com/products/ai-services/openai-service](https://azure.microsoft.com/en-us/products/ai-services/openai-service)
  — OpenAI models delivered through Azure, with Azure's
  compliance posture (SOC 2, HIPAA, PCI-DSS,
  data-residency to the customer's chosen Azure region).
- **AWS Bedrock** —
  [aws.amazon.com/bedrock](https://aws.amazon.com/bedrock/)
  — a curated model catalogue (Anthropic Claude, Meta
  Llama, Mistral, Cohere, Amazon Titan, Amazon Nova,
  Stability, and others) delivered through AWS, with
  AWS's compliance posture and IAM.
- **GCP Vertex AI Model Garden** —
  [cloud.google.com/vertex-ai/generative-ai/docs](https://cloud.google.com/vertex-ai/generative-ai/docs)
  — Gemini, plus a curated set of open and partner models,
  delivered through Vertex AI on GCP.

Economic and strategic properties:

- **Compliance inherited from the cloud.** For a startup
  already on a hyperscale cloud, using the cloud's model
  gateway is often the fastest path to a compliance
  paperwork story an enterprise buyer accepts.
- **Data stays in your cloud account** (region-scoped),
  which is materially different from a frontier-API vendor
  where data crosses to a different account and network.
- **Model availability lags the direct API** — new model
  releases typically land on the direct vendor API first,
  and on the cloud gateway some period later.
- **Cost structure similar to the direct API**, sometimes
  discounted via cloud commit / credits (chapter 02) —
  worth negotiating.

### Open-weight and self-host

The third option: an open-weight model family (Meta Llama
via [llama.com](https://www.llama.com/), Mistral via
[mistral.ai](https://mistral.ai/), or Qwen / Gemma / DeepSeek
and their peers) served either from a specialist inference
vendor or from your own GPU fleet.

- **Specialist inference vendors** — Together AI
  ([together.ai](https://www.together.ai/)), Fireworks AI
  ([fireworks.ai](https://fireworks.ai/)), Replicate
  ([replicate.com](https://replicate.com/)), Modal
  ([modal.com](https://modal.com/)), Baseten
  ([baseten.co](https://www.baseten.co/)). They run the
  GPUs; you consume via API; per-token or per-GPU-hour
  pricing.
- **Self-hosted inference stacks** — vLLM
  ([docs.vllm.ai](https://docs.vllm.ai/)) and Hugging Face
  Text Generation Inference
  ([github.com/huggingface/text-generation-inference](https://github.com/huggingface/text-generation-inference))
  are the leading OSS inference servers. NVIDIA Triton
  ([developer.nvidia.com/triton-inference-server](https://developer.nvidia.com/triton-inference-server))
  is the widely-adopted vendor option. You provision GPU
  capacity (usually via a hyperscaler or a GPU-specialist
  vendor such as CoreWeave / Lambda / Crusoe), run the
  inference server, and manage the model files and the
  scaling.

Economic and strategic properties:

- **Data sovereignty.** Nothing leaves your infrastructure
  (or the inference vendor's, in the specialist case).
  This is the "we own the data posture entirely" option.
- **Fine-tuning is native.** Open-weight models can be
  fine-tuned on your data — SFT, LoRA / QLoRA
  ([arxiv.org/abs/2305.14314](https://arxiv.org/abs/2305.14314)
  is the QLoRA paper), preference tuning — without any
  vendor negotiation. This is the option that matters if
  the model *behaviour* is the moat.
- **Cost economics are workload-shape-dependent.** For
  low-throughput / bursty workloads, per-token pricing on
  a frontier API is often cheaper than the amortised cost
  of an under-utilised GPU. For high-throughput / steady
  workloads at scale, self-hosted or specialist inference
  can be materially cheaper — but the crossover point
  depends on model size, batching efficiency, and quality
  targets, and requires modelling with numbers from your
  actual traffic.
- **Operational burden is real.** GPU scheduling, model
  quantisation, batching, health checks, canary rollouts
  for model updates, evals — every one of these is a
  capability the team either builds or defers to
  [`ai-infra-mlops`](../../../ai-infra-mlops-learning)
  and [`ai-infra-ml-platform`](../../../ai-infra-ml-platform-learning).

### The three-layer summary

- **Frontier API** — highest leverage per engineer-hour,
  lowest operational burden, most-exposed to per-token
  pricing at scale, most-constrained on data posture.
- **Cloud-hosted frontier** — inherits cloud compliance,
  keeps data in your cloud account, moderate lag on model
  availability.
- **Open-weight self-host / specialist** — deepest control
  over data and behaviour, highest operational burden,
  economically favourable only at material sustained
  throughput.

The seed-stage default for most AI-native startups is **a
frontier API (or cloud-hosted frontier) for the primary
model layer, with an open-weight fallback path documented in
the ADR**. Chapter 06's scorecard formalises the fallback
path — instrument against a provider-abstract interface (see
below), keep the prompts / evals in a form portable across
providers, and know which open-weight family you would
migrate to under what triggering condition.

## Decision B — architecture pattern

### RAG — retrieval-augmented generation

Introduced by Lewis et al.'s 2020 paper *Retrieval-Augmented
Generation for Knowledge-Intensive NLP Tasks*
([arxiv.org/abs/2005.11401](https://arxiv.org/abs/2005.11401)),
RAG is the pattern in which the application retrieves
relevant context (from a vector store, a search index, or a
structured database) at query time and passes it into the
model as part of the prompt. The model does not need to have
been trained on your data; it needs to be able to read your
data at inference time.

- **When RAG fits.** The knowledge is proprietary,
  frequently changing, and needs to be citable back to a
  source. The model's *reasoning* is fine; you just need to
  give it the right facts. Most enterprise-search,
  documentation-Q&A, and knowledge-worker-assistant
  products are RAG-shaped.
- **What RAG needs.** A retrieval index (a vector database
  such as pgvector on Postgres, Pinecone
  [pinecone.io](https://www.pinecone.io/), Weaviate
  [weaviate.io](https://weaviate.io/), Qdrant
  [qdrant.tech](https://qdrant.tech/), or a plain BM25
  keyword index) and an ingestion pipeline that keeps the
  index in sync with the source of truth.
- **What RAG does not require.** Model training, fine-
  tuning, or GPU operation. It is the pattern most
  compatible with a frontier-API model layer.

### Fine-tuning — SFT, LoRA, preference tuning

Modifying the model weights on your data. Options include
supervised fine-tuning (SFT) on labelled examples,
parameter-efficient methods like LoRA / QLoRA that update a
small adapter rather than the full weights, and preference-
tuning methods (RLHF, DPO
[arxiv.org/abs/2305.18290](https://arxiv.org/abs/2305.18290))
that shape behaviour against human or model preferences.

- **When fine-tuning fits.** The desired model behaviour is
  hard to express in a prompt, or the domain is specialised
  enough that a base model needs to be adapted (specialised
  code, legal, medical, or scientific corpora). The
  behaviour, not the knowledge, is the moat.
- **What fine-tuning needs.** A labelled dataset (or a
  preference dataset), training infrastructure (a hosted
  fine-tune API on the frontier vendor or self-hosted GPU
  training), and an evaluation harness to prevent
  regressions.
- **What fine-tuning does not remove.** The need for RAG
  when the domain knowledge changes faster than the
  fine-tune cadence, or when the answer needs to be
  citable.

### Tool-use / agentic patterns

The application exposes typed functions (or a broader tool
protocol like Anthropic's Model Context Protocol
[modelcontextprotocol.io](https://modelcontextprotocol.io/))
that the model can call, and the application scaffolds a
loop that lets the model decompose a task into a sequence of
tool invocations. This is where the current wave of
autonomous-agent, coding-assistant, and workflow-assistant
products lives.

- **When tool-use fits.** The task requires interacting with
  the real world — querying a database, calling an API,
  running a computation, editing a file — rather than
  producing a single text response.
- **What tool-use needs.** A clear tool schema, a scaffold
  that manages the loop (planning, tool selection,
  execution, observation, retry, termination), and an eval
  harness that measures success across multi-turn
  interactions rather than single completions.
- **Where tool-use gets expensive fast.** Multi-step agents
  consume many model calls per user request. Latency and
  per-request cost both scale with the number of steps.
  This is the category where per-token economics matter
  most.

### Composition is the normal case

Most production AI-native systems are not one pattern; they
are RAG + tool-use (retrieve relevant context, then invoke
tools with that context), or fine-tune + RAG (a fine-tuned
base model that speaks the domain, retrieving up-to-date
facts at query time), or a router that dispatches to
different specialisms.

The seed-stage CTO's job on this decision is:

- **Start with the simplest architecture that could work.**
  Prompt-only → RAG → tool-use → fine-tune, in that order
  of increasing commitment. Each step forward requires
  justification.
- **Instrument the architecture with an eval harness from
  the first ship.** Without evals, you cannot say whether
  a change (a new model release, a fine-tune, a prompt
  rewrite) improved or regressed the product.
  [`ai-infra-mlops`](../../../ai-infra-mlops-learning) is
  the depth on this.

## Decision C — data posture

This is the decision that determines whether the enterprise
sales cycle opens or shuts. It has three sub-questions.

### Sub-question 1 — the DPA

The Data Processing Agreement (DPA) is the GDPR-required
contract between a *controller* (you) and a *processor* (the
vendor) that governs the processor's handling of personal
data. See
[gdpr.eu/what-is-gdpr](https://gdpr.eu/what-is-gdpr/) for
the vocabulary; see the EDPB's guidance
[edpb.europa.eu](https://www.edpb.europa.eu/) for the
authoritative interpretation. Every enterprise customer in
the EU (and increasingly the US and UK) will require you to
name your data sub-processors, which forces you to have a
signed DPA from each model vendor you route data through.

- OpenAI's DPA —
  [openai.com/policies/data-processing-addendum](https://openai.com/policies/data-processing-addendum/).
- Anthropic's DPA — via
  [anthropic.com/legal](https://www.anthropic.com/legal).
- Google Cloud's DPA (covers Vertex AI Gemini) —
  [cloud.google.com/terms/data-processing-addendum](https://cloud.google.com/terms/data-processing-addendum).
- AWS's DPA (covers Bedrock) —
  [aws.amazon.com/compliance/gdpr-center](https://aws.amazon.com/compliance/gdpr-center/).
- Microsoft's DPA (covers Azure OpenAI) —
  [microsoft.com/licensing/docs/view/Data-Protection-Addendum](https://www.microsoft.com/licensing/docs/view/Data-Protection-Addendum).

Get the DPA in place before the first enterprise prospect
asks. See [`mod-107`](../mod-107-founder-scope-security-and-compliance/)
for the depth on the DPA / vendor-DPA acquisition workflow.

### Sub-question 2 — the BAA (for HIPAA-covered use)

If the product handles Protected Health Information (PHI)
under HIPAA, every downstream vendor that touches PHI must
sign a Business Associate Agreement (BAA). The BAA is the
HIPAA contract that binds the processor to HIPAA's rules and
that puts the processor on the hook for breach notification.
This narrows the model-layer choice materially:

- **OpenAI** offers a BAA on its
  Enterprise API — see the API data-usage policy at
  [platform.openai.com](https://platform.openai.com/) and
  the enterprise-privacy page
  [openai.com/enterprise-privacy](https://openai.com/enterprise-privacy/).
- **Anthropic** offers a BAA — see
  [anthropic.com/legal/hipaa](https://www.anthropic.com/legal/hipaa).
- **Azure OpenAI** is HIPAA-eligible under Microsoft's BAA
  ([microsoft.com/trust-center/compliance/hipaa](https://www.microsoft.com/en-us/trust-center/compliance/hipaa)).
- **AWS Bedrock** is HIPAA-eligible under AWS's BAA
  ([aws.amazon.com/compliance/hipaa-compliance](https://aws.amazon.com/compliance/hipaa-compliance/)).
- **GCP Vertex AI** — Google publishes HIPAA-covered
  services at
  [cloud.google.com/security/compliance/hipaa](https://cloud.google.com/security/compliance/hipaa);
  check the current in-scope list before assuming.

Always check the vendor's current, canonical HIPAA / BAA
page — the coverage list changes as new services and models
launch. Do not rely on any snapshot.

### Sub-question 3 — data-residency

An enterprise buyer in the EU, in Canada, in Australia, or
under specific US federal requirements often wants a
commitment that data — at rest, in transit, and during model
inference — stays inside a specific region. The three
options for the model layer differ:

- **Frontier APIs** — OpenAI, Anthropic, Google — have made
  progressively stronger data-residency commitments for
  enterprise customers; check the vendor's current
  data-residency documentation before committing.
- **Cloud-hosted frontier** — Azure OpenAI, AWS Bedrock,
  GCP Vertex — inherit the cloud's region model. If Azure
  OpenAI is available in the EU region you need, the
  data-residency story is straightforward.
- **Open-weight self-host** — you choose the region
  entirely. This is the option that most trivially
  satisfies residency requirements, at the operational
  cost noted above.

### Zero-retention and training-opt-out

Distinct from residency, ask specifically whether the vendor
retains your prompts / completions and whether they train on
them. The frontier API vendors offer *zero-retention* and
*opt-out-of-training* modes on their enterprise tiers; the
consumer tiers do not always. Read the specific policy for
the specific tier you are on. The cloud-hosted frontier
services are usually zero-retention by default on the API
surface (check for the specific model and region).

## The composition — how the three decisions interact

The three decisions bind each other. Some common shapes:

- **B2B SaaS with enterprise ambitions, no PHI.** Frontier
  API (Anthropic or OpenAI) for the model layer, RAG plus
  optional tool-use for the architecture, DPA plus
  zero-retention plus opt-out-of-training for the data
  posture. Instrumented against a provider-abstract
  interface so the model layer is swappable if pricing
  moves. This is a common shape.
- **Healthcare, PHI-handling.** Cloud-hosted frontier
  (Azure OpenAI or AWS Bedrock) for the model layer, to
  inherit the BAA and the region posture; RAG over the
  PHI-safe store; the DPA / BAA in place with the cloud
  provider. If the cloud-hosted variant of the frontier
  model does not meet the quality bar, the fallback is
  a HIPAA-BAA-covered frontier API — validate the
  paperwork before committing.
- **AI-native product where model behaviour is the moat.**
  Open-weight self-host (or specialist inference vendor)
  for the model layer, fine-tuning plus RAG for the
  architecture, full data sovereignty. This is the
  posture that justifies the operational burden — the
  model behaviour is the differentiator you are
  investing in.
- **Consumer product with cost-per-user constraint.**
  Frontier API for the frontier-quality path, open-weight
  self-host or specialist inference for the volume path,
  with a router deciding which handles each request. The
  volume path is what makes unit economics work as user
  count grows.

## The provider-abstract interface

For any of the compositions above, instrument the
application layer against a provider-abstract chat / tool /
embedding interface — LangChain
([langchain.com](https://www.langchain.com/)) and LlamaIndex
([llamaindex.ai](https://www.llamaindex.ai/)) are the two
widely-used OSS options; the OpenAI-compatible chat schema
is a de-facto lingua franca that most model-serving vendors
now support. Instrumenting to a provider-abstract interface
does for the model layer what OpenTelemetry does for
observability and OpenFeature does for feature flags — it
keeps the backend swappable at the cost of a small
integration-layer investment now. This is the OSS-fallback
path chapter 06 asks for on every "buy" row of the matrix.

## Concrete example: the unit-economics reopening trigger

An AI-native seed-stage company ships v1 on a frontier API
(let us say GPT-4-class model, direct API). Product-market
fit lands; usage grows. Six months in, the finance model
shows that at the current per-user usage pattern, the
per-token cost is approaching a substantial share of gross
margin.

The team faces four levers, each with an ADR shape:

- **Reduce token usage per request** — prompt engineering,
  smaller context windows, more aggressive caching of
  identical completions. Cheapest to try; often gets
  meaningful improvement without changing the model layer.
- **Route the volume path to a cheaper model** — a smaller
  frontier model, or a strong open-weight model on a
  specialist inference vendor, with the frontier-quality
  model reserved for the high-value requests. This
  requires the router and the eval harness to prove the
  cheaper model meets quality.
- **Move the model layer to open-weight self-host** for the
  bulk of the volume. Requires the operational commitment
  and materially changes the cost structure from
  per-token-variable to GPU-fixed. Only economical above
  a sustained throughput floor.
- **Raise the price** — a product decision that either
  works or doesn't, but is worth naming as one of the
  levers.

The correct pattern is not "pick one now". It is: **the
reopening trigger for the model-layer ADR fires when the
per-user token cost crosses a modelled threshold**, at which
point the team runs a spike (per
[`mod-102` chapter 06](../mod-102-architecture-under-uncertainty/06-spikes-and-kill-criteria.md))
to evaluate the router-plus-cheaper-model option first
because it is the smallest architectural change. The
open-weight self-host path is the fallback, taken when the
router option is not sufficient.

## Common failure modes

- **Locking into one frontier vendor's proprietary
  primitives.** Building the product against a single
  vendor's function-calling shape, structured-output
  format, or provider-specific SDK such that swapping the
  model layer requires rewriting the application.
  Instrument against a provider-abstract interface.
- **No evals.** Adopting a model, a prompt, a RAG index, or
  a fine-tune without an eval harness that can tell you
  whether a change improved or regressed the product. This
  is the failure mode that turns model-layer changes into
  guesses. Defer the eval-harness depth to
  [`ai-infra-mlops`](../../../ai-infra-mlops-learning) but
  ship *some* eval from the first release.
- **DPA / BAA acquired only when the deal is in flight.**
  The enterprise buyer asks; the team scrambles; the deal
  slips. Get the DPA in place with every model vendor you
  route data through before you need it.
- **Modelling AI unit economics against the credits.**
  Startup credits from OpenAI, Anthropic, Azure, AWS, and
  GCP are real, but the same discipline as chapter 02
  applies: model post-credit pricing when you check unit
  economics.
- **Over-investing in self-hosted inference before
  throughput justifies it.** Standing up a GPU fleet
  because "self-hosted is cheaper" without the sustained
  volume that would make the amortised cost cheaper than
  per-token pricing. Model the crossover first.

## Where this defers up and sideways

- **MLOps depth** — training pipelines, feature stores,
  experiment tracking, model registries, eval harness
  frameworks —
  [`ai-infra-mlops`](../../../ai-infra-mlops-learning)
  (level 25).
- **ML platform depth** — inference platforms, GPU
  orchestration, model-serving frameworks, autoscaling —
  [`ai-infra-ml-platform`](../../../ai-infra-ml-platform-learning)
  (level 30).
- **AI-risk hygiene** — safe-behaviour evals, jailbreak
  resistance, red-teaming, RAI policy — peer to
  `ai-risk-engineer` (level 25, AI Governance family),
  cited in the module's
  [`README.md`](README.md).
- **Enterprise-grade compliance paperwork** — DPA / BAA
  acquisition workflow, SOC 2 Type II scope for AI
  systems — [`mod-107`](../mod-107-founder-scope-security-and-compliance/).

## Summary

- The AI-native seed-stage CTO is making three coupled
  decisions: **model layer (A)**, **architecture pattern
  (B)**, **data posture (C)**. Each moves the others.
- The model-layer options are **frontier API**,
  **cloud-hosted frontier**, and **open-weight self-host /
  specialist inference**. The seed-stage default for most
  products is frontier API (or cloud-hosted frontier),
  with an open-weight fallback path documented in the
  ADR.
- The architecture-pattern ladder is **prompt-only → RAG →
  tool-use → fine-tune**, in order of increasing
  commitment. Start at the simplest that works; step up
  with justification.
- The data-posture questions — **DPA, BAA, data-residency,
  zero-retention, training-opt-out** — decide whether the
  enterprise sales cycle opens or shuts. Get the DPA in
  place before the first enterprise prospect asks.
- Instrument against a **provider-abstract interface** to
  keep the model layer swappable. Ship *some* eval
  harness from the first release, even if the deep MLOps
  work defers to
  [`ai-infra-mlops`](../../../ai-infra-mlops-learning).
- The reopening trigger for the model-layer ADR is often
  **unit-economics-driven** — the per-user token cost
  crosses a threshold, at which point the router / cheaper-
  model / self-host levers get evaluated.

The chapter's paired exercise —
[`exercise-04-ai-native-stack-decision-foundation-model-vs-self-host.md`](exercises/exercise-04-ai-native-stack-decision-foundation-model-vs-self-host.md)
— walks the three coupled decisions for a specific
AI-native seed-stage product, ending with an ADR and a
scorecard entry that anchors the fallback path.
