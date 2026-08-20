# The Vendor-Selection Scorecard — Switching Cost, Vendor Trajectory, OSS Fallback

> The scorecard is the resolution artifact for every "buy"
> row on the chapter-01 matrix. It names the criteria that
> actually decide the choice, weights them by your specific
> situation, forces a per-option evaluation against those
> criteria, and — most importantly — captures the
> switching cost, the vendor's own strategic trajectory,
> and the open-source fallback path. Without those three
> columns, the scorecard is a feature-matrix, not a
> decision instrument.

## Motivation

Chapters 01–05 established the frame, the categories, the
AI-native shape, and how to read the industry references.
This chapter is where the concrete choice lands.

The scorecard is the paperwork the CTO uses to defend a
vendor selection — to a co-founder, to a first engineering
hire, to a technical advisor, to a due-diligence reviewer.
Its job is not to be right. Its job is to make the choice
*legible* — legible enough that the reader can follow the
reasoning, disagree specifically rather than generically,
and see what would have to change to force a re-decision.

Feature-comparison matrices are common online (any vendor
publishes one comparing themselves favourably to their
competitors). The scorecard adds three columns that the
vendor's own comparison matrix will not include:

- **Switching cost.** What would it actually take to move
  off this vendor if we decided to?
- **Vendor-trajectory risk.** How likely is the vendor's
  own strategic direction to diverge from ours over the
  next 24-36 months, and what would happen if it did?
- **OSS fallback path.** Is there an open-source or
  open-standard alternative we could migrate to, and how
  wide is the gap we would have to close?

Those three columns are what turn a vendor comparison into
a *risk-adjusted* choice. The rest of this chapter is how to
build the scorecard, how to weight it, and how to keep it
alive as a decision instrument.

## The shape of the scorecard

A workable shape for the scorecard is a Markdown table in
the same repo as the ADR (per
[`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md)),
linked from the ADR context section. One scorecard per
category, one row per candidate option, one column per
criterion.

```
| Criterion                       | Weight | Option A: WorkOS | Option B: Auth0 | Option C: Self-hosted Keycloak |
|---------------------------------|--------|------------------|-----------------|--------------------------------|
| Fits our B2B SSO/SCIM need this quarter |  25%   | 5 (per-connection pricing) | 4 (per-MAU on enterprise tier) | 3 (SSO/SCIM works but requires setup) |
| DPA + SOC 2 Type II available   |  15%   | 5                | 5               | 3 (we operate, we attest)      |
| Fits our per-MAU cost envelope at expected 12-month growth | 15%    | 5                | 3               | 5 (no per-MAU fee)             |
| Time-to-integration (engineer-weeks)                       | 10%    | 4                | 5               | 2                              |
| Team has operated this class of system before              | 10%    | 4                | 4               | 2                              |
| Switching cost (engineer-quarters to move off)             | 10%    | 3                | 3               | 4                              |
| Vendor-trajectory risk (24-36mo)                           |  8%    | 4                | 3 (post-Okta)   | 5                              |
| OSS fallback / standard-based portability                  |  7%    | 3 (OIDC standard) | 3 (OIDC standard) | 5 (Keycloak itself is the OSS) |
| **Weighted total**                                         | 100%   | **4.3**          | **3.9**         | **3.5**                        |
```

The specific scores in the table above are illustrative.
The actual scores must come from your situation. Two things
about the shape:

- **Weights sum to 100%.** Forcing yourself to spend the
  budget is what surfaces the honest priority. If you
  cannot decide whether Criterion X is 10% or 15%, ask
  what you would trade another 5% away from.
- **The three "extra" columns —
  switching cost, vendor-trajectory risk, OSS fallback —
  are always present**, even when they are low-weight,
  because their absence would leave a decision with no
  risk model.

The rest of this chapter walks each of the three extra
columns in depth.

## The switching-cost column

Switching cost is the sum of the work it would take, in
engineer-effort and elapsed time, to move off this vendor
onto a comparable substitute. It has multiple sub-components:

- **Data migration.** Moving the data (user records, event
  history, warehouse tables, media assets, embeddings)
  from this vendor to another. Egress cost (chapter 02),
  data-transformation code, downtime or dual-write
  windows.
- **Integration re-plumbing.** Replacing SDK calls, webhook
  handlers, and vendor-specific primitives with the
  substitute's equivalents. Non-linear when the vendor's
  primitives are deep — Stripe Connect and Stripe Billing
  are much harder to replace than Stripe's basic card
  charge; Datadog dashboards are harder to replace than
  Datadog metric ingestion.
- **Compliance re-attestation.** Signing new DPAs / BAAs
  with the substitute vendor, updating your privacy
  policy and sub-processor list, re-checking SOC 2 audit
  scope. See [`mod-107`](../mod-107-founder-scope-security-and-compliance/)
  on the compliance re-attestation workflow.
- **Team re-training.** The team's tacit knowledge of the
  incumbent vendor's console, alerting model, cost
  structure, and edge cases resets. This is not free,
  even if the substitute has "better" primitives on paper.
- **Customer-perceptible surface change.** If the vendor
  is behind an outward-facing surface (a payment page,
  a login screen, a search box), the switch will be
  visible to users. Any customer confusion, support
  ticket volume, or regression risk becomes part of the
  cost.

Score the column on the scorecard using a rough
engineer-quarter denominator: a **5** is "we could swap
this in a week"; a **3** is "one engineer-quarter"; a **1**
is "one or more engineer-years". You will underestimate;
double what your first estimate gave you and score against
the doubled number.

The switching-cost column also anchors the reopening
trigger. A row with switching cost **1** (very hard to
move) should have a correspondingly *high* bar for
reopening the ADR — the cost of the move is what would
justify absorbing considerable vendor friction before
triggering it. A row with switching cost **5** (easy to
move) can be reopened readily when a better option emerges;
the vendor is functionally interchangeable.

## The vendor-trajectory-risk column

A vendor is a business. It has its own strategy, its own
investors, its own segment focus, and its own life-cycle.
Over any 24-36 month window, several things can happen
that materially change the calculus:

- **Acquisition.** The vendor is bought by a larger
  company whose strategy differs — the pricing model
  changes, the segment focus shifts, favoured integrations
  are deprecated. Auth0's acquisition by Okta
  ([businesswire.com — Okta announces close](https://www.businesswire.com/news/home/20210503005357/en/Okta-Completes-Acquisition-of-Auth0))
  is one widely-cited example; the ecosystem is full of
  similar cases. When your vendor is acquired, the
  scorecard row you filled out under the old ownership
  may not be accurate under the new.
- **Pricing revision.** A vendor changes its pricing tiers,
  adds a per-usage line item, removes a free-tier
  capability, or moves a feature you rely on to a higher-
  cost tier. HashiCorp's licence change to the Business
  Source License in 2023
  ([hashicorp.com/blog/hashicorp-adopts-business-source-license](https://www.hashicorp.com/blog/hashicorp-adopts-business-source-license))
  and Elastic's earlier licence change in 2021
  ([elastic.co/blog/why-license-change-aws](https://www.elastic.co/blog/why-license-change-aws))
  are two widely-discussed cases where a licence /
  business-model shift by the vendor materially changed
  the trade-off for downstream users. Both were resolved
  in the ecosystem by forks (OpenTofu
  [opentofu.org](https://opentofu.org/) forking Terraform
  under the Linux Foundation; OpenSearch
  [opensearch.org](https://opensearch.org/) forking
  Elasticsearch under the AWS-founded Foundation) — the
  existence of a forked path is itself a scorecard input.
- **Segment pivot.** The vendor decides its future growth
  is in enterprise, deprecates the developer-tier or the
  small-team tier, and reworks the product accordingly. Or
  the reverse — a vendor once focused on enterprise
  simplifies for prosumers and drops the SLA / support
  posture your enterprise customers require.
- **Business collapse.** The vendor fails to raise, gets
  acquired for the technology at a discount, or shuts
  down. Small SaaS vendors are more exposed than
  category-defining incumbents; both happen.
- **Product deprecation.** The vendor keeps the business
  but sunsets the specific product line you depend on.
  Common when the vendor pivots its own portfolio.

Score the column on the scorecard against a rough
"probability of a materially adverse change × severity of
that change to us" mental model. A **5** is "the vendor is
category-defining, publicly-traded, and its trajectory
aligns with our segment for the foreseeable future"; a **3**
is "some risk of a segment pivot or acquisition event"; a
**1** is "we are one of very few customers on a specific
tier that the vendor could deprecate at any time".

Signals to look at when scoring:

- **The vendor's funding stage and public trajectory.**
  Public companies are more stable in the short-run but
  are more exposed to activist-investor-driven pricing
  changes. Late-stage private companies are under
  pressure to grow into their valuations, which often
  manifests as pricing changes. Seed-stage vendors can
  disappear.
- **The vendor's customer concentration.** A vendor whose
  revenue is heavily concentrated in one segment (which
  may or may not be yours) is more likely to reshape the
  product around that segment.
- **The vendor's public statements about strategy.**
  Blog posts, earnings calls (for public companies),
  founder interviews. Slow-burning strategy shifts are
  often visible for a year before they hit the product.
- **The vendor's history of customer-hostile changes.**
  Past behaviour is the best predictor of future
  behaviour on this axis. A vendor that has moved a
  capability to a paid tier once is more likely to do it
  again.

## The OSS-fallback column

The OSS-fallback column asks a specific question: **if the
vendor became unacceptable (any of the trajectory risks
above), what is the open-source or open-standard path we
would take, and how wide is the gap we would have to close?**

Some categories have a native OSS fallback:

- **Identity.** OpenID Connect is the standard; Keycloak
  ([keycloak.org](https://www.keycloak.org/)) or Ory
  Kratos ([ory.sh](https://www.ory.sh/)) is the OSS
  server. Migration from a compliant SaaS vendor is
  a real project but not a category shift.
- **Observability.** OpenTelemetry
  ([opentelemetry.io](https://opentelemetry.io/)) is the
  instrumentation standard; Grafana + Prometheus + Loki +
  Tempo is the OSS backend. Migration is a re-plumbing
  of the backend, not of the application code, if you
  instrumented against OTel.
- **Feature flags.** OpenFeature
  ([openfeature.dev](https://openfeature.dev/)) is the
  API standard; GrowthBook or Flagsmith are OSS backends.
- **Data warehouse.** Apache Iceberg
  ([iceberg.apache.org](https://iceberg.apache.org/))
  plus Trino or Spark is the open-lakehouse fallback for
  the proprietary warehouses.
- **CI/CD.** Argo Workflows / Argo CD
  ([argoproj.github.io](https://argoproj.github.io/)) or
  Woodpecker ([woodpecker-ci.org](https://woodpecker-ci.org/))
  provide OSS fallbacks for hosted CI.
- **Container orchestration.** Kubernetes
  ([kubernetes.io](https://kubernetes.io/)) is the
  category standard; every major managed offering (EKS,
  GKE, AKS) is Kubernetes underneath, and self-hosted
  Kubernetes is the OSS fallback.
- **AI model layer.** Open-weight model families (chapter
  04) plus self-hosted inference (vLLM, TGI) is the
  fallback path for the frontier APIs.

Some categories do not have a full OSS fallback:

- **Payments.** No OSS project is a substitute for a
  processor (someone has to hold the acquirer relationship
  and carry the PCI-scope compliance burden). The
  fallback is "another commercial processor", not "an
  OSS deployment".
- **Cloud infrastructure.** No OSS project substitutes
  for the entire cloud (though components — Kubernetes,
  Postgres, S3-API-compatible object stores like MinIO
  [min.io](https://min.io/) or Ceph
  [ceph.io](https://ceph.io/) — do substitute for
  individual cloud services).

Score the column against **how close the fallback is** to
where you are today. A **5** is "we already instrument
against the open standard; we would swap the backend in
weeks"; a **3** is "there is an OSS project we could
adopt, but there's a re-plumbing cost"; a **1** is "no
comparable OSS exists in this category".

The presence of a strong OSS fallback is the most powerful
single hedge against vendor-trajectory risk. A vendor whose
API is compatible with an open standard — OIDC, OTel,
OpenFeature, Iceberg, the S3 API, the Postgres wire
protocol — is materially less risky than an equivalent
vendor whose API is proprietary, even if the switch-day
work is still real.

## Weighting the scorecard

Weights are the mechanism by which the scorecard reflects
*your* situation rather than a generic best-of comparison.
Some patterns:

- **A pre-seed startup optimising for team-time** weights
  time-to-integration and team-familiarity heavily, and
  the switching-cost / OSS-fallback columns lightly (the
  bet is that the next re-architect is 12-18 months away,
  and getting to first customer commitment beats
  everything else).
- **A seed-stage B2B SaaS with enterprise ambitions**
  weights compliance posture (DPA / BAA / SOC 2) and
  vendor-trajectory risk heavily. A vendor whose
  compliance surface is deep enough to unlock enterprise
  deals in the next two quarters is worth more than a
  cheaper vendor whose compliance would take another two
  quarters to reach parity.
- **A Series-A company scaling** weights cost economics
  (per-MAU, per-transaction, per-GB) heavily as the
  vendor bill scales with revenue, and re-runs the
  scorecard on incumbent vendors as part of the annual
  vendor-review rhythm.
- **A regulated industry startup (fintech, healthtech,
  regtech)** weights DPA / BAA availability and
  data-residency as effective threshold criteria — score
  of 3 or below on those criteria disqualifies the
  option regardless of the weighted total.

**Threshold criteria** are worth naming explicitly:
sometimes a criterion is not a weight input but a filter —
the option must score ≥ N or it is out. A vendor without
a BAA is *out* for a HIPAA-covered use case, not
"downweighted".

## The scorecard as a living document

The scorecard is not a one-time artifact. Two rhythms
matter:

- **Re-run the scorecard on incumbent vendors annually.**
  The scorecard as originally authored reflects the
  vendor as it was; a year later, the vendor may have
  moved (new pricing, new capabilities, an acquisition,
  a licence change). Annual re-run either confirms the
  incumbent (which is often the outcome) or surfaces the
  reopening trigger before it becomes urgent.
- **Author a fresh scorecard whenever a new option in a
  category becomes credible.** A new frontier model
  release; a competitor to Stripe reaching the geography
  you sell into; an OSS project graduating out of CNCF
  Sandbox into Incubating status (chapter 05). The
  scorecard is where you evaluate whether the new option
  changes the calculus.

Version the scorecards in the repo, alongside the ADRs
they anchor. Each ADR should link to its scorecard; each
scorecard should link back to the ADR it produced.

## Concrete example: the observability re-selection

Suppose the observability ADR at seed selected Datadog
against a scorecard where Datadog scored 4.4, Grafana Cloud
scored 4.1, and self-hosted Prometheus scored 3.2. The
weighted difference (4.4 vs. 4.1) was small; the deciding
column was time-to-integration weighted at 25% because the
team needed observability shipped in the first sprint.

Twelve months later, the annual re-run of the scorecard
looks different:

- **Time-to-integration** is no longer weighted at 25% —
  everyone is already instrumented. Downweighted to 5%.
- **Cost per host / per log-GB / per metric-cardinality**
  is now weighted at 30% — the bill has become material.
  Datadog's score on this line has dropped because the
  team's cardinality profile has grown.
- **OSS-fallback / open-standard portability** is
  reweighted upward because the team has learned the
  hard way (from the cost trajectory) that vendor
  swappability matters. Grafana Cloud's score on this
  line rises because its OSS fallback is native to the
  same stack.
- **Vendor-trajectory risk** may or may not have moved
  materially; Datadog is a mature category incumbent
  and its trajectory is well-understood.

The re-scored total might have Grafana Cloud tie or beat
Datadog. That does not automatically trigger a switch —
switching cost is now real (Datadog dashboards, custom
metrics, integrations, on-call muscle memory). The right
next artifact is a **spike** (per
[`mod-102` chapter 06](../mod-102-architecture-under-uncertainty/06-spikes-and-kill-criteria.md))
to evaluate the migration cost against the annual bill
delta, with an explicit kill criterion. This is the
scorecard doing its job: not making the decision, but
surfacing that a decision is *due*.

## Common failure modes

- **The scorecard is a feature matrix.** Only vendor-
  advertised features get columns; switching cost,
  trajectory risk, and OSS fallback are absent. Fix: those
  three columns are non-negotiable, even at low weights.
- **The weights are hidden.** The scorecard shows scores
  but not weights, so the reader can't tell what actually
  decided the outcome. Fix: publish weights and the
  reasoning for the weights (a short paragraph in the
  ADR context section).
- **Threshold criteria are treated as weights.** A vendor
  without a BAA scores 1 on the compliance column,
  down-weighted to 0.15, and still tops the weighted
  total. This is a threshold criterion masquerading as a
  weight. Fix: mark threshold criteria explicitly and
  disqualify options below the threshold.
- **The scorecard is authored and never revisited.** The
  vendor was chosen 18 months ago; the world has moved;
  the scorecard is a museum piece. Fix: annual re-run on
  the incumbent for every material category.
- **Ranking vendors on their own marketing.** Filling in
  the scorecard from the vendor's website comparison
  page. Fix: score against your own criteria, using the
  vendor's docs / TOS / DPA — not their comparison chart
  — as the source.
- **Ignoring the switching-cost / re-plumbing tail.**
  Scoring switching cost as "we could migrate in two
  weeks" when in fact the compliance re-attestation, the
  team re-training, and the customer-perceptible-surface
  work would take three months. Fix: double your first
  estimate.

## The tie-in back to the matrix

Each vendor decision, resolved via a scorecard, becomes a
row on the chapter-01 build-vs-buy matrix. The matrix has
columns for capability, disposition, vendor, moat,
leverage, and reopening trigger. The scorecard is the
depth behind the matrix row; the ADR is the durable
one-page record; the matrix is the portfolio view.

At any point in time, the CTO should be able to walk a
technical advisor through:

- **The matrix** — the portfolio view (chapter 01).
- **A specific row** — click through to the ADR (chapter
  02 of [`mod-102`](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md)).
- **The reasoning for the vendor within that row** — the
  scorecard.
- **The re-decision triggers** — visible on both the
  matrix row and the scorecard.

That's the artifact chain. Everything in this module has
been building toward it.

## Summary

- The **vendor-selection scorecard** is the resolution
  artifact for every "buy" row on the chapter-01 matrix.
  It names the criteria that actually decide the choice
  and forces per-option evaluation against those
  criteria.
- Three extra columns are non-negotiable:
  **switching cost** (what would it take to move off?),
  **vendor-trajectory risk** (how likely is the vendor's
  strategy to diverge from ours?), and **OSS fallback
  path** (is there an open alternative, and how wide is
  the gap?).
- **Weights sum to 100%** and reflect *your* situation
  — a pre-seed startup, a seed B2B SaaS, and a Series-A
  regulated-industry startup will weight the same
  criteria differently.
- **Threshold criteria** (BAA availability for HIPAA-
  covered use, GDPR DPA for EU customers,
  data-residency for regulated jurisdictions) are
  filters, not weights.
- The scorecard is a **living document**: re-run
  annually on incumbents; author a fresh one whenever a
  new credible option in the category emerges.
- The scorecard links up to the **ADR** (the durable
  one-page record), and up to the **matrix** (the
  portfolio view). Investors, first engineering hires,
  and technical due-diligence reviewers should be able
  to walk the chain matrix → ADR → scorecard for any
  load-bearing vendor decision the company has made.

The chapter's paired exercise —
[`exercise-05-vendor-selection-scorecard-authoring.md`](exercises/exercise-05-vendor-selection-scorecard-authoring.md)
— walks the authoring of a full scorecard for one real
vendor choice at your (or a real reference) startup,
including the three extra columns and the wiring back into
the matrix and the ADR.
