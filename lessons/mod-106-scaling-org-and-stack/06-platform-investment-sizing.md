# Platform Investment Sizing per Stage

> "The team's velocity does not cliff at 15 or 50
> engineers *by accident*. It cliffs because the
> platform investment that would have prevented the
> cliff was not sized for the transition." Platform
> investment sizing is the discipline of *anticipating*
> the tax that CI, deploy infrastructure, observability,
> and developer tooling will impose at the next stage —
> and pre-paying enough of it to keep the DORA numbers
> from regressing.

## Motivation

Every CTO has watched — or lived — a version of this
sequence: the team hits 15 engineers; the CI pipeline
that took 2 minutes at 5 engineers now takes 25 minutes
because of the accumulated test suite; Lead Time for
Changes doubles; the team's morale drops; three engineers
quietly re-negotiate their work to avoid the CI queue.
Same story at 50: the observability stack that worked
for one product team is opaque across five teams; every
incident starts with an hour of *"whose log stream is
this?"*; MTTR climbs from thirty minutes to three
hours.

These are not accidents. They are the predictable
outcome of *under-investing in platform capacity in the
stage before the cliff*. The DORA numbers (chapter 05)
are the leading indicator; the platform investment is
the lever.

This chapter names the **four platform categories**
that need explicit sizing at each transition — test
infrastructure, deploy infrastructure, observability,
and developer platform — and gives a per-stage sizing
heuristic for each. The chapter's discipline is
*deliberately* under-investing before the earn-its-keep
test passes (chapter 03) and *deliberately*
over-investing before the cliff appears.

## The four platform categories

- **Test infrastructure** — CI runners, test-data
  management, test parallelism, ephemeral
  environments, contract-test frameworks. The category
  that determines whether CI stays fast as the test
  suite grows.
- **Deploy infrastructure** — CD pipelines, deployment
  automation, feature flags, canary / blue-green /
  progressive rollout mechanisms, rollback tooling.
  The category that determines whether Deployment
  Frequency stays high as the surface area grows.
- **Observability** — logging, metrics, distributed
  tracing, alerting, dashboards, error tracking. The
  category that determines whether MTTR stays low as
  the system complexity grows.
- **Developer platform** — internal developer portal,
  service catalogue, scaffolding / templates,
  self-service infrastructure, environment management,
  documentation tooling. The category that determines
  whether new engineers ramp fast and existing
  engineers stay in flow as the org grows.

The four are not independent. Test infrastructure feeds
deploy infrastructure (a fast, reliable test suite is a
precondition for continuous deployment); observability
feeds developer platform (a shared observability
substrate is the substrate the developer portal
integrates against). The 15-50 sizing exercise usually
plans them in order, with the earlier categories'
investments as prerequisites for the later ones.

## Sizing at 0-5 engineers

The 0-5 sizing question is *"what is the smallest thing
that works, and how much of the team's time can I
justify spending on it"*. The rough answer: **no
dedicated platform investment; a handful of
foundational decisions covered in chapter 01**.

Per category:

- **Test infrastructure.** The CI pipeline from
  chapter 01. One workflow file. No dedicated CI
  runners. The public GitHub Actions / GitLab CI
  runners are sufficient. Total investment: hours,
  not weeks.
- **Deploy infrastructure.** Deploy from `main` on
  every green build, using the CI system's built-in
  deployment integration. Vercel, Render, Fly, Railway,
  and the major cloud PaaS options all support this
  out of the box. Total investment: hours.
- **Observability.** Application logs to standard
  output; a hosted log aggregator (Datadog, Grafana
  Cloud, Better Stack, Axiom) collecting them; a
  single dashboard the CTO looks at daily; error
  tracking via Sentry or the equivalent. Total
  investment: hours; the standing cost is the SaaS
  fees.
- **Developer platform.** The README in the repo.
  The engineering handbook from chapter 02 is *not
  yet* an artifact — the 0-5 team is too small. The
  `README.md` and `docs/setup.md` are the developer
  platform.

The 0-5 discipline: *do not hire a platform engineer at
this stage*. Every hire is a stream-aligned product
engineer. If the CI is taking too long or the deploy is
too manual, the fix is the CTO or a rotating product
engineer spending a Friday on it, not a dedicated hire.

The earn-its-keep test from
[`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md)
almost never passes at 0-5.

## Sizing at 5-15 engineers

The 5-15 sizing question is *"what do we need to add
in the next two quarters so that the 15-engineer team
does not cliff"*. The rough answer: **~10% of one
engineer per category, allocated to a rotating
product-engineer volunteer, coordinated by a senior
IC or the first tech lead**.

Per category:

- **Test infrastructure.** The CI pipeline needs to
  stay under 10 minutes as the test suite grows.
  Concrete investments at this stage: parallelism
  (splitting tests across runners), caching
  (dependency caches, build caches), and dedicated CI
  runners if the public runners become the bottleneck.
  The load-bearing reference on the discipline of a
  fast, reliable test suite is Michael Nygard's
  *Release It!*
  ([pragprog.com/titles/mnee2/release-it-second-edition](https://pragprog.com/titles/mnee2/release-it-second-edition/))
  and *Continuous Delivery*
  ([continuousdelivery.com](https://continuousdelivery.com/))
  by Jez Humble and David Farley.
- **Deploy infrastructure.** Feature flags become
  load-bearing at this stage — the first launched
  feature that needs to be gated to a subset of users
  is usually engineer #8 or #9. LaunchDarkly
  ([launchdarkly.com](https://launchdarkly.com/)),
  Unleash
  ([getunleash.io](https://www.getunleash.io/)),
  Flagsmith
  ([flagsmith.com](https://flagsmith.com/)),
  PostHog feature flags
  ([posthog.com](https://posthog.com/)) are the
  common vendor / open-source options. Canary or
  progressive-rollout tooling — Argo Rollouts
  ([argoproj.github.io/rollouts](https://argoproj.github.io/argo-rollouts/)),
  Flagger
  ([flagger.app](https://flagger.app/)) — usually
  becomes worthwhile around engineer #12.
- **Observability.** The three-pillar stack — logs,
  metrics, traces — needs to be in place by the end
  of 5-15. If tracing is not in place, MTTR at 15
  engineers will climb as the number of service
  interactions grows. Load-bearing reference:
  OpenTelemetry
  ([opentelemetry.io](https://opentelemetry.io/)) as
  the instrumentation standard, then any vendor or
  self-hosted stack for storage / query. Honeycomb
  ([honeycomb.io](https://www.honeycomb.io/)) and
  Grafana Tempo
  ([grafana.com/oss/tempo](https://grafana.com/oss/tempo/))
  are commonly used at this scale. On the alerting
  side, the Google SRE book's chapter on
  *Practical Alerting from Time-Series Data* —
  [sre.google/sre-book/practical-alerting](https://sre.google/sre-book/practical-alerting/)
  — is the load-bearing read.
- **Developer platform.** The engineering handbook
  from chapter 02 is now the primary developer-
  platform artifact. Rough contents already covered
  there. No dedicated tooling investment yet.

The 5-15 discipline: still no dedicated platform hire.
The investments are *allocated to a named engineer for
a named quarter* (usually the first tech lead's
technical initiative), with the earn-its-keep test
result documented. The tech-debt inventory format from
[`mod-105` chapter 06](../mod-105-technical-debt-as-business-decision/06-debt-inventory-and-portfolio-decision-log.md)
is a useful shape for the "what platform work is
underway" tracker.

## Sizing at 15-50 engineers

The 15-50 sizing question is *"what does the platform
team, if any, look like — and if there is one, what is
its charter"*. The rough answer: **the first platform
team, of 2-4 engineers, but only if the earn-its-keep
tests from [`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md)
pass** (recapped in chapter 03 artifact 2).

Per category, at 15-50:

- **Test infrastructure.** Under 15 minutes on the
  full suite; test-data management is now a real
  problem (production-like test data without leaking
  production data); ephemeral environments per pull
  request become common (Vercel-style preview
  deployments; kubernetes ephemeral namespaces). The
  first platform team's charter often includes
  test-infrastructure ownership.
- **Deploy infrastructure.** CD is fully automated
  from `main`. Progressive rollout is in place
  (canary or blue-green). Rollback is one command or
  one dashboard click. Multi-environment deploys
  (staging, production, sometimes region-specific
  environments) are managed. Argo CD
  ([argoproj.github.io/cd](https://argo-cd.readthedocs.io/en/stable/)),
  Flux
  ([fluxcd.io](https://fluxcd.io/)), Spinnaker
  ([spinnaker.io](https://spinnaker.io/)) are
  common vendor / open-source options.
- **Observability.** SLI / SLO / error-budget
  practice becomes real at this scale. Google SRE
  workbook —
  [sre.google/workbook/table-of-contents](https://sre.google/workbook/table-of-contents/)
  — chapters on SLOs and error budgets are the
  load-bearing reads. Trace-based debugging
  (Honeycomb, DataDog APM, OpenTelemetry + Grafana
  Tempo) is now table stakes; if it is not in place,
  MTTR at 30+ engineers will be a chronic complaint.
- **Developer platform.** The internal developer
  portal question appears at this scale. Backstage
  ([backstage.io](https://backstage.io/)) is the
  open-source reference implementation, from Spotify;
  OpsLevel, Cortex, Port are commercial alternatives.
  The service catalogue — the *"what services do we
  have, who owns each, what is its dependency graph"*
  register — is usually the first developer-platform
  investment.

The 15-50 discipline: **the platform team is subject to
earn-its-keep, and the charter is a time-boxed pilot**.
See chapter 03 artifact 2 for the framework. Concrete
first platform-team charters that commonly earn-their-
keep in this order at 15-50:

1. Build / CI-and-deploy platform (the first, because
   CI is the shared bottleneck by ~15 engineers).
2. Shared observability stack (the second, driven by
   the second or third serious production incident).
3. Shared data platform (the third, driven by CEO
   ask for self-serve product analytics).
4. Internal developer portal / service catalogue
   (the fourth, and often premature at this stage —
   defer until the org has 30+ services).

The 15-50 anti-pattern: the CTO reads a big-tech
platform-engineering blog post (Uber, Airbnb, Netflix)
and tries to import the whole stack. The imported
stack has a build cost of 3-5 engineer-years and the
org has 30 engineers total. Read the blog posts as
directional references, not as targets. See
Team Topologies
([teamtopologies.com](https://teamtopologies.com/))
on the *platform-team* interaction mode: the platform
team's success is measured by the stream-aligned
teams' velocity, not by the platform team's
sophistication.

## Sizing at 50-150 engineers

The 50-150 sizing question is *"how do we prevent the
cliff at 100 engineers, and where do we defer the deep
technical depth to a senior architect we have hired"*.
The rough answer: **multiple platform teams, each with
a specific charter; deep technical architecture
delegated to a hired senior architect or principal
engineer**.

Per category, at 50-150:

- **Test infrastructure.** Under 20 minutes on the
  full suite even as the test count doubles. Test
  reliability (flake rate) becomes a first-order
  metric. The dedicated test-platform team, if any,
  owns this.
- **Deploy infrastructure.** Multi-region deployments
  may be entering scope, especially if the product
  has entered a regulated or data-residency market.
  This is the point at which the boundary to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) becomes structural — the CTO does not
  personally design the multi-region deploy control
  plane; a hired senior architect does.
- **Observability.** SLO / error-budget practice is
  the default, not a novelty. Per-team error budgets
  interact with the delivery cadence (chapter 07).
  Cost of the observability stack itself becomes a
  budget-line-item concern; per-team retention
  policies, sampled tracing, and cost-aware alerting
  become common. The OpenTelemetry ecosystem's
  documentation at
  [opentelemetry.io/docs](https://opentelemetry.io/docs/)
  is the substrate reference.
- **Developer platform.** The internal developer
  portal / service catalogue is now load-bearing.
  Backstage
  ([backstage.io](https://backstage.io/)) or
  equivalent is the substrate. The
  platformengineering.org community —
  [platformengineering.org](https://platformengineering.org/)
  — publishes the vocabulary and the reference
  patterns.

The 50-150 discipline: **the platform-team charters are
now the CTO's / VP Eng's primary vehicle for shaping
engineering velocity**. Each platform team has an
earn-its-keep test that is measured continuously (not
just at charter time), and a platform team that is not
earning its keep is disbanded or re-chartered.

The deferrals to
[`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
(level 45) at this stage typically include:

- The multi-region / data-residency architecture.
- The multi-tenancy isolation model at scale (silo /
  pool / bridge — see the AWS SaaS Lens
  ([docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html](https://docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html))).
- The distributed-consensus / storage-layer choices
  for a scale-critical subsystem.
- The bespoke platform layer (a custom scheduler, a
  custom storage engine, a custom networking layer),
  if the product actually needs one.

The deferrals to
[`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
(level 55) at this stage typically include:

- Cross-region / multi-cloud strategy at scale.
- Compliance-critical architecture decisions
  (FedRAMP, HIPAA at scale, SOC 2 Type II — with
  [`mod-107`](../mod-107-founder-scope-security-and-compliance/README.md)
  as the CTO-scope adjacent module).
- The multi-year platform-team roadmap that spans
  multiple platform teams.

The CTO's job at 50-150 with these deferrals is
*approving the architect's proposal, understanding it
well enough to defend it to the board, and ensuring it
fits the company strategy* — not authoring it. See
chapter 04 on the CTO-role delta.

## The earn-its-keep test applied to platform work

Every platform investment at 5-15, 15-50, and 50-150
runs the earn-its-keep test from
[`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md).
The applied version for the four categories:

- **Test infrastructure.** Named internal customer:
  the teams whose CI queue is the current
  bottleneck. Sized carry-cost: how many engineer-
  hours per week are lost to slow CI? Explicit-vs-
  buy alternative: is there a hosted-CI vendor
  (Buildkite, CircleCI Cloud, GitHub Actions Larger
  Runners) that would solve the problem?
- **Deploy infrastructure.** Named internal
  customer: the teams whose Deployment Frequency is
  currently constrained by manual steps. Sized
  carry-cost: how much of the DORA lead-time is
  the deploy step? Explicit-vs-buy alternative:
  hosted CD (Vercel, Render, Fly, Railway,
  Cloudflare, Netlify) or hosted GitOps tools?
- **Observability.** Named internal customer: the
  teams currently paying the *"whose log stream is
  this"* tax during incidents. Sized carry-cost:
  MTTR delta attributable to observability gaps.
  Explicit-vs-buy alternative: the major
  observability vendors, most of which are
  substantially cheaper than a build-from-scratch
  team.
- **Developer platform.** Named internal customer:
  the ramp-up time for new engineers, the
  onboarding-checklist completion time, the cost
  of running each new service through a
  manual-review gate. Sized carry-cost: hours per
  week across the whole team. Explicit-vs-buy
  alternative: hosted service-catalogue tools.

The failure mode: the platform team is chartered
without any of the four tests passing, on the theory
that *"it is important that we have a platform team"*.
See
[`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md)
on the *"build because we want to be seen to build"*
pattern.

## Summary

- **Four platform categories** need explicit sizing
  at each transition: **test infrastructure**,
  **deploy infrastructure**, **observability**, and
  **developer platform**.
- **0-5** — no dedicated platform investment; the
  four foundational decisions from chapter 01. No
  platform hire.
- **5-15** — ~10% of one engineer per category,
  rotating product-engineer allocation, coordinated
  by the first tech lead. Feature flags, tracing,
  and CI parallelism become load-bearing. No
  dedicated platform hire.
- **15-50** — first platform team of 2-4 engineers,
  *if the earn-its-keep tests pass* (chapter 03
  artifact 2). Common charter order: build-and-
  deploy → observability → data platform →
  internal developer portal. Anti-pattern:
  importing a big-tech platform stack wholesale.
- **50-150** — multiple platform teams, each
  earn-its-keep-tested continuously. Deep
  architectural depth (multi-region, multi-tenancy,
  distributed-consensus, bespoke platform layer)
  delegated to a hired
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) or
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55) — *not* to the CTO.
- **Load-bearing references** by category:
  *Continuous Delivery*
  ([continuousdelivery.com](https://continuousdelivery.com/))
  and Nygard's *Release It!*
  ([pragprog.com/titles/mnee2/release-it-second-edition](https://pragprog.com/titles/mnee2/release-it-second-edition/))
  for the test / deploy discipline; the Google SRE
  book chapters on alerting
  ([sre.google/sre-book/practical-alerting](https://sre.google/sre-book/practical-alerting/))
  and SLOs
  ([sre.google/sre-book/service-level-objectives](https://sre.google/sre-book/service-level-objectives/))
  for the observability discipline; Team Topologies
  ([teamtopologies.com](https://teamtopologies.com/))
  and platformengineering.org
  ([platformengineering.org](https://platformengineering.org/))
  for the developer-platform discipline.
- **Every investment runs the earn-its-keep test**
  from
  [`mod-103`](../mod-103-build-vs-buy-and-platform-economics/README.md).
  The platform team is subject to the same
  discipline as any other build-vs-buy decision.

The chapter's paired exercise —
[`exercise-06-platform-investment-sizing-per-stage.md`](exercises/exercise-06-platform-investment-sizing-per-stage.md)
— asks you to size the four categories at each of the
four stages, with per-stage investment rationale, the
earn-its-keep test result, and the deferral list to
[`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning).

Chapter 07 walks the delivery-cadence and on-call
design — the weekly rhythm, the kanban-vs-sprint call,
the on-call rotation shape, the blameless post-mortem
template, and the incident-response playbook that
closes the loop from an incident back to the debt
portfolio and the DORA numbers.
