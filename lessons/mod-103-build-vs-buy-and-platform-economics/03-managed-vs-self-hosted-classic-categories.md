# Managed vs. Self-Hosted Across the Classic Categories

> The managed / self-hosted call is the same call as the
> build-vs-buy call, one level lower. It applies inside every
> row of the chapter-01 matrix that resolved to "buy": the
> data warehouse, the auth provider, the payments processor,
> the observability stack, the CI/CD pipeline, the feature-
> flag system. The category shapes the answer; the frame is
> the same.

## Motivation

Chapter 01 established the portfolio frame: leverage vs. moat
vs. team-time economics, resolved once per capability at the
build-vs-buy level. This chapter drops one level of
resolution: **for each capability where the answer was "buy",
which flavour do we buy — a fully managed SaaS from a vendor,
a cloud-managed service on our hyperscaler, or a self-hosted
open-source deployment we operate ourselves?**

The categories the seed-stage CTO faces this quarter are
well-defined and recurring — the data warehouse, auth /
identity, payments, observability, CI/CD, feature flags,
plus (in chapter 04) the AI-native model layer. This chapter
walks each one and names the decision-forcing questions
specific to that category, rather than pretending a single
generic answer applies across all of them.

The goal is not a vendor recommendation. It is a decision
framework that lets the seed-stage CTO defend the choice on
each row of the matrix — to a technical advisor, to a
first engineering hire, to an investor doing technical due
diligence — with reference to the actual axes that governed
the call.

## The three flavours the "buy" decision resolves into

Before going category-by-category, name the three flavours
that a "buy" disposition can resolve into. Each has a
different economic profile.

- **Fully-managed SaaS from an independent vendor.**
  Snowflake, Auth0, Stripe, Datadog, LaunchDarkly, GitHub
  Actions (as a SaaS). The vendor operates the software; you
  consume it via an API or console; you have zero
  operational burden on the underlying stack. Highest
  leverage per dollar, deepest lock-in, most-exposed to
  vendor-trajectory risk (chapter 06).
- **Cloud-managed service from your hyperscaler.** RDS /
  Cloud SQL / Azure SQL for Postgres; Cognito / Azure AD B2C
  for identity; CodePipeline / Cloud Build / Azure DevOps
  for CI; CloudWatch / Cloud Logging / Azure Monitor for
  observability. The hyperscaler operates the software; you
  configure it; the lock-in is to that cloud, not to a
  separate vendor. Discounted by credits (chapter 02); tied
  to your cloud choice.
- **Self-hosted OSS on your own infrastructure.** Postgres
  on RDS-or-Kubernetes; Keycloak or Ory Kratos for identity;
  Prometheus + Grafana + Loki for observability; self-hosted
  GitLab or Woodpecker for CI/CD; OpenFeature + a self-
  hosted flag backend like Flagd or GrowthBook for feature
  flags. You operate the software; the licence cost is zero
  (subject to the specific OSS licence — see the OSI
  licence list at
  [opensource.org/licenses](https://opensource.org/licenses/))
  but the operational cost is real. Lowest lock-in, highest
  team-time cost, and only defensible when the operational
  team-time is available.

Each category below asks a set of questions that surface
which flavour is defensible **for your startup, at your
stage**. Nothing here says "always pick option X" — the
answer moves with stage, with team, and with the specific
customer commitment on the roadmap.

## Category: data warehouse

The classic decision: **Snowflake vs. BigQuery vs. Redshift
vs. self-hosted OSS (Postgres, ClickHouse, DuckDB, Apache
Iceberg on object storage, or a self-hosted Trino cluster)**.

- **Snowflake** ([snowflake.com](https://www.snowflake.com/))
  — separation of storage and compute, credit-based pricing
  ([snowflake.com/pricing](https://www.snowflake.com/pricing/)),
  cloud-agnostic (runs on AWS / GCP / Azure). Strong for
  teams whose analytics workload has spiky query patterns
  and where the multi-cloud posture is a real requirement.
- **Google BigQuery**
  ([cloud.google.com/bigquery](https://cloud.google.com/bigquery)) —
  serverless, per-query and per-storage pricing (or
  reservation-based
  [cloud.google.com/bigquery/pricing](https://cloud.google.com/bigquery/pricing)),
  GCP-native. Strong for teams already on GCP with strong
  BI ambitions and moderate warehouse volumes.
- **Amazon Redshift**
  ([aws.amazon.com/redshift](https://aws.amazon.com/redshift/)) —
  cluster-based (with Serverless option), AWS-native.
  Strong for teams already on AWS with predictable,
  provisioned analytics workloads.
- **Self-hosted analytics** — the space is broad and
  fast-moving. Postgres is the "one-database" default at
  small scale (a warehouse is not required if the
  transactional store handles the analytics volume);
  ClickHouse
  ([clickhouse.com](https://clickhouse.com/)) is a leading
  OSS columnar option; DuckDB
  ([duckdb.org](https://duckdb.org/)) is a leading
  single-node analytics engine; Apache Iceberg
  ([iceberg.apache.org](https://iceberg.apache.org/)) plus
  a query engine (Trino, Spark) on object storage is the
  common "open lakehouse" pattern.

The decision-forcing questions:

- **What's the analytics load this quarter?** If a Postgres
  read replica can answer the analytics questions, you do
  not have a warehouse decision; you have a "do we need a
  warehouse?" decision. Defer the split.
- **Where does the data live already?** The egress trap from
  chapter 02 shapes the answer. A warehouse in a different
  cloud than the production data means an ongoing egress
  bill.
- **Who runs it?** A self-hosted Iceberg-plus-Trino stack is
  a defensible technical answer with zero licence cost and
  a large operational footprint. If nobody on the team has
  operated it before and you cannot dedicate an engineer's
  time to it, the operational cost eats the licence saving.
- **What's the query-cost trajectory?** BigQuery's
  per-query pricing rewards well-optimised queries and
  punishes select-star exploration. Snowflake's per-credit
  pricing rewards short queries and punishes long-running
  ones. Redshift's provisioned pricing rewards steady load
  and punishes bursty load. Model the workload shape
  against the pricing shape.

Seed-stage default when a warehouse is genuinely needed: a
fully-managed SaaS or cloud-managed warehouse on the same
cloud as the transactional data. Self-host only when a
specific team member owns the operational duty and the
licence savings materially help unit economics.

## Category: auth / identity

The classic decision: **Auth0 vs. WorkOS vs. Clerk vs.
Firebase Auth vs. cloud-native (Cognito / Azure AD B2C) vs.
self-hosted (Keycloak, Ory Kratos, Supertokens)**.

- **Auth0**
  ([auth0.com](https://auth0.com/) — now part of Okta) —
  the incumbent developer-friendly identity SaaS. Broad
  standards coverage (OIDC, SAML, SCIM), enterprise-grade
  compliance posture. Pricing is per-active-user with
  tiered feature gating; the enterprise features (SAML,
  SCIM, MFA policies) live in the higher tiers.
- **WorkOS**
  ([workos.com](https://workos.com/)) — positioned
  specifically at the "add SSO / SCIM to your B2B SaaS"
  problem, with per-connection pricing rather than per-MAU
  for the enterprise features. Strong for B2B SaaS whose
  enterprise deals require SSO/SCIM plumbing early.
- **Clerk** ([clerk.com](https://clerk.com/)) — modern
  React/Next.js-native developer experience with pre-built
  UI components. Strong for consumer-facing or dev-tool
  products where auth UX is a first-class concern.
- **Firebase Auth**
  ([firebase.google.com/products/auth](https://firebase.google.com/products/auth))
  — Google's consumer-scale identity service; strong for
  mobile-first consumer products, especially on GCP.
- **AWS Cognito**
  ([aws.amazon.com/cognito](https://aws.amazon.com/cognito/))
  and **Microsoft Entra External ID / Azure AD B2C**
  ([microsoft.com/entra/external-id](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-external-id))
  — cloud-native alternatives, discounted via cloud credits;
  developer experience is a common critique.
- **Self-hosted OIDC** — Keycloak
  ([keycloak.org](https://www.keycloak.org/)) is the
  reference open-source identity server (Apache 2.0). Ory
  Kratos ([ory.sh/kratos](https://www.ory.sh/kratos/)) is
  the API-first modern alternative. Supertokens
  ([supertokens.com](https://supertokens.com/)) offers a
  self-host + managed hybrid. Zero licence cost; real
  operational cost.

The decision-forcing questions:

- **B2B or B2C?** B2B products with enterprise ambitions
  need SAML SSO and SCIM provisioning early; those are the
  features that gate design partners at the "let's roll
  this out to 500 employees" stage. WorkOS and Auth0
  Enterprise are common answers; a self-hosted Keycloak
  will do the job at higher operational cost.
- **What's the MAU shape?** Per-MAU pricing hurts most at
  the seed-to-Series-A transition (large user base, small
  revenue). Per-connection or per-enterprise-customer
  pricing (WorkOS's model) is often a better fit for B2B
  SaaS.
- **What's the compliance surface?** SOC 2 Type II,
  HIPAA (BAA), FedRAMP requirements are all easier through
  a compliant vendor than a self-hosted stack (see
  [`mod-107`](../mod-107-founder-scope-security-and-compliance/)
  on the vendor DPA / BAA acquisition). Compliance is
  usually the pivotal input.
- **How central is auth UX to the product?** For a
  consumer-facing product where the login screen is the
  first impression, Clerk's UI-native model wins; for a
  B2B API product, the UX matters less than the SSO/SCIM
  coverage.

Seed-stage default: **buy**, with the specific vendor
chosen against B2B/B2C shape and MAU/connection economics.
Self-hosted identity is defensible when the team has
operated Keycloak or Kratos before and when the compliance
posture allows.

## Category: payments

The classic decision: **Stripe vs. Adyen vs. Braintree vs.
build-your-own-integration-with-an-acquirer**. This is the
category where "build" is almost never a defensible option
at seed.

- **Stripe** ([stripe.com](https://stripe.com/)) — the
  developer-experience-first incumbent. Broad geographic
  coverage, deep product surface (Billing, Radar for fraud,
  Connect for marketplaces, Terminal for POS, Issuing for
  card issuance). Per-transaction pricing.
- **Adyen** ([adyen.com](https://www.adyen.com/)) —
  enterprise-oriented, strong on multi-currency /
  multi-region and unified merchant-of-record features.
  Typically wins on cost at material transaction volumes.
- **Braintree**
  ([braintreepayments.com](https://www.braintreepayments.com/)) —
  PayPal-owned, strong PayPal / Venmo integration; a
  common alternative when PayPal wallet support is a
  first-class requirement.

The decision-forcing questions:

- **What's PCI scope?** Every option above reduces the
  merchant's PCI-DSS scope to SAQ A (the lightest tier)
  when the tokenisation flow is used correctly. Building
  card handling in-house means SAQ D (the heaviest tier).
  This alone decides the call for almost every seed-stage
  startup.
- **Geography and payment methods?** Stripe's geographic
  coverage is broad but not universal (check the current
  supported-countries list before assuming); Adyen leads
  in some markets Stripe does not fully cover; Braintree's
  PayPal / Venmo integration is unmatched. Match the
  vendor to the customer base.
- **Fee economics.** All three publish per-transaction
  fees; the actual take-rate at material volume is
  negotiated. For an early-stage startup, the headline
  fee is what you pay; for a Series-A+ company doing
  material volume, negotiate.
- **Product-surface breadth.** Stripe Billing (subscription
  and usage-based invoicing) and Stripe Connect
  (marketplace payouts) are the two extensions that most
  materially raise the switching cost off Stripe — worth
  naming in the ADR.

Seed-stage default: **buy a card-not-present processor**
(Stripe is the common answer for developer-experience
reasons; Adyen when multi-region or marketplace scale is
material; Braintree when PayPal is a first-class rail).
Self-build is not a defensible option; the closest
build-side call is which processor SDK to build against.

## Category: observability (logs, metrics, traces)

The classic decision: **Datadog vs. Grafana Cloud vs. New
Relic vs. Honeycomb vs. an OSS stack (Prometheus + Grafana +
Loki + Tempo, or the OpenTelemetry stack pointed at any
compatible backend)**.

- **Datadog** ([datadoghq.com](https://www.datadoghq.com/)) —
  the incumbent all-in-one observability SaaS. Strong
  breadth (APM, logs, metrics, RUM, security). Per-host and
  per-GB-ingested pricing.
- **Grafana Cloud**
  ([grafana.com/products/cloud](https://grafana.com/products/cloud/)) —
  a managed version of the Grafana / Prometheus / Loki /
  Tempo stack. Strong for teams that want the OSS stack
  without the operational cost, and that value the option
  to move to self-hosted later.
- **New Relic** ([newrelic.com](https://newrelic.com/)) —
  APM-first observability incumbent with a shifted
  usage-based pricing model.
- **Honeycomb** ([honeycomb.io](https://www.honeycomb.io/)) —
  event-first observability with strong support for
  high-cardinality dimensions; leading choice when the
  workload is distributed-systems debugging rather than
  metric dashboards.
- **OpenTelemetry-based OSS stacks** — the
  [OpenTelemetry](https://opentelemetry.io/) project has
  become the vendor-neutral instrumentation standard (a
  CNCF graduated project — see chapter 05). The typical
  self-hosted composition is OTel collectors →
  Prometheus / Mimir (metrics) + Loki (logs) + Tempo /
  Jaeger (traces) → Grafana (dashboards). Zero licence
  cost; substantial operational surface at scale.

The decision-forcing questions:

- **What's the cardinality profile?** A per-user-ID or
  per-request-ID dimension in the metric explodes cost on
  any per-cardinality-priced backend (most of them). Tools
  that price events, not cardinality (Honeycomb), fit
  high-cardinality workloads better.
- **What's the log volume trajectory?** Log-ingest-priced
  vendors (Datadog Logs and peers) can become the largest
  line on the vendor bill faster than the team notices.
  Set alerts on the log-cost line early.
- **How pluggable is the instrumentation?** Instrumenting
  in OpenTelemetry primitives keeps the backend swappable
  later — one of the cheapest hedges against
  observability-vendor lock-in.
- **Who's on-call?** A small team on-call rotates through
  the same on-call engineer often; making that engineer's
  triage fast is a first-order investment. The vendor
  whose UI the on-call engineer actually uses in a 3am
  incident is often the right answer.

Seed-stage default: **buy** — self-hosting the full metric /
log / trace stack is a full-time job the seed-stage team
does not have. Instrument in OpenTelemetry primitives so the
backend is swappable; choose the backend for on-call
usability and per-workload cost fit.

## Category: CI / CD

The classic decision: **GitHub Actions vs. CircleCI vs.
GitLab CI vs. Buildkite vs. self-hosted (Jenkins, Woodpecker,
Argo Workflows, Tekton)**.

- **GitHub Actions**
  ([github.com/features/actions](https://github.com/features/actions)) —
  the default when the code is already on GitHub. Native
  integration; managed runners with per-minute pricing;
  optional self-hosted runners for larger jobs or GPU
  builds.
- **CircleCI** ([circleci.com](https://circleci.com/)) — the
  incumbent independent CI SaaS; strong parallelism
  primitives, Docker-first workflow.
- **GitLab CI** ([about.gitlab.com/ci](https://about.gitlab.com/topics/ci-cd/)) —
  the tightly-integrated CI in GitLab (SaaS or self-hosted).
- **Buildkite** ([buildkite.com](https://buildkite.com/)) —
  hybrid model: hosted control plane, self-hosted agents.
  Strong for teams needing custom runner environments
  (GPUs, large VMs) with a managed orchestration layer.
- **Self-hosted OSS** — Jenkins
  ([jenkins.io](https://www.jenkins.io/)) is the incumbent;
  Argo Workflows / Argo CD
  ([argoproj.github.io](https://argoproj.github.io/)) is the
  Kubernetes-native option; Woodpecker
  ([woodpecker-ci.org](https://woodpecker-ci.org/)) is a
  lightweight modern OSS CI.

The decision-forcing questions:

- **Where does the code live?** If it's on GitHub,
  Actions is the near-default; if on GitLab, GitLab CI is
  the near-default; if on Bitbucket, Bitbucket Pipelines.
  Cross-platform CI adds a whole build-service dependency.
- **What's the build-time envelope?** Long builds (large
  frontend bundles, native compilation, ML training) push
  toward self-hosted runners regardless of the control-plane
  vendor.
- **What's the build-security posture?** SLSA
  ([slsa.dev](https://slsa.dev/)) build-provenance targets
  (see [`mod-107`](../mod-107-founder-scope-security-and-compliance/))
  are easier on some CI systems than others; check the
  supported-attestations matrix before committing to a
  self-signed build path.
- **What's the runner-cost trajectory?** Per-minute runner
  pricing scales linearly with build volume; self-hosted
  runners on spot instances (chapter 02) can be materially
  cheaper at material CI volume, at the cost of runner
  maintenance.

Seed-stage default: **use the CI that's built into your
code-hosting** — GitHub Actions for GitHub, GitLab CI for
GitLab. Self-host runners for GPU / long-build workloads if
the per-minute bill justifies it. Full self-hosted Jenkins
or Argo is defensible when the team already runs it or when
regulated deployment targets require it.

## Category: feature flags

The classic decision: **LaunchDarkly vs. Split vs. Optimizely
vs. GrowthBook vs. Flagsmith vs. OpenFeature-with-a-self-
hosted-backend**.

- **LaunchDarkly** ([launchdarkly.com](https://launchdarkly.com/)) —
  the incumbent enterprise flags SaaS. Broad SDK
  coverage, strong on percentage rollouts and audit trail;
  per-MAU pricing.
- **Split** ([split.io](https://www.split.io/)) — feature
  flags plus experimentation; strong on the
  experiment-attribution side.
- **Optimizely**
  ([optimizely.com](https://www.optimizely.com/)) —
  experimentation-first; feature flags via Optimizely
  Feature Experimentation. Strong when
  experimentation-as-primary-workflow.
- **GrowthBook** ([growthbook.io](https://www.growthbook.io/)) —
  open-source (self-host or cloud) feature flags plus
  experimentation.
- **Flagsmith** ([flagsmith.com](https://www.flagsmith.com/)) —
  open-source (self-host or cloud) feature flags.
- **OpenFeature**
  ([openfeature.dev](https://openfeature.dev/)) — the
  CNCF-hosted (see chapter 05) vendor-neutral feature-flag
  API standard. Instrument against OpenFeature and plug in
  any compatible backend (self-hosted or SaaS) later —
  same portability hedge as OpenTelemetry gives on the
  observability side.

The decision-forcing questions:

- **Is this flags or experimentation?** If the team needs
  A/B testing with statistical attribution, that's
  experimentation, and the flags-plus-experimentation
  vendors are stronger. Pure feature flags is a smaller
  scope.
- **What's the MAU count?** Per-MAU pricing on
  LaunchDarkly-tier vendors becomes material fast at
  consumer scale. B2B SaaS with tens of thousands of MAU
  can afford it; consumer products with millions may not.
- **How portable does the instrumentation need to be?**
  OpenFeature is the answer to "we don't want to be
  locked in to any one flags vendor". Instrument once,
  swap backends.

Seed-stage default: **use an OSS or open-standard flags
option** — GrowthBook, Flagsmith, or the OpenFeature API with
a modest backend — unless the MAU / feature scale genuinely
warrants a paid enterprise flags SaaS. Feature flags are the
category where OSS has caught up hardest with the incumbents.

## Cross-category patterns

Across all the categories above, three patterns recur.

- **Instrument to an open interface where one exists.**
  OpenTelemetry for observability; OpenFeature for feature
  flags; OpenID Connect / OAuth 2.1 for identity; SQL and
  Iceberg for warehouse portability; the S3 API for object
  storage. Instrumenting to the open interface preserves
  the option to swap the backing implementation (chapter
  06's OSS-fallback path) even inside a "buy" decision.
- **The vendor's take-rate rises with your value.** Per-MAU,
  per-transaction, per-host, per-log-GB pricing all scale
  with your success. A vendor whose fee was 2% of revenue
  at seed can be 15% of gross margin at Series A. Model
  the fee trajectory as part of the ADR.
- **The category where you self-host is the category the
  team will always be operating.** Self-hosted Postgres,
  self-hosted Prometheus, self-hosted GitLab, self-hosted
  Keycloak — pick at most one category to self-host at
  seed. The team-time cost of running two production OSS
  stacks in parallel is disproportionate.

## Concrete example: the observability-cost surprise

A recurring seed-stage story:

- Team adopts Datadog on the Free / Pro tier during the
  first months. Instrumentation is easy; dashboards are
  good. Everyone is happy.
- Traffic grows. A well-meaning engineer adds a per-user-ID
  tag to a set of custom metrics for debugging. Metric
  cardinality explodes.
- The next month's Datadog bill is significantly larger
  than the previous month. The team investigates; the
  culprit is the high-cardinality tag and the growing
  application-log volume from the new logging library
  the team also added.
- The team either scales back the instrumentation
  (accepting reduced observability), migrates to a
  cardinality-friendly backend (an engineer-week to
  re-instrument, but the observability improves), or
  negotiates with Datadog for a committed-use discount
  (which locks in the current spend for a year).

Portfolio verdict: **the observability ADR should have
named the per-cardinality cost mechanism and the cost
alert**. Not "don't use Datadog" — the leverage is real —
but "here's the pricing shape, here's the alert threshold
that trips before the bill triples, and here's the
OpenTelemetry hedge that keeps the backend swappable if the
cost trajectory doesn't fit us". Chapter 06's scorecard is
the tool that surfaces this per-category dynamic before it
becomes a bill.

## Summary

- Every "buy" row on the chapter-01 matrix resolves into
  one of three flavours: **fully-managed SaaS**, **cloud-
  managed service**, or **self-hosted OSS**. Each has a
  distinct economic profile.
- The **classic categories** — data warehouse, auth,
  payments, observability, CI/CD, feature flags — each
  come with a small set of decision-forcing questions
  that shape the flavour. There is no single generic
  answer.
- **Payments is the category where self-build is almost
  never defensible at seed**, because PCI scope alone
  decides the call.
- **Feature flags is the category where OSS has caught up
  hardest with the incumbents**, and OpenFeature is a
  cheap portability hedge for the category as a whole.
- Cross-category, three patterns recur: **instrument to
  open interfaces**, **model the vendor's take-rate as it
  scales with your success**, and **pick at most one
  category to self-host** at seed.
- Every meaningful category decision should be captured in
  an ADR (see [`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md))
  with the reopening trigger named — the trajectory
  condition under which the flavour would change.

The chapter's paired exercise —
[`exercise-03-managed-vs-self-hosted-drill-for-three-categories.md`](exercises/exercise-03-managed-vs-self-hosted-drill-for-three-categories.md)
— walks the managed-vs-self-hosted call for three chosen
categories from the list above. Chapter 04 picks up the same
frame for the AI-native stack, where the managed / cloud-
managed / self-hosted trichotomy takes a different shape.
