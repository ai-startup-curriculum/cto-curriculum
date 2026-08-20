# Exercise 03 — Managed vs. Self-Hosted Drill for Three Categories

**Module:** `mod-103-build-vs-buy-and-platform-economics`
**Planned time:** ~2.5 hours
**Chapter this builds on:** [`03-managed-vs-self-hosted-classic-categories.md`](../03-managed-vs-self-hosted-classic-categories.md)

## Problem statement

Pick **three** of the classic categories from chapter 03 —
data warehouse, auth / identity, payments, observability,
CI / CD, feature flags — and for each, resolve the managed
vs. self-hosted call for your (or a real reference) startup.
Answer each with the category-specific decision-forcing
questions from chapter 03, not with a generic default, and
land each in an ADR.

The point of the drill is not to pick "the right vendor" in
each category. It is to force the category-specific
questions — the ones that actually decide the answer —
into a per-category writeup that a future maintainer, a
new engineering hire, or a due-diligence reviewer can
consume.

## Requirements

Produce **one writeup per category (three total)**, each on
roughly one page. Each writeup is anchored to an ADR (per
[`mod-102` chapter 02](../../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md))
and updates the relevant row on your build-vs-buy matrix
(exercise 01).

### Choosing the three categories

The three must span at least two of the following axes so
you exercise the frame across different pressures:

- One category where **operational-burden avoidance** is
  likely to dominate (observability, CI/CD, warehouse) —
  because ops-heavy self-host is where team-time cost
  bites earliest.
- One category where **compliance surface** is likely to
  dominate (identity, payments) — because
  compliance-heavy categories force different vendor
  scoring than convenience-driven ones.
- One category where **OSS parity has caught up** and the
  self-hosted option is genuinely competitive (feature
  flags, observability with OpenTelemetry, warehouse with
  Iceberg + Trino / DuckDB, identity with Keycloak) —
  because these are the categories where the decision is
  actually close.

Any three across those axes work. Do not pick three that
would all resolve to "buy managed SaaS from vendor X" for
obvious reasons; the drill has more value on the categories
where the answer is contested.

### Per-category writeup structure

Each of the three writeups has the same shape.

**1. The decision-forcing questions.** Reproduce the
category-specific questions from chapter 03 as a bulleted
list. Answer each in one line for *your* startup. Do not
copy generic answers.

Example (for data warehouse):

- *What's the analytics load this quarter?* — 100M events
  per month, growing, primarily BI queries for the
  internal team plus one enterprise customer's admin
  dashboard.
- *Where does the data live already?* — Postgres RDS on
  AWS; app runs on AWS.
- *Who runs it?* — nobody today; the founding team has no
  operational bandwidth for a warehouse.
- *What's the query-cost trajectory?* — <unknown at this
  stage; the reopening trigger for this ADR will be when
  the warehouse bill crosses X% of the AWS spend>.

**2. The candidate options.** Enumerate 3-5 realistic
options — a fully-managed SaaS, a cloud-managed service on
your existing cloud, and a self-hosted OSS option at
minimum. Cite the vendor / project page for each. Do not
enumerate every option that exists; enumerate the ones you
would actually consider.

**3. The disposition and one-paragraph reasoning.** Pick
one — managed SaaS / cloud-managed / self-hosted — and
justify it in one paragraph. The justification must
reference the decision-forcing questions from step 1, not
generic vendor virtues.

**4. The ADR.** Author a full Nygard-format ADR in
`docs/adr/` in the same repo as your other ADRs. Title,
Status, Context (linking the category writeup), Decision,
Consequences (Positive / Negative / Deferred), Reopening
Trigger.

**5. The switching-cost estimate.** In one paragraph, name
what it would take to reverse this decision — engineer-time,
data migration, compliance re-attestation, team retraining.
This becomes an input to the exercise-05 scorecard when the
scorecard is authored for this category.

### Matrix update

After the three writeups, update the corresponding rows on
your build-vs-buy matrix (exercise 01) to reflect the
per-category resolution. Add a "scorecard link" or "ADR
link" column entry where none existed before.

### The meta-question

After the three writeups and the matrix update, write
**200-400 words** answering:

- Of the three categories you worked, which one had the
  most **surprising** answer — the one where you started
  with an aesthetic bias and the frame changed the call?
- Which category, if any, is a candidate for **hybrid**
  — where you would buy managed for one segment of the
  workload and self-host for another (a common pattern
  in observability: managed Datadog for the on-call
  workflow, self-hosted Prometheus for the high-volume
  raw metrics that would break the Datadog budget)? If
  hybrid, name explicitly what each side owns.

## Starter guidance

- **Payments is not the "surprising" category.** For
  almost every seed-stage startup, payments resolves to
  a card-not-present processor SaaS on PCI-scope-
  reduction grounds. If you pick payments as one of the
  three, do it for the drill on scoring the specific
  processor (Stripe vs. Adyen vs. Braintree), not for
  the managed-vs-self-host resolution.
- **Do not enumerate every OSS project in a category.**
  Pick the one or two OSS options that would realistically
  be in scope for your team's operational bandwidth. A
  five-option comparison is inertia; a two-or-three
  option comparison is a decision.
- **Cite the vendor / project pages.** Every option gets
  a source link — vendor pricing page for SaaS, project
  home for OSS. The reader should be able to follow the
  link to check your claims.
- **Chapter 05's Radar / Landscape reading is legitimate
  context.** Cite them where relevant, in the form
  chapter 05 recommends (edition / retrieval date /
  specific reasoning that applies to you) — not as the
  argument.
- **The "team has operated this before" input matters.**
  A self-hosted stack the team has never run in
  production is a different risk than a self-hosted
  stack the founding engineer ran at their previous
  company. Name the prior-experience input explicitly in
  the writeup.

## Acceptance criteria

Your three category writeups are complete when a reader
(a first engineering hire, a technical advisor, a
due-diligence reviewer) can:

- Read each writeup standalone and understand which
  managed / cloud-managed / self-hosted option was
  chosen for that category and *why*, without asking a
  follow-up question.
- Cross-reference each writeup to the ADR that captures
  the decision and to the row on the build-vs-buy matrix
  that the ADR updates.
- Read the switching-cost paragraph and follow the effort
  estimate the CTO is committing to if the reopening
  trigger fires.
- Identify at least one category where the frame changed
  the CTO's initial aesthetic bias (from the meta-
  question paragraph).

The three ADRs from this exercise feed into exercise 05,
where at least one of them becomes the anchor for the full
vendor-selection scorecard.
