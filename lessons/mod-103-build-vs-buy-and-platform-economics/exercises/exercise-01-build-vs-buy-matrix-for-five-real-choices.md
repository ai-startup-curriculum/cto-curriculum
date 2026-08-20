# Exercise 01 — Build-vs-Buy Matrix for Five Real Choices

**Module:** `mod-103-build-vs-buy-and-platform-economics`
**Planned time:** ~2 hours
**Chapter this builds on:** [`01-build-vs-buy-as-portfolio-decision.md`](../01-build-vs-buy-as-portfolio-decision.md)

## Problem statement

Author a one-page **build-vs-buy matrix** for your (or a
real reference) startup covering **five load-bearing
capabilities** the product depends on. Score each row on the
three portfolio axes from chapter 01 — leverage of buying,
moat, team-time economics — resolve each to a disposition
(build / buy / hybrid), and name the reopening trigger that
would force the row to be revisited.

The point of the drill is not to fill in a template. It is
to force the portfolio frame onto capabilities you currently
hold aesthetic views about, and to make the reasoning
legible to a reader (a co-founder, a first engineering
hire, a technical advisor, or a lead investor) who was not
part of the conversation.

## Requirements

Produce a **one-page matrix** (roughly one screen when
rendered), plus a **short accompanying paragraph** on the
one row you found hardest to resolve.

### The five rows

Choose **five** capabilities from the list below (or five
of equivalent scope specific to your product). The five
must span **at least three** of the categories — do not
pick five variations of one category.

Suggested picks (choose across categories):

- Identity / auth (see [`chapter 03`](../03-managed-vs-self-hosted-classic-categories.md#category-auth--identity))
- Payments / billing (see [`chapter 03`](../03-managed-vs-self-hosted-classic-categories.md#category-payments))
- Data warehouse / analytics (see [`chapter 03`](../03-managed-vs-self-hosted-classic-categories.md#category-data-warehouse))
- Observability (logs / metrics / traces)
- CI / CD
- Feature flags
- Foundation-model layer (see [`chapter 04`](../04-ai-native-stack-decisions.md))
- Cloud provider (see [`chapter 02`](../02-cloud-providers-as-economic-actors.md))
- Transactional email / notifications
- File / object storage
- Search / vector index
- Background-job substrate
- The domain-specific ML pipeline or workflow that is (or is candidate to be) your moat

For each of the five, the row must include:

- **Capability** — the noun. One line.
- **Disposition** — Build / Buy / Hybrid. Hybrid is only
  acceptable when the split responsibility is named (e.g.
  "buy the frontier-model API for the frontier-quality
  path, build the router that dispatches volume to a
  cheaper option").
- **Vendor / build note** — if buy, the specific vendor or
  managed service; if build, the one-line description of
  what you own.
- **Moat?** — Yes / No / Partial, with a one-line
  justification. If Yes or Partial, name specifically what
  the moat *is* (the algorithm, the dataset, the
  workflow, the compliance posture, the network effect).
- **Leverage of buying** — High / Medium / Low, with a
  one-line justification anchored in the specific
  capability the vendor provides that you would otherwise
  build.
- **Reopening trigger** — the specific, observable
  condition under which this row would be revisited. "When
  we grow" is not a trigger. "When per-transaction cost
  exceeds 4% of gross margin" is.

### The paragraph

After the table, write **200-400 words** on the single row
you found hardest to resolve. Answer:

- Why was it hard? Was the moat axis ambiguous (this is
  common for AI-native products where the model behaviour
  might or might not be the moat)? Was the leverage axis
  ambiguous (this is common for capabilities where a
  vendor and an OSS project are close in fitness)? Was
  the team-time axis ambiguous (this is common when the
  team has one person with strong opinions in a category
  where nobody else has operated the alternative)?
- What is the smallest observable thing that would resolve
  the ambiguity — a customer commitment, a bill trajectory,
  a stage transition, a specific hire?
- Is this row a candidate for a **spike** (per
  [`mod-102` chapter 06](../../mod-102-architecture-under-uncertainty/06-spikes-and-kill-criteria.md))
  before the disposition is committed? If yes, name the
  spike's success / kill criterion.

### Format

Produce the matrix as a Markdown table (see the chapter-01
example shape) checked into a real repo, in a
`docs/portfolio/build-vs-buy-matrix.md` or equivalent path.
The paragraph belongs in the same file, below the table.

## Starter guidance

- The matrix is a **portfolio view**, not an
  authoritative-recommendation view. Five rows, one page.
  If you find yourself writing paragraphs of context per
  row, that context belongs in the ADR, not on the matrix.
- Anchor each row to an ADR from
  [`mod-102` exercise 02](../../mod-102-architecture-under-uncertainty/exercises/exercise-02-adr-authoring-for-three-real-decisions.md).
  If a row has no ADR, the ADR is the follow-up artifact —
  name it in the row.
- For AI-native products, the model-layer row is almost
  certainly one of the five. Use chapter 04's three coupled
  decisions to reason about it and note the coupled
  architecture / data-posture consequences in the row.
- Cite the [ThoughtWorks Technology Radar](https://www.thoughtworks.com/en-us/radar)
  or [CNCF Landscape](https://landscape.cncf.io/)
  (chapter 05) as *one* input where relevant, not as the
  argument.
- Do not invent numbers. If you do not know the vendor's
  current pricing, write `<pricing: check current vendor
  page>` rather than a plausible-looking number. Same for
  latency, throughput, and any other claim you cannot
  verify.

## Acceptance criteria

Your matrix is complete when a reader (co-founder, first
engineering hire, technical advisor, lead investor doing
technical due diligence) can:

- Read the five rows and understand which capabilities you
  own, which you delegated, and — most importantly — *why*
  each was resolved that way, without asking a follow-up
  question.
- Identify at a glance which rows involve moat and which
  are commodity, and see that the team's time is
  concentrated on the moat rows.
- Read each reopening trigger and know the observable
  condition that would force a re-decision. No "we'll
  revisit later" columns.
- Read the paragraph and see that the CTO has honestly
  identified the row where the reasoning is weakest, and
  named the smallest next artifact that would resolve
  it.
- Cross-reference the matrix to at least two ADRs from
  the mod-102 exercise (or note the ADRs to be authored).

The output of this exercise feeds directly into every
subsequent exercise in this module:

- Exercise 02 goes deeper on the cloud-provider row.
- Exercise 03 goes deeper on three managed-vs-self-hosted
  rows.
- Exercise 04 goes deeper on the AI-native model-layer
  row.
- Exercise 05 authors the scorecard behind one specific
  vendor pick that this matrix identified.

The matrix also becomes an artifact in the capstone
[`project-101`](../../../projects/project-101-first-year-technical-strategy-for-one-seed-startup)
first-year technical-strategy package.
