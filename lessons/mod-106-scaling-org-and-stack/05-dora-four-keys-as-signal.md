# DORA Four Keys as Signal, Not Goal

> "When a measure becomes a target, it ceases to be a
> good measure." — Marilyn Strathern (1997), often
> cited as *Goodhart's Law* after Charles Goodhart's
> 1975 monetary-policy paper
> ([oro.open.ac.uk/22183](https://oro.open.ac.uk/22183/)).
> The DORA four-key metrics are the most useful
> measurement instrument the CTO has for engineering
> delivery — *and* the metric most vulnerable to the
> failure mode Strathern named.

## Motivation

Every founder-CTO reaches a point at which someone
external — a CFO, a board member, a new VP Eng
candidate — asks *"how do you measure engineering
performance?"* The bad answers are well documented:
lines of code, story points, hours worked, features
shipped. The good answer, for the last ten years, has
been the **DORA four keys**: Deployment Frequency,
Lead Time for Changes, Change Failure Rate, and Mean
Time to Restore (sometimes called Time to Restore
Service).

The DORA program at [dora.dev](https://dora.dev/) —
originally the DevOps Research and Assessment team, now
part of Google — has published the annual *State of
DevOps Report*
([dora.dev/research](https://dora.dev/research/))
since 2014 with a large multi-year survey backing the
claim that these four metrics correlate with
organisational performance across a wide range of
industries. The book-length treatment is Nicole
Forsgren, Jez Humble, and Gene Kim's *Accelerate*
([itrevolution.com/product/accelerate](https://itrevolution.com/product/accelerate/)),
which is the load-bearing reference for the four keys.

The reason DORA gets its own chapter in this module is
that it is the measurement instrument that runs through
*all four* stage transitions — 0-5 baseline, 5-15
diagnostic, 15-50 team-level scoreboard, 50-150
per-team dashboard — and each transition has a
different failure mode of the metric.

## The four metrics — definitions

The DORA definitions, as published by the DORA program
and *Accelerate*:

- **Deployment Frequency.** How often the organisation
  successfully deploys to production. Measured as a
  rate (per day, per week, per month) or a bucket
  (elite / high / medium / low).
- **Lead Time for Changes.** The time from a code
  change being committed to that change being
  successfully running in production. Measured as a
  duration (minutes / hours / days / weeks / months) or
  a bucket.
- **Change Failure Rate.** The percentage of changes to
  production that result in degraded service and
  require remediation (rollback, hotfix, forward-fix).
  Measured as a percentage.
- **Mean Time to Restore.** How long, on average, it
  takes to restore service after a production incident.
  Measured as a duration. (The DORA program has, in
  more recent reports, sometimes renamed this
  *"failed deployment recovery time"* to distinguish
  from generic MTTR; the concept is the same.)

The four keys are grouped into two pairs — Deployment
Frequency and Lead Time as **speed / throughput**
metrics, Change Failure Rate and MTTR as **stability**
metrics. The *Accelerate* research finding is that
top-performing organisations achieve *both* pairs
simultaneously: they deploy faster *and* have fewer
failures. The historical management assumption that
speed trades off against stability is not supported by
the data.

## The bands — situating tool, not target

The *State of DevOps Report* publishes annual
performance bands — elite, high, medium, low — for each
of the four metrics. The exact band cutoffs shift year
to year as the industry baseline moves, so this chapter
does not pin specific numbers to specific bands;
consult the current
[dora.dev/research](https://dora.dev/research/) report
for the current-year cutoffs.

The rough shape as of recent reports:

- **Elite** — deploys multiple times per day; lead time
  measured in hours; change failure rate under ~10%;
  MTTR under an hour.
- **High** — deploys between once per day and once per
  week; lead time measured in days; change failure rate
  under ~15-20%; MTTR under a day.
- **Medium** — deploys between once per week and once
  per month; lead time measured in days to weeks;
  change failure rate under ~30%; MTTR under a day to a
  week.
- **Low** — deploys less than once per month; lead
  time measured in weeks to months; change failure
  rate ~30-45%; MTTR measured in days.

The critical point: **these bands are a situating tool,
not a target**. Two reasons:

- The bands are population statistics from a survey of
  thousands of organisations across many industries. A
  particular org's *appropriate* target depends on its
  domain (a medical-device company, a regulated
  financial-services company, and a consumer SaaS
  company have legitimately different appropriate
  targets). Blindly adopting the "elite" band as a
  target imports assumptions from a survey that did
  not sample your domain.
- The bands describe *symptoms* of a healthy
  engineering practice, not the practice itself. An
  org that hits the elite band by rushing changes
  through with lower testing coverage will discover the
  band was papering over a real drop in stability.

The DORA program's own guidance is explicit about this
— see the framing in the annual report and the
[dora.dev quickcheck](https://dora.dev/quickcheck/)
tool, which is a diagnostic rather than a scoreboard.

## The three failure modes

The four-key vocabulary has been in wide use for eight
years and three specific failure modes have emerged in
the founder-CTO community. Each is worth naming
explicitly.

### Failure mode 1 — Goal-ification (Goodhart's Law)

The metric becomes the goal. Concrete symptoms:

- The team's OKR is *"Deployment Frequency > 5 per
  day"*. Engineers start splitting a coherent change
  into five artificial deploys to hit the number. The
  metric goes up; the underlying practice does not
  improve.
- The team's OKR is *"Change Failure Rate < 5%"*.
  Engineers start not-reporting incidents that would
  otherwise be counted as failures. The metric goes
  down; the underlying stability does not improve.
- The team's OKR is *"MTTR < 15 minutes"*. Engineers
  learn to close incidents as *"resolved"* the moment
  the alert quiets, even if the underlying cause is
  not fixed. The metric goes down; the customer's
  experience is unchanged.

Marilyn Strathern's 1997 formulation —
*"When a measure becomes a target, it ceases to be a
good measure"*
([oro.open.ac.uk/22183](https://oro.open.ac.uk/22183/))
— is the load-bearing observation. The remedy is
*never* to set a DORA number as an OKR or a
performance-review target. The numbers are a
diagnostic, and the diagnostic is only useful if the
team trusts it.

### Failure mode 2 — Single-metric fixation

The team optimises for one of the four metrics and lets
the other three drift. Common shapes:

- **Deployment Frequency-only.** The team deploys many
  times per day and the Change Failure Rate quietly
  climbs to 40%. Customer-facing incidents rise; the
  team-facing dashboard says *"we are elite"*.
- **MTTR-only.** The team gets excellent at rapid
  incident response, and Lead Time for Changes quietly
  climbs to weeks because the team is always in
  firefighting mode.
- **Change Failure Rate-only.** The team introduces a
  heavy review process, gets the failure rate to under
  5%, and Deployment Frequency drops from many-per-day
  to weekly.

The remedy is that the four metrics are read *together*
as a set, not one at a time. The *Accelerate* research
finding — top performers achieve speed and stability
simultaneously — is the framing.

### Failure mode 3 — Cross-team benchmarking

The org reads DORA numbers *across teams* and treats a
lower-performing team as a problem to fix. Two
distortions follow:

- **Different teams have legitimately different
  profiles.** A platform team that ships a
  breaking-change every quarter and a product team
  that ships small changes daily will have very
  different Deployment Frequency numbers — and both
  can be healthy. Ranking them against each other is
  meaningless.
- **The measured team responds by gaming the metric
  rather than improving the underlying practice.** See
  failure mode 1. The moment DORA becomes a comparison
  tool between teams, the numbers stop being trustable.

The remedy is that DORA numbers are read *within* a
team as a trend, not *across* teams as a benchmark.
The exception is a rough industry benchmark against
the DORA report's population bands, which is a
low-frequency check rather than an operational
comparison.

## Where DORA is not enough

DORA measures the *delivery pipeline*. It is silent on
several things a CTO also needs to measure:

- **Developer experience / satisfaction.** Whether the
  team enjoys the work, feels productive, has the
  tools they need. The SPACE framework — Nicole
  Forsgren, Margaret-Anne Storey, Chandra Maddila,
  Thomas Zimmermann, Brian Houck, Jenna Butler,
  *The SPACE of Developer Productivity*, ACM Queue
  2021 —
  [queue.acm.org/detail.cfm?id=3454124](https://queue.acm.org/detail.cfm?id=3454124)
  — is the load-bearing reference. Five dimensions:
  Satisfaction, Performance, Activity, Communication,
  Efficiency & flow. DORA is a subset.
- **Developer experience at the tool level.** Abi
  Noda, Margaret-Anne Storey, Nicole Forsgren, Michaela
  Greiler, *DevEx: What Actually Drives Productivity*,
  ACM Queue 2023 —
  [queue.acm.org/detail.cfm?id=3595878](https://queue.acm.org/detail.cfm?id=3595878)
  — three dimensions: Feedback loops, Cognitive load,
  Flow state. A useful complementary lens.
- **Business outcomes.** DORA correlates with
  organisational performance in the *Accelerate*
  research, but it does not directly measure revenue,
  customer satisfaction, or retention. The 15-50 and
  50-150 CTO reads DORA against the business
  outcomes; a rising DORA number with a falling
  customer-satisfaction number is a warning sign, not
  a win.

The 50-150 CTO commonly maintains a *dashboard* with
the DORA four, a small set of SPACE-inspired
developer-satisfaction questions (usually a quarterly
survey), and the business outcomes (customer
satisfaction, retention, revenue per engineer). None of
these is a scoreboard; each is a diagnostic.

## The ritual — how DORA gets used

The measurement is only as valuable as the ritual that
turns it into a conversation. The ritual per stage:

- **0-5** — the CTO updates the four numbers weekly
  in a spreadsheet. Nobody else looks at it. The
  ritual is habitual, not consequential.
- **5-15** — the weekly cadence meeting starts with
  the four numbers on a shared dashboard. The tech
  leads and the CTO ask *"what changed and why?"* The
  ritual is diagnostic.
- **15-50** — each team owns its own four numbers.
  The team's weekly retro includes a five-minute
  reading of them. The CTO / VP Eng reviews the
  aggregate monthly. The ritual is team-level
  ownership.
- **50-150** — each team's four numbers are visible
  on a per-team dashboard (Backstage / Grafana / a
  vendor tool). The org-level aggregate is a
  quarterly reading. The board pre-read
  ([`mod-108`](../mod-108-cto-ceo-and-board-communication/README.md))
  includes the aggregate with narrative context. The
  ritual is org-level accountability, not
  cross-team benchmarking.

Two references worth having open on the ritual side:

- **The Google SRE book chapter on service-level
  objectives** — [sre.google/sre-book/service-level-objectives](https://sre.google/sre-book/service-level-objectives/).
  Free online. The SLO / error-budget vocabulary is
  what tightens the *stability* side of DORA into an
  operational lever.
- **The Google SRE workbook** —
  [sre.google/workbook/table-of-contents](https://sre.google/workbook/table-of-contents/)
  — the applied companion to the SRE book, with the
  practical shape of SLI / SLO adoption.

## How to measure — data sources and tooling

The four keys, mapped to source data:

- **Deployment Frequency** — deploy log (CI/CD system:
  GitHub Actions, GitLab CI, CircleCI, Buildkite,
  Argo CD, Spinnaker). Count deploys to production
  per unit time.
- **Lead Time for Changes** — the time between a
  commit's first push and its deployment. Requires
  correlating git history with the deploy log.
- **Change Failure Rate** — requires a labelled
  incident stream. Common shapes: an incident
  tracking system (incident.io, PagerDuty, Jira /
  Linear label), or a `hotfix:` / `rollback:` commit
  convention that CI can count.
- **MTTR** — from the incident tracking system: time
  from incident open to incident closed (with the
  discipline of not-closing-until-resolved).

Two open-source tools worth being aware of:

- **DORA's `four-keys` reference implementation** —
  [github.com/GoogleCloudPlatform/fourkeys](https://github.com/GoogleCloudPlatform/fourkeys)
  — an open-source reference implementation showing
  how to derive the four keys from GitHub / GitLab /
  incident-tracking data. Read the source for the
  computation logic even if you use a vendor tool.
- **Grafana + Prometheus / OpenTelemetry** —
  [grafana.com](https://grafana.com/),
  [opentelemetry.io](https://opentelemetry.io/) —
  the substrate most 15-50 orgs use for the dashboard.

Commercial vendor tools that compute DORA include
Sleuth, LinearB, and Jellyfish; the DORA program's
own guidance is that the *data source* and the
*ritual* matter more than the tool. Do not spend
weeks vendor-evaluating before you have the numbers.

## Summary

- The **DORA four keys** — Deployment Frequency, Lead
  Time for Changes, Change Failure Rate, MTTR — are
  the most useful measurement instrument the CTO has
  for engineering delivery. Load-bearing references:
  [dora.dev](https://dora.dev/), the annual *State of
  DevOps Report* at
  [dora.dev/research](https://dora.dev/research/), and
  Forsgren / Humble / Kim's *Accelerate*
  ([itrevolution.com/product/accelerate](https://itrevolution.com/product/accelerate/)).
- The four are grouped into **speed** (Deployment
  Frequency, Lead Time) and **stability** (Change
  Failure Rate, MTTR) pairs. *Accelerate*'s research
  finding: top performers achieve both simultaneously.
- The **elite / high / medium / low bands** are a
  *situating tool*, not a target. Population
  statistics; your appropriate target depends on
  domain. Consult the current annual report at
  [dora.dev/research](https://dora.dev/research/) for
  current cutoffs.
- **Failure mode 1 — Goal-ification** (Goodhart /
  Strathern
  [oro.open.ac.uk/22183](https://oro.open.ac.uk/22183/)):
  DORA becomes an OKR, engineers game the metric.
  Never set a DORA number as a target.
- **Failure mode 2 — Single-metric fixation**: team
  optimises one metric, the other three drift. Read
  the four as a set.
- **Failure mode 3 — Cross-team benchmarking**:
  different teams have legitimately different
  profiles. Read within-team trends, not across-team
  comparisons.
- **Where DORA is not enough** — SPACE
  ([queue.acm.org/detail.cfm?id=3454124](https://queue.acm.org/detail.cfm?id=3454124))
  for developer experience; DevEx
  ([queue.acm.org/detail.cfm?id=3595878](https://queue.acm.org/detail.cfm?id=3595878))
  for tool-level flow / cognitive load / feedback
  loops; business outcomes (retention, satisfaction,
  revenue-per-engineer) as the outer check.
- **The ritual per stage** — 0-5 spreadsheet, 5-15
  cadence-meeting dashboard, 15-50 team-owned
  numbers, 50-150 per-team dashboard + board pre-read
  aggregate.
- **Tooling** — GoogleCloudPlatform/fourkeys
  ([github.com/GoogleCloudPlatform/fourkeys](https://github.com/GoogleCloudPlatform/fourkeys))
  is the open-source reference implementation.
  Vendor tools exist; the data source and the
  ritual matter more than the vendor.

The chapter's paired exercise —
[`exercise-05-dora-four-key-measurement-plan.md`](exercises/exercise-05-dora-four-key-measurement-plan.md)
— asks you to author a per-metric measurement plan
(data source, collection frequency, reporting cadence,
the-team-owns-the-number ritual), with an explicit
anti-goal-ification section.

Chapter 06 walks the platform-investment sizing at each
stage — the test infra, deploy infra, observability,
and developer-platform decisions that keep the DORA
numbers from cliffing at 15 and 50 engineers.
