# mod-103 — Build-vs-Buy, Vendor Selection, and Platform Economics

> How the pre-seed / seed CTO turns every "which vendor?"
> and "should we build this?" conversation into a
> portfolio call — legible to a co-founder, a first
> engineering hire, and a lead investor — instead of a
> series of aesthetic preferences accumulated one component
> at a time.

**Planned time:** 18 hours (6 chapters + 5 exercises + 1
lab + 1 quiz)
**Track:** [`cto-curriculum`](../../README.md) — Co-Founder
/ CTO, level 25
**Prerequisites:** [`mod-101`](../mod-101-cto-role-and-ownership-map/README.md)
(especially chapter 05 on the shared reading vocabulary),
[`mod-102`](../mod-102-architecture-under-uncertainty/README.md)
(especially chapter 02 on ADRs and exercise 02's
Bucket-B vendor ADR), and the engineering-craft
prerequisites in
[`PREREQUISITES.md`](../../PREREQUISITES.md).

## Learning objectives

- Frame build-vs-buy as a **portfolio decision** —
  leverage vs. moat vs. team-time economics — not an
  aesthetic or NIH judgement. Produce a build-vs-buy
  matrix an investor can read.
- Reason about **major cloud providers (AWS / GCP /
  Azure) as economic actors** — egress, reserved-capacity,
  credits programmes, lock-in risk, migration cost — not
  as a beauty contest.
- Choose between **managed vs. self-hosted for the
  classic categories** — data warehouse
  (Snowflake / BigQuery / Redshift vs. self-hosted),
  auth / identity (Auth0 / WorkOS / Clerk vs. self-hosted),
  payments (Stripe / Adyen / Braintree), observability
  (Datadog / Grafana Cloud / OSS stack), CI / CD
  (GitHub Actions / CircleCI / self-hosted), feature
  flags (LaunchDarkly / OSS).
- For **AI-native startups**: choose between
  foundation-model APIs (OpenAI / Anthropic / Google /
  Azure OpenAI / AWS Bedrock) vs. open-weight self-host;
  RAG vs. fine-tune vs. tool-use architecture; the
  inference-cost economics; the DPA / BAA /
  data-residency posture that unlocks enterprise sales.
  MLOps platform depth defers to
  [`ai-infra-mlops`](../../../ai-infra-mlops-learning)
  (level 25); ML platform depth defers to
  [`ai-infra-ml-platform`](../../../ai-infra-ml-platform-learning)
  (level 30).
- Read the **ThoughtWorks Technology Radar** and the
  **CNCF Landscape** as reference material — not as
  adopt-lists — and defend a technology choice with your
  own criteria.
- Author a **vendor-selection scorecard** that captures
  the cost of switching, the strategic risk of the
  vendor's own trajectory, and the OSS-fallback path.

## Chapters

1. [Build-vs-Buy as a Portfolio Decision](01-build-vs-buy-as-portfolio-decision.md) — leverage vs. moat vs. team-time economics; the investor-legible one-page matrix.
2. [Cloud Providers as Economic Actors](02-cloud-providers-as-economic-actors.md) — AWS / GCP / Azure pricing structure, egress, reserved capacity, credits, lock-in taxonomy, migration cost.
3. [Managed vs. Self-Hosted Across the Classic Categories](03-managed-vs-self-hosted-classic-categories.md) — data warehouse, auth, payments, observability, CI/CD, feature flags — the category-specific decision-forcing questions.
4. [AI-Native Stack Decisions — Foundation Model, Architecture, and Data Posture](04-ai-native-stack-decisions.md) — the three coupled decisions the AI-native CTO makes at once; provider-abstract interface; the DPA / BAA / residency posture that unlocks enterprise sales.
5. [Reading the ThoughtWorks Technology Radar and the CNCF Landscape as References](05-radar-and-cncf-landscape-as-references.md) — how to consume the industry references correctly, and how not to.
6. [The Vendor-Selection Scorecard — Switching Cost, Vendor Trajectory, OSS Fallback](06-vendor-selection-scorecard.md) — the resolution artifact for every "buy" row; the three non-negotiable columns; annual re-run rhythm.

## Exercises

1. [Build-vs-Buy Matrix for Five Real Choices](exercises/exercise-01-build-vs-buy-matrix-for-five-real-choices.md) — ~2 hours. One-page portfolio matrix for five load-bearing capabilities, disposition + reopening trigger per row.
2. [Cloud-Provider Economic Comparison](exercises/exercise-02-cloud-provider-economic-comparison.md) — ~2.5 hours. Structured AWS / GCP / Azure comparison against a specific workload profile, landing in an ADR with a reopening trigger.
3. [Managed vs. Self-Hosted Drill for Three Categories](exercises/exercise-03-managed-vs-self-hosted-drill-for-three-categories.md) — ~2.5 hours. Three category writeups + three ADRs, plus a switching-cost paragraph each.
4. [AI-Native Stack Decision — Foundation Model vs. Self-Host](exercises/exercise-04-ai-native-stack-decision-foundation-model-vs-self-host.md) — ~3 hours. The three coupled decisions worked as a coherent bundle: ADR + mini-scorecard + provider-abstract-interface note + reopening trigger.
5. [Vendor-Selection Scorecard Authoring](exercises/exercise-05-vendor-selection-scorecard-authoring.md) — ~2 hours. Full scorecard for one real vendor decision, including the non-negotiable switching-cost / vendor-trajectory / OSS-fallback columns, closing the matrix → ADR → scorecard artifact chain.

## Lab

- `lab-01-vendor-strategy-package-for-your-startup` (~2
  hours) — planned. Bundles the build-vs-buy matrix
  (exercise 01), the cloud ADR (exercise 02), the three
  category ADRs (exercise 03), the AI-native artifact
  bundle (exercise 04), and the full scorecard (exercise
  05) into a single reviewable **vendor-strategy
  package** the CTO can walk a technical advisor, a
  first engineering hire, or a lead investor through.
  Scaffolded from the exercise outputs once the paired
  prompt is authored.

## Quiz

- One quiz (~30 min) covering: the three portfolio axes
  (leverage / moat / team-time), the egress trap and the
  hyperscale lock-in taxonomy, the category-specific
  decision-forcing questions for at least three of the
  classic categories, the three coupled AI-native
  decisions (model layer / architecture / data posture),
  the three-line test for Radar / Landscape citations,
  and the three non-negotiable scorecard columns.

## Resources

See [`resources.md`](resources.md) for the module's primary
references. Full citations for the whole curriculum are in
[`.aicg/job-requirements.json`](../../.aicg/job-requirements.json)
under `authoritative_references`.

## What comes next

Once you have completed the exercises here,
[`mod-104`](../mod-104-first-engineering-hires-and-team-topology)
(*First Engineering Hires and Team Topology*) is the
natural next module — every "build" disposition on the
build-vs-buy matrix has a hiring consequence, and the
hiring plan mod-104 asks you to author is built against
the matrix from exercise 01. The vendor-strategy package
this module produces also feeds directly into the
capstone
[`project-101`](../../../projects/project-101-first-year-technical-strategy-for-one-seed-startup),
which integrates the mod-101 → mod-104 outputs into a
single first-year technical-strategy artifact.
