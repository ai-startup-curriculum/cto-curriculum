# Cloud Providers as Economic Actors

> A hyperscale cloud is not a neutral utility. It is a
> for-profit counterparty with a pricing strategy, a
> credits programme calibrated to acquire and retain
> workloads, an egress structure that shapes where your
> data can affordably live, and a roadmap that reflects its
> commercial interests — not yours. Choose accordingly.

## Motivation

For most seed-stage startups the choice of cloud is treated
as an aesthetic default — "we're an AWS shop", "we're on GCP
because the founders came from Google", "we picked Azure
because the enterprise design partner asked" — with the
economic shape of that choice left implicit. Two or three
years later, when the monthly cloud bill is one of the
largest line items on the P&L, the CFO or the lead investor
asks the CTO to defend the choice on economic grounds, and
"we've always been on AWS" is no longer a defence.

This chapter frames AWS, Google Cloud, and Microsoft Azure as
what they are — for-profit economic actors — and gives the
seed-stage CTO the vocabulary to reason about their pricing
structure (egress, reserved capacity, spot / preemptible),
their credits programmes, the lock-in each cloud creates via
its managed-service catalogue, and the migration cost of
moving between them. The goal is not to pick a "best" cloud —
there isn't one — but to make the choice defensibly, name the
lock-in the choice creates, and set the reopening triggers
that would force a re-plan.

The output pairs with the build-vs-buy matrix from chapter
01: the cloud row is the single largest "buy" line for most
startups, and its economics deserve to be modelled explicitly
rather than absorbed as a fixed cost of doing business.

## Where the cloud makes its money

At a first approximation, hyperscale cloud revenue comes from
three flows: **compute** (VMs, containers, serverless
functions), **storage** (block, object, database services),
and **data movement** (network, especially egress). All three
matter for the seed-stage CTO's model, but the pricing
structure of each has different strategic implications.

### Compute

Compute is priced per second (or per millisecond for
serverless functions), with headline on-demand prices that
are the highest a customer will ever pay. Every provider
offers multiple discount mechanisms that trade flexibility
for price:

- **Reserved-capacity / committed-use discounts.** AWS's
  Savings Plans and Reserved Instances
  ([aws.amazon.com/savingsplans](https://aws.amazon.com/savingsplans/)),
  Google Cloud's Committed Use Discounts
  ([cloud.google.com/docs/cuds](https://cloud.google.com/docs/cuds)),
  and Azure's Reservations
  ([azure.microsoft.com/pricing/reserved-vm-instances](https://azure.microsoft.com/en-us/pricing/reserved-vm-instances/))
  each trade a 1-year or 3-year usage commitment for a
  material discount off on-demand pricing. The exact
  discount varies by instance family, region, and commitment
  term — read the vendor page for current figures rather
  than relying on any number in a training deck. **These
  programmes require *predictable* usage** — a pre-seed
  startup whose traffic could 10x or vanish in the next
  quarter is often better off staying on-demand until the
  usage stabilises.
- **Spot / preemptible / low-priority.** AWS Spot
  ([aws.amazon.com/ec2/spot](https://aws.amazon.com/ec2/spot/)),
  Google Cloud Spot VMs
  ([cloud.google.com/spot-vms](https://cloud.google.com/spot-vms)),
  and Azure Spot VMs
  ([azure.microsoft.com/services/virtual-machines/spot](https://azure.microsoft.com/en-us/services/virtual-machines/spot/))
  sell excess capacity at a steep discount off on-demand,
  with the trade-off that the provider can reclaim the
  instance on short notice. Well suited to fault-tolerant
  batch workloads (ML training, data-processing pipelines,
  CI); poorly suited to user-facing latency-critical work.
- **Serverless.** AWS Lambda, Google Cloud Run / Cloud
  Functions, Azure Functions charge per-invocation and per-
  ms of compute, with generous free tiers. The pricing
  model shifts *operational* risk to the provider (scaling,
  patching, capacity) at the cost of a per-invocation fee
  that is only economical up to a certain sustained
  request rate — above that rate, a right-sized VM or
  container platform is usually cheaper.

The strategic implication for the seed-stage CTO is: **the
headline on-demand price is a ceiling, not the price you
will pay at scale**. The discount mechanisms are real, but
each one is a commitment that either constrains architectural
flexibility (reserved capacity → you own an instance family
for a year) or workload shape (spot → your workload must be
interruption-tolerant). Model the discount mechanism you plan
to graduate into, not the on-demand headline, when building
the multi-year cost curve.

### Storage

Object storage (S3, Google Cloud Storage, Azure Blob) is the
commodity floor of cloud storage and is priced per-GB per
month, with tiered pricing for hotter or colder access
patterns (S3 Standard vs. S3 Glacier
[aws.amazon.com/s3/pricing](https://aws.amazon.com/s3/pricing/);
GCS Standard vs. Coldline / Archive
[cloud.google.com/storage/pricing](https://cloud.google.com/storage/pricing);
Azure Blob Hot / Cool / Archive
[azure.microsoft.com/pricing/details/storage/blobs](https://azure.microsoft.com/en-us/pricing/details/storage/blobs/)).
At seed-stage volumes, storage-per-GB is rarely the dominant
line item — but **the per-request charges and the *egress*
charges are what turn a low storage bill into a large
network bill**. See the egress section below.

Managed database storage (RDS, Cloud SQL, Azure SQL,
BigQuery, Snowflake-on-cloud, etc.) is priced as a package —
the CPU / RAM allocated to the database plus the storage
attached plus the network the queries generate. At seed
stage, managed databases are almost always the right call
(see chapter 03 on managed vs. self-hosted), but the total
cost of a managed database at scale is not "the storage
price" — it is the composed cost of compute + storage +
network + backup + read replicas + high-availability
premium.

### Data movement — the egress trap

The single most under-appreciated economic feature of the
hyperscale clouds, from the perspective of a seed-stage
startup, is **egress pricing**. Ingress (data coming into the
cloud) is free on all three hyperscalers. Egress (data
leaving the cloud, to the public internet or to another
cloud) is charged per-GB, at rates that make cross-cloud
data movement a first-order economic constraint.

- **AWS data-transfer pricing** —
  [aws.amazon.com/ec2/pricing/on-demand/#Data_Transfer](https://aws.amazon.com/ec2/pricing/on-demand/#Data_Transfer)
  — publishes per-GB rates for egress to the internet, to
  other AWS regions, and between AZs. Rates vary by region;
  read the current page rather than recalling any specific
  number. AWS did announce free egress *when leaving AWS
  entirely*
  ([aws.amazon.com/blogs/aws/free-data-transfer-out-to-internet-when-moving-out-of-aws](https://aws.amazon.com/blogs/aws/free-data-transfer-out-to-internet-when-moving-out-of-aws/)),
  but only for a customer who is fully off-boarding — this
  does not make routine multi-cloud egress cheap.
- **Google Cloud network pricing** —
  [cloud.google.com/vpc/network-pricing](https://cloud.google.com/vpc/network-pricing)
  — publishes per-GB egress rates split by destination
  (internet, other-region, same-region same-zone) and by
  network tier (Premium vs. Standard).
- **Azure bandwidth pricing** —
  [azure.microsoft.com/pricing/details/bandwidth](https://azure.microsoft.com/en-us/pricing/details/bandwidth/)
  — publishes per-GB egress rates split by destination and
  by monthly volume tier.
- The **Cloudflare** blog series on egress — starting with
  [blog.cloudflare.com/aws-egregious-egress](https://blog.cloudflare.com/aws-egregious-egress/) —
  is the widely-read outside-vendor critique of hyperscale
  egress pricing. Read it with a skeptical eye (Cloudflare
  is not a neutral commentator; it sells R2, an egress-free
  competitor to S3) but the *shape* of the argument
  survives the source.

The strategic implication is architectural: **an application
architected to pull large volumes of data across cloud
boundaries — a warehouse in one cloud reading from a
transactional database in another, an ML training pipeline
pulling from an object store in a different cloud, a
customer-facing endpoint serving media from a different
provider than the compute — accumulates egress bills that
easily dominate the cloud spend at scale**. This is the
lock-in mechanism the hyperscalers rely on: once your data
gravity is in AWS, moving compute to GCP is a decision with
a per-GB tax attached.

Design decisions that trigger the egress trap should be
explicit ADRs (per
[`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md))
and should feed the cloud-provider row of the chapter-01
build-vs-buy matrix.

## Credits programmes

All three hyperscalers run structured credits programmes
targeted at early-stage startups, and the seed-stage CTO
should treat these as a real economic input — but should also
understand what the credit is buying for the vendor.

- **AWS Activate** —
  [aws.amazon.com/activate](https://aws.amazon.com/activate/)
  — credit packages for startups (typically tiered by
  accelerator / VC affiliation and stage), plus technical
  content and Business Support at the top tier.
- **Google for Startups Cloud Program** —
  [cloud.google.com/startup](https://cloud.google.com/startup)
  — similar credit tiers with an AI-focused track for
  AI-native startups.
- **Microsoft for Startups Founders Hub** —
  [microsoft.com/startups](https://www.microsoft.com/en-us/startups)
  — Azure credits plus GitHub, Office, and (via the AI
  track) OpenAI / Azure OpenAI credits.

The economic reality behind these programmes is that the
vendor is acquiring your workload cheaply now in the
expectation that (a) you will still be running on their
cloud when the credits expire, (b) the data-gravity /
managed-service lock-in accumulated during the credit
period will make it uneconomical to move, and (c) the
lifetime value of a growing startup customer justifies the
up-front acquisition cost. This is a rational trade for the
vendor and can be a rational trade for the startup — but
recognise the trade:

- **Do not architect against the credit.** If your unit
  economics only work while the credit is subsidising the
  bill, you are running a business that will become
  unprofitable the day the credit expires. Model your
  cost-to-serve at *post-credit* on-demand pricing (with
  reasonable committed-use discounts), not at the credit
  price.
- **Do not let the credit pick the architecture.** A managed
  service that is generously credited but has no OSS
  fallback (see chapter 06) is a stronger lock-in than a
  managed service on the same cloud that is a Kubernetes
  distribution or a Postgres compatible interface. Where
  possible, prefer the cloud-lock-avoiding variant even
  under credits.
- **Use the credits for the workloads that would otherwise
  be under-invested.** Development environments, CI /
  build fleets, experimental ML training runs — the work
  the runway would not otherwise pay for at full price.
  This is the highest-ROI use of the credits, and it
  minimises the architectural entanglement the credits
  create.

## Lock-in — where the switching cost accumulates

Not all cloud lock-in is equal. Some services are effectively
commodity between providers; others are deep enough that
moving off them is an engineer-quarter or more of work. A
useful first-pass taxonomy:

- **Low lock-in.** Compute (VMs, containers) — the underlying
  IaaS is close enough between providers that moving a
  container image between them is straightforward. Object
  storage — S3, GCS, and Azure Blob all speak either the S3
  API or a close variant, and object-storage clients are
  usually two lines of configuration away from cross-cloud
  portability.
- **Medium lock-in.** Managed Kubernetes (EKS, GKE, AKS) —
  the workload YAML is portable, but the cluster's
  identity, networking, and add-on ecosystem
  (load-balancers, ingress controllers, cluster
  autoscalers) are provider-specific. Managed relational
  databases (RDS / Cloud SQL / Azure SQL) — the SQL is
  portable, but the operational tooling (backups, replicas,
  IAM integration) is not.
- **High lock-in.** Managed serverless (Lambda, Cloud Run
  triggered by GCP-specific events, Azure Functions bound
  to Azure Event Grid) — the business logic often depends
  on provider-specific event sources and IAM. Managed data
  warehouses (Redshift, BigQuery, Synapse) — the SQL
  dialects, the ingest APIs, and the operational models
  differ enough that moving between them is a significant
  project (see chapter 03).
- **Very high lock-in.** Provider-specific ML services
  (SageMaker, Vertex AI, Azure ML pipelines) that couple
  training, deployment, and monitoring to the provider's
  own primitives. Provider-specific streaming, analytics,
  and identity fabric (Kinesis, Cognito, Pub/Sub, IAM
  role trust policies specific to STS).

The strategic implication for the seed-stage CTO is: **name
the lock-in you are accepting, per major managed service, in
the ADR that accepts it, and reflect it on the build-vs-buy
matrix**. The seed-stage default is to accept meaningful
lock-in in exchange for the leverage of managed services (see
chapter 03) — the discipline is naming it, not avoiding it.
Chapter 06's vendor-selection scorecard formalises the
switching-cost dimension.

## Migration cost — what it actually takes to move

Migrating between clouds is expensive in three ways that are
often under-modelled:

- **Data-egress cost of the move itself.** Moving many
  terabytes of object storage or a large warehouse across
  cloud boundaries incurs the per-GB egress charge on the
  source cloud. For a warehouse or data-lake heavy
  business this can be the single largest line item of the
  migration. Vendors do sometimes waive or credit egress
  for a full off-boarding (AWS's off-boarding programme
  cited above; GCP has periodically run similar programmes),
  but the terms are conditional and slow.
- **Engineer-time to re-plumb managed services.** The
  cross-cloud equivalents are rarely 1:1. IAM models
  differ; managed queue semantics differ; log and metric
  schemas differ. The re-plumbing is usually
  engineer-quarters of work, not weeks, and it happens
  alongside the ongoing product work rather than in
  isolation. Consult vendor migration guides such as
  Google's cloud-migration center
  ([cloud.google.com/migration-center](https://cloud.google.com/migration-center))
  and AWS Migration Hub
  ([aws.amazon.com/migration-hub](https://aws.amazon.com/migration-hub/))
  — but treat their timelines as advertised, not observed.
- **Regression risk during the move.** A cloud migration
  under time pressure is where you discover the undocumented
  cloud-specific behaviour your product depended on. See
  chapter 05 of
  [`mod-102`](../mod-102-architecture-under-uncertainty/05-monolith-modular-monolith-services-and-cap.md)
  on how the same StranglerFig pattern that applies to
  service extraction applies to workload migration between
  clouds: incrementally, with kill criteria, and never as a
  big-bang cutover if it can be avoided.

The seed-stage CTO does not need to plan a cloud migration.
The seed-stage CTO does need to **know what it would cost**
so that the current cloud choice is a defensible one and not
an inertia one.

## Multi-cloud as a strategic posture (usually the wrong default)

A common reaction to reading about lock-in is to reach for
"we should be multi-cloud from day one". This is almost
always the wrong call at seed stage. Multi-cloud multiplies
the operational surface (two IAM models, two monitoring
stacks, two ingress paths, two networking meshes), imposes
egress cost on any cross-cloud data flow, and effectively
denies the team the leverage of any single cloud's managed
services (because those services differ per cloud). The
result is that the team runs *less* infrastructure per
engineer-hour, not more.

The narrow cases where multi-cloud is defensible at seed:

- A specific enterprise customer's data-residency
  requirement forces deployment into a region only one
  vendor serves — but for that customer only, not for the
  whole stack.
- A specific capability is materially better on one cloud
  than the others *and* is small enough that the split
  operational surface is manageable (a common example is a
  large-scale ML training workload on GCP TPUs while the
  production application runs elsewhere; see
  [`ai-infra-mlops`](../../../ai-infra-mlops-learning) for
  the depth on this).
- The company is genuinely at scale and the risk of a
  single-cloud outage or business-relationship breakdown is
  worth the operational cost. This is a growth-stage or
  post-Series-B posture — see the deferral to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45).

Otherwise: **single cloud, named lock-in, ADR that captures
the reopening trigger for a future multi-cloud call**.

## Concrete example: the data-warehouse-egress trap

A common shape of the egress trap at seed stage:

- The company's transactional application runs on AWS (EC2 /
  EKS / RDS), because the founding engineer knew AWS.
- The analytics team adopts BigQuery (GCP) as the data
  warehouse, on the argument that the serverless query
  model is easier than Redshift and the AI/ML integrations
  are ahead of AWS's.
- A daily ETL pipeline copies transactional data — hundreds
  of gigabytes and rising — from RDS on AWS into BigQuery
  on GCP. The pipeline works. Nobody looks at the AWS
  data-egress line on the monthly bill for two quarters.
- Six months in, the data-egress line is a material fraction
  of the AWS spend and is growing linearly with usage. The
  team either eats the cost, re-architects to keep the
  warehouse on the same cloud (a Redshift or Snowflake-on-
  AWS migration, itself an engineer-quarter), or accepts a
  compressed / incremental ETL redesign that trades data
  freshness for cost.

Portfolio verdict: **the egress trap should have been named
in the ADR that chose BigQuery**. Not as "don't choose
BigQuery" — the analytics benefits may well justify the
cost — but as "here is the egress consequence, here is the
reopening trigger (egress line exceeds X% of AWS spend), and
here is the mitigation path". This is the discipline
chapter 06's scorecard formalises across all vendor
choices.

## Common failure modes

- **Modelling the on-demand headline.** A cost model that
  uses on-demand pricing forever underestimates spend at
  scale (misses the reserved-capacity opportunity) and
  overestimates the runway impact (misses the credits and
  volume-discount realities). Model the pricing you plan to
  graduate into.
- **Ignoring egress until the bill spikes.** The egress line
  is invisible until the volume crosses a threshold, then
  becomes the largest line. Instrument egress from the
  first month and put a monitor on it.
- **Multi-cloud-as-hedge at seed.** Splitting the stack
  across two clouds "for optionality" without a specific
  customer or capability reason. The optionality is worth
  less than the operational cost.
- **Credit-driven architecture.** A managed service adopted
  because it is credited but with no OSS-compatible
  interface (chapter 06). The lock-in outlasts the credit.
- **No cost-per-customer view.** The cloud bill is tracked
  at the total-spend level but never divided by active
  customers or by unit-of-work. Unit-cost visibility is
  what turns the cloud line from a fixed cost into a
  variable the CTO and CEO can steer. See
  [`mod-108`](../mod-108-cto-ceo-and-board-communication/)
  on how this becomes part of the CTO's board pre-read.

## Summary

- The hyperscale clouds are **for-profit economic actors**.
  Pricing structure (on-demand headline, reserved capacity,
  spot, serverless), credits programmes, egress, and managed-
  service lock-in are all deliberate commercial decisions —
  not features of nature.
- **Egress is the single most under-modelled line** in the
  cloud bill. Design decisions that pull data across cloud
  boundaries or out to end-users at scale should be
  explicit ADRs.
- **Credits are real** but do not architect against them.
  Model post-credit pricing when checking unit economics;
  use the credits for the workloads runway would not
  otherwise fund; prefer OSS-fallback interfaces (chapter
  06) even under credits.
- **Lock-in is a spectrum** — compute and object storage are
  near-commodity; managed serverless, data warehouses, and
  provider-specific ML platforms are deep. Name the
  lock-in in the ADR that accepts it.
- **Multi-cloud is almost never the seed-stage default.** A
  single cloud with named lock-in and an explicit reopening
  trigger is the defensible posture.
- The cloud row on the chapter-01 build-vs-buy matrix
  deserves a corresponding ADR and — for any startup where
  cloud is a material cost line — its own quarterly review
  alongside the ADR-index review.

The chapter's paired exercise —
[`exercise-02-cloud-provider-economic-comparison.md`](exercises/exercise-02-cloud-provider-economic-comparison.md)
— walks a structured comparison of the three hyperscalers
against a realistic seed-stage workload, ending with a
defensible ADR-shaped recommendation. Chapter 03 picks up on
the managed-vs-self-hosted trade-off inside whichever cloud
you land on.
