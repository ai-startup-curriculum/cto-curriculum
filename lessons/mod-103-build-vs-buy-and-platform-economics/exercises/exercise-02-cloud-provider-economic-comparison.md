# Exercise 02 — Cloud-Provider Economic Comparison

**Module:** `mod-103-build-vs-buy-and-platform-economics`
**Planned time:** ~2.5 hours
**Chapter this builds on:** [`02-cloud-providers-as-economic-actors.md`](../02-cloud-providers-as-economic-actors.md)

## Problem statement

Author a structured economic comparison of **AWS, Google
Cloud, and Microsoft Azure** against a specific, realistic
seed-stage workload profile of your choosing. Land the
comparison in a defensible ADR-shaped recommendation with an
explicit reopening trigger.

The point of the drill is not to declare a "winner". It is
to make the cloud choice a *defensible* one — grounded in
your specific workload shape, priced against the discount
mechanism you plan to graduate into (not the on-demand
headline), and honest about the lock-in and egress
consequences of the choice.

## Requirements

Produce a **one-page comparison worksheet** plus a
**one-page ADR** that recommends and justifies the choice.

### Part 1 — the workload profile

Before you can compare, name the workload. In one page:

- **Product one-liner.** Who buys the product, what it
  does.
- **Load-bearing workload shape**, in explicit terms.
  Address at minimum:
  - Expected steady-state compute footprint over the next
    12 months (approximate vCPU-hours / month, or "small
    / medium / large" against your judgment).
  - Expected data-egress volume (both public-internet
    egress and any cross-cloud data movement — see the
    egress trap in chapter 02).
  - Expected object-storage volume and access pattern
    (hot / warm / cold).
  - Whether the workload is bursty (spot / preemptible
    viable) or steady (reserved capacity viable) or
    serverless-shaped (per-request pricing viable).
  - Any managed-service capabilities you consider
    non-negotiable at seed (managed Postgres, managed
    Kubernetes, managed OIDC, managed queues, managed
    warehouse, etc.).
- **Data-residency / compliance constraints**, if any —
  regions you must be in, regulated jurisdictions you
  sell into, HIPAA / GDPR / FedRAMP posture.
- **Team-context.** Which cloud(s) has the founding
  engineering team operated in production before?

Do not invent numbers you don't have. Where uncertainty is
material, write "small / medium / large" or "unknown —
placeholder" rather than a plausible-looking number.

### Part 2 — the comparison worksheet

For each of AWS, GCP, and Azure, fill in a common
worksheet. Use the vendor's current published pricing pages
(links in chapter 02 and the module's [`resources.md`](../resources.md))
as your source; do not cite generic industry averages.

Minimum columns to compare:

- **On-demand compute pricing** for a representative
  instance type that would host your steady-state
  workload. Cite the vendor page and the region you
  priced.
- **Reserved / committed-use discount rate** available at
  a 1-year commitment for that instance type. Cite the
  vendor page.
- **Spot / preemptible availability and pricing** for
  the same instance family (for the batch / interruption-
  tolerant portion of your workload, if any).
- **Object storage** — per-GB-month for the standard tier
  in the region you priced.
- **Egress pricing** — per-GB rate for internet egress at
  the volume tier you expect.
- **Managed Postgres** (or your primary data store) —
  pricing at the instance class you'd start with.
- **Availability of the credits programme** relevant to
  your stage (AWS Activate, Google for Startups Cloud
  Program, Microsoft for Startups Founders Hub — see
  chapter 02). Note the credit tier your accelerator /
  investor affiliation qualifies you for, if known.
- **Compliance posture** — SOC 2 / HIPAA-BAA / GDPR-DPA
  posture for the specific services you plan to consume.
- **Regional coverage** for the specific regions your
  data-residency profile requires.

### Part 3 — the egress-and-lock-in analysis

Two sub-analyses that the vendor comparison pages will not
give you:

- **Egress trajectory.** Model the monthly egress bill on
  each cloud at your expected 12-month workload. Which
  cloud is cheapest at your specific egress profile? What
  design decision (a specific CDN, a specific
  cross-cloud pipeline, a decision to host media on the
  same cloud as compute) would change that answer
  materially?
- **Lock-in inventory.** For each cloud, list the managed
  services you would rely on and score each against the
  low / medium / high / very-high lock-in taxonomy from
  chapter 02. Which cloud has the highest total lock-in
  under your plan, and why?

### Part 4 — the ADR

Author a Nygard-format ADR (per
[`mod-102` chapter 02](../../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md))
that lands the recommendation. Requirements:

- **Title.** "Use $CLOUD as the primary cloud provider" or
  equivalent imperative statement.
- **Status.** `Proposed` is acceptable; `Accepted` if the
  decision is already committed.
- **Context.** Reference the workload profile from Part 1;
  cite the vendor pricing pages you used in Part 2 with
  the retrieval date.
- **Decision.** One paragraph. If the recommendation is
  multi-cloud, defend it against the "usually the wrong
  default" argument in chapter 02.
- **Consequences.** Positive / Negative / Deferred, using
  ISO/IEC 25010 vocabulary (see
  [`mod-102` chapter 04](../../mod-102-architecture-under-uncertainty/04-iso-25010-quality-attribute-trade-offs.md))
  where relevant. At minimum, name the lock-in accepted
  and the egress exposure.
- **Reopening trigger.** The observable condition (an
  egress bill crossing a threshold, a customer
  data-residency requirement, a specific managed-service
  gap, a credit expiry) that would force the ADR to be
  superseded.

## Starter guidance

- **Read the vendor pricing pages yourself.** Every
  training deck (this one included) becomes stale within
  weeks. The AWS
  ([aws.amazon.com/ec2/pricing/on-demand](https://aws.amazon.com/ec2/pricing/on-demand/)),
  GCP
  ([cloud.google.com/compute/all-pricing](https://cloud.google.com/compute/all-pricing)),
  and Azure
  ([azure.microsoft.com/pricing/details/virtual-machines/linux](https://azure.microsoft.com/en-us/pricing/details/virtual-machines/linux/))
  compute-pricing pages are the sources. Cite the
  retrieval date in the ADR context.
- **Model post-credit pricing when checking unit
  economics.** Chapter 02's discipline: credits are real,
  but a business whose unit economics only work while
  credited is a business that becomes unprofitable when
  the credit expires.
- **Do not fill in numbers you don't know.** If you don't
  know a vendor's SLA, egress tier, or reserved-instance
  discount off the top of your head, look it up or write
  `<check: link to vendor page>`. Making up numbers is
  the failure mode this exercise exists to prevent.
- **Feature-matrix vs. economics.** This exercise is the
  economics exercise. Managed-service *feature*
  comparison (which Postgres has better vacuum tuning?
  which managed Kubernetes has better upgrade UX?) is
  legitimately interesting but is not the point here —
  save the feature comparison for the per-service
  scorecard in exercise 05.
- **If your workload is genuinely tiny** (very early stage,
  pre-launch), the exercise is still useful — it forces
  you to name what you expect the workload to look like
  when you have the traffic to defend an ADR on. The
  reopening trigger becomes "when actual workload
  deviates materially from the assumption above".

## Acceptance criteria

Your comparison is complete when a reader (a co-founder, a
technical advisor, a due-diligence reviewer, a lead
investor) can:

- Read the workload profile and understand your specific
  situation, distinct from a generic startup.
- Read the comparison worksheet and follow which numbers
  you sourced from where — every price cell has a
  citation.
- Read the egress trajectory and the lock-in inventory
  and see that the *strategic* consequences of the
  choice — not just the sticker price — were reasoned
  about.
- Read the ADR and follow the decision to its explicit
  reopening trigger, without needing to ask "but what
  about X?"
- Identify at least one *counter-recommendation* — the
  strongest argument for choosing a *different* cloud
  than you recommended — and see that the ADR
  acknowledges it rather than pretending it doesn't
  exist.

The output of this exercise updates the cloud-provider row
of your build-vs-buy matrix (exercise 01) and becomes the
depth reference for the scorecard in exercise 05 when the
cloud is the vendor decision the scorecard is authored
against.
