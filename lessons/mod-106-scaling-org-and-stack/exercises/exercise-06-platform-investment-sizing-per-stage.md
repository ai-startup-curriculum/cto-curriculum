# Exercise 06 — Platform Investment Sizing per Stage

**Module:** `mod-106-scaling-org-and-stack`
**Planned time:** ~3 hours
**Chapter this builds on:** [`06-platform-investment-sizing.md`](../06-platform-investment-sizing.md),
supported by [`mod-103`](../../mod-103-build-vs-buy-and-platform-economics/README.md)
on the earn-its-keep test that every platform
investment runs, [`mod-105`](../../mod-105-technical-debt-as-business-decision/README.md)
on the cost-to-carry frame the platform-investment
sizing uses, and [`05-dora-four-keys-as-signal.md`](../05-dora-four-keys-as-signal.md)
on the numbers the platform investment moves.

## Problem statement

Author a **per-stage platform-investment sizing
matrix** as a `docs/scaling/platform/` sub-tree in
the working repo. The matrix sizes the four platform
categories from chapter 06 — **test infrastructure,
deploy infrastructure, observability, developer
platform** — at each of the four stages (0-5, 5-15,
15-50, 50-150), with a per-stage rationale, the
earn-its-keep test result, and the explicit
deferral list to
[`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
(level 45) and
[`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
(level 55) for the deep architectural depth that
belongs beyond the CTO's scope.

The exercise's discipline is *anticipating* the tax
the next stage will impose — CI wall-clock at 15,
observability opacity at 50, developer-platform ramp
cost at 100 — and sizing enough of the investment
pre-cliff that the DORA numbers do not regress. The
matrix is the artifact that names the sizing calls
concretely enough that the CTO cannot avoid the
decision by deferring it.

## Requirements

Directory shape:

```
docs/scaling/platform/
  README.md                        # index and framing (this file's twin)
  matrix.md                        # the 4x4 sizing matrix
  test-infrastructure.md           # per-category deep-dive (artifact 2)
  deploy-infrastructure.md         # per-category deep-dive (artifact 3)
  observability.md                 # per-category deep-dive (artifact 4)
  developer-platform.md            # per-category deep-dive (artifact 5)
  earn-its-keep-results/
    README.md                      # convention
    <one file per current-stage platform-team candidate>
  deferral-list.md                 # what belongs to the senior architect
```

### `docs/scaling/platform/README.md`

One page. Sections:

- **Purpose.** One paragraph on why the org sizes
  platform investment per stage, framed against the
  cliff-avoidance discipline from chapter 06.
- **The four categories**, one sentence each, linking
  to the per-category deep-dive files.
- **The four stages** (0-5, 5-15, 15-50, 50-150),
  linking to the matrix.
- **The earn-its-keep test.** One paragraph, pointing
  at [`mod-103`](../../mod-103-build-vs-buy-and-platform-economics/README.md)
  and at the `earn-its-keep-results/` directory.
- **The deferral list.** One paragraph, pointing at
  `deferral-list.md` and at the higher-altitude
  tracks (`ai-infra-senior-architect`,
  `ai-infra-principal-architect`).

### Artifact 1 — The 4x4 sizing matrix

`matrix.md` — one to two pages. A table or a
per-category-per-stage list that names, at each
intersection of {test infrastructure, deploy
infrastructure, observability, developer platform}
and {0-5, 5-15, 15-50, 50-150}:

- **Investment shape.** No dedicated hire /
  ~10% of one engineer / 2-4 engineer platform team
  / multi-team platform investment. Concrete.
- **Named tooling / vendor at this stage.** GitHub
  Actions public runners at 0-5; Grafana + Prometheus
  + OpenTelemetry at 15-50; Backstage at 50-150;
  etc. Cite the primary source per row (see the
  chapter-06 links).
- **Expected DORA impact.** Which of the four keys
  this investment protects (Lead Time for the CI
  investment, Deployment Frequency for the
  progressive-rollout investment, MTTR for the
  observability investment, etc).
- **Cost line at this stage.** Rough
  engineer-weeks per year plus SaaS spend
  ($/month or $/year). Concrete ranges, not
  placeholder ranges — see the starter guidance
  below on comp-band-derived costing.

The matrix at minimum has 16 populated cells. Each
row references the per-category deep-dive; each
column references the stage's chapter (chapter 01
for 0-5, chapter 02 for 5-15, chapter 03 for 15-50,
chapter 04 for 50-150).

### Artifacts 2-5 — Per-category deep-dive files

One file per category, one to two pages. Same
shape across all four:

- **Definition.** One paragraph on what this
  category covers (chapter 06's four-category
  list).
- **Why this category matters at each stage.** 4
  short paragraphs, one per stage, on the
  specific pain the category resolves and the
  specific cliff it prevents.
- **The staged investment.** For each of the four
  stages: what is bought / built / hired, what is
  deferred, and what triggers the transition to
  the next stage's investment level.
- **The named vendors / open-source projects.**
  A short list, with primary-source links, of
  the concrete tools at each stage. From
  chapter 06:
  - **test-infrastructure.md** — GitHub Actions
    ([docs.github.com/actions](https://docs.github.com/en/actions)),
    GitLab CI, CircleCI, Buildkite,
    plus the discipline references *Continuous
    Delivery*
    ([continuousdelivery.com](https://continuousdelivery.com/))
    and *Release It!*
    ([pragprog.com/titles/mnee2/release-it-second-edition](https://pragprog.com/titles/mnee2/release-it-second-edition/)).
  - **deploy-infrastructure.md** — feature-flag
    vendors (LaunchDarkly
    [launchdarkly.com](https://launchdarkly.com/),
    Unleash [getunleash.io](https://www.getunleash.io/),
    Flagsmith [flagsmith.com](https://flagsmith.com/),
    PostHog [posthog.com](https://posthog.com/)),
    progressive-rollout tooling (Argo Rollouts
    [argoproj.github.io/argo-rollouts](https://argoproj.github.io/argo-rollouts/),
    Flagger [flagger.app](https://flagger.app/)),
    GitOps tooling (Argo CD
    [argo-cd.readthedocs.io](https://argo-cd.readthedocs.io/en/stable/),
    Flux [fluxcd.io](https://fluxcd.io/), Spinnaker
    [spinnaker.io](https://spinnaker.io/)).
  - **observability.md** — OpenTelemetry
    ([opentelemetry.io](https://opentelemetry.io/)),
    Prometheus, Grafana (Loki / Mimir / Tempo),
    Honeycomb ([honeycomb.io](https://www.honeycomb.io/)),
    Datadog, Sentry, plus the SRE-book chapters
    on alerting
    ([sre.google/sre-book/practical-alerting](https://sre.google/sre-book/practical-alerting/))
    and SLOs
    ([sre.google/sre-book/service-level-objectives](https://sre.google/sre-book/service-level-objectives/)).
  - **developer-platform.md** — Backstage
    ([backstage.io](https://backstage.io/)),
    OpsLevel, Cortex, Port, plus
    [platformengineering.org](https://platformengineering.org/)
    for the vocabulary and Team Topologies
    ([teamtopologies.com](https://teamtopologies.com/))
    on the platform-team interaction mode.
- **The at-this-stage anti-pattern.** 2-3 bullets
  on the specific way this category most-often
  gets over- or under-invested. From chapter 06:
  the imported big-tech platform stack at 15-50;
  the platform team without an earn-its-keep test;
  the multi-region deploy the CTO tries to
  personally design at 50-150.
- **References.** The primary sources cited above.

### Artifact 6 — Earn-its-keep test results

`earn-its-keep-results/README.md` — a short
convention document:

- File naming — `<category>-<stage>-<slug>.md`
  (e.g., `observability-15-to-50-shared-tracing.md`).
- Each result file follows the five-question
  framework from chapter 03 artifact 2 and
  [`mod-103`](../../mod-103-build-vs-buy-and-platform-economics/README.md):
  named internal customer(s), sized cost-to-carry
  (in engineer-hours per week — reference the
  sizing methodology from
  [`mod-105` chapter 03](../../mod-105-technical-debt-as-business-decision/03-cost-to-carry-and-depreciation-schedule.md)),
  explicit vs.-buy alternative with vendor
  named, product-team-first alternative, time-
  boxed pilot with cancel criteria, and a
  decision (charter / defer / buy).
- **Author at least one earn-its-keep result** for
  the platform-team candidate at the *current
  stage* of your working-repo scenario. If your
  scenario is at 15-50, that is the first platform-
  team charter (usually build / CI-and-deploy per
  chapter 06's first-in-order list); at 5-15 the
  result is usually *"defer, size the investment
  as ~10% of one engineer's time on a rotation"*;
  at 0-5 the result is usually *"defer, no
  investment"*.

The `earn-its-keep-results/` directory can start
with a single result file plus the README; the
directory grows over time as more platform
candidates get tested.

### Artifact 7 — Deferral list

`deferral-list.md` — one page. What the CTO
explicitly defers to the higher-altitude tracks.
Sections:

- **Defers to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45).** 3-6 bullets. From chapter 06's
  list: multi-region / data-residency architecture;
  multi-tenancy isolation model at scale (silo /
  pool / bridge — see the AWS SaaS Lens at
  [docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html](https://docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html));
  distributed-consensus / storage-layer choices
  for a scale-critical subsystem; the bespoke
  platform layer (custom scheduler / storage
  engine / networking layer) if the product
  actually needs one.
- **Defers to
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55).** 3-4 bullets. From chapter 06's
  list: cross-region / multi-cloud strategy at
  scale; compliance-critical architecture
  decisions (FedRAMP, HIPAA-at-scale, SOC 2
  Type II — with
  [`mod-107`](../../mod-107-founder-scope-security-and-compliance/README.md)
  as the CTO-scope adjacent module); multi-year
  platform-team roadmap that spans multiple
  platform teams.
- **The CTO's role in those decisions.** One
  paragraph. Approving the architect's proposal;
  understanding it well enough to defend it to
  the board; ensuring it fits company strategy;
  *not* authoring it. Cite chapter 04's CTO-role
  delta.
- **The trigger for hiring the architect.** Named.
  Usually one or more of: multi-region requirement
  landed as a customer / compliance ask; the
  team is at 50+ engineers and the deep-technical
  gap is bottlenecking the roadmap; a specific
  scale-critical subsystem is failing under
  load and the current team lacks the domain
  depth.

## Starter guidance

- **Fill the matrix at your current stage first,
  then the next stage.** The 0-5 and 5-15 cells
  are easy if your scenario is at 15-50 — they
  are the historical baseline. The 50-150 cells
  are the ones CTOs cheat on, either by importing
  a big-tech reference architecture wholesale or
  by writing *"TBD"*. Neither is acceptable — the
  matrix is the artifact that forces you to size
  the future stages *now*, based on the chapter's
  heuristics rather than a reference org's
  choices.
- **The comp-band-derived cost line is where the
  sizing gets real.** *"~10% of one engineer"* at
  the mid-band from
  [`mod-104` chapter 06](../../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md)
  is a concrete number (engineer-weeks per year
  and dollar cost per year), not an abstract
  fraction. Compute it. A platform investment
  that costs *"about a quarter of an engineer"*
  is invisible; a platform investment that costs
  *"$60k of engineering time per year, plus $18k
  of SaaS spend, against a $2.4M engineering
  budget"* can be defended (or refused) on
  concrete grounds.
- **Do not import big-tech reference stacks
  wholesale.** Chapter 06's 15-50 anti-pattern is
  the CTO who reads an Uber / Airbnb / Netflix
  platform-engineering post and imports the full
  stack. Read the posts as directional
  references. Cite the reference. Then size your
  own stack against your team's actual load, not
  the reference org's. If you cannot articulate
  what your team's Kubernetes / Backstage
  investment specifically *pays for*, defer it.
- **The earn-its-keep test is the discipline that
  keeps the platform team from existing as an
  aesthetic choice.** Chapter 06's failure mode
  ("*it is important that we have a platform
  team*") is the one to guard against. If your
  earn-its-keep result on the current-stage
  platform-team candidate is *"the tests do not
  pass yet"*, that is a valid answer — write down
  the negative result and defer. If every
  earn-its-keep result authored in every
  exercise instance ended in *"yes, charter it"*,
  the discipline is not real.
- **The deferral list is a CTO-role artifact,
  not a hedge.** *"We do not do multi-region
  yet"* is not a deferral; *"multi-region
  architecture, if / when required by a customer
  or compliance ask, is delegated to a hired
  senior architect and not authored by the CTO"*
  is. The deferral list is where the CTO writes
  down what they will *not* try to personally
  own, which is the honest counterpart to the
  CTO-role delta memo from
  [exercise 04](exercise-04-fifty-to-onefifty-first-vp-eng-transition.md).
- **Read the four per-category deep-dives
  against the matrix.** The matrix is the summary;
  the deep-dives are the reasoning. If a matrix
  cell says *"2-4 engineer platform team"* but
  the deep-dive does not name what that team
  actually builds and what earn-its-keep test it
  passed, the matrix is a placeholder rather
  than a plan. Revise until the two agree.
- **The DORA impact per row is a check on the
  investment thesis.** Each platform investment
  should protect a specific one (or two) of the
  four DORA keys. If a row cannot name the
  DORA number it protects, the investment thesis
  is under-cooked. Reference the DORA
  measurement plan from
  [exercise 05](exercise-05-dora-four-key-measurement-plan.md).
- **Cite each matrix cell's tooling by product
  page, not by vendor name alone.** The matrix
  row's named-tooling column should carry the
  primary-source URL so the sizing can be
  reproduced by the next reader. Chapter 06 names
  each vendor's URL — carry it forward into the
  matrix row rather than re-flattening the name.
  For the CI transition out of public runners,
  the GitHub Actions
  [larger-runner docs](https://docs.github.com/en/actions/using-github-hosted-runners/about-larger-runners)
  and the [Actions pricing page](https://github.com/features/actions)
  are the specific sub-pages the 5-15 → 15-50
  pricing call depends on; for the 50-150
  developer-platform row, cite
  [backstage.io/docs](https://backstage.io/docs/)
  rather than the product homepage — the docs
  are what will hold the sizing to reality.
- **The DORA bands are a calibration reference,
  not a per-cell sizing target.** The
  "the DORA numbers do not regress" discipline
  in the problem statement uses the
  [dora.dev/research](https://dora.dev/research/)
  elite / high / medium / low cutoffs as a
  situating tool at the annual re-read, not as a
  numeric target in any matrix cell. Do not
  write *"get Lead Time to elite"* into a cell
  — name the practice the investment protects
  (fast CI, progressive rollout, SLO
  instrumentation, service catalogue) and let
  the number follow. [Exercise 05 artifact 5](exercise-05-dora-four-key-measurement-plan.md)
  is the local defence against the goal-
  ification slip.
- **The comp-band-derived cost line is a
  [`mod-104` chapter 06](../../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md)
  output, not a new number.** The *"$60k of
  engineering time per year"* worked example
  above assumes a specific seed / Series-A
  engineer cost at a 1.3-1.5x fully-loaded
  multiplier; the sources are
  [Levels.fyi](https://www.levels.fyi/),
  [Pave](https://www.pave.com/), and the
  [Index Ventures Option Plan](https://www.indexventures.com/optionplan/),
  with the multiplier being a CFO number per
  [`mod-104` exercise 01's starter guidance](../../mod-104-first-engineering-hires-and-team-topology/exercises/exercise-01-hiring-plan-against-roadmap-and-runway.md).
  Cite the Levels.fyi row (or the Pave / Radford
  row, if your People lead has access) you
  derived the engineer-cost against — a $60k
  line item without a sourced row is an invented
  number.
  <!-- needs-research: a sourced primary
  reference for the chapter-06 per-stage
  platform-investment sizing fractions
  ("~10% of one engineer" at 5-15; "2-4 engineer
  platform team" at 15-50; "multi-team platform
  investment" at 50-150). These are rule-of-
  thumb sizings; the closest canonical readings
  are Team Topologies
  ([teamtopologies.com](https://teamtopologies.com/))
  on platform-team scope and the
  platformengineering.org community guidance,
  neither of which pin a specific headcount at
  these stage bands. -->
- **Big-tech reference stacks are directional
  blog posts, not reference architectures.**
  When chapter 06's 15-50 anti-pattern (the
  imported Uber / Airbnb / Netflix platform
  stack) is invoked in the matrix or in a
  per-category deep-dive, link the specific
  post as a *directional* reference rather than
  as a target. Entry points to the primary
  publications, not aggregator recaps:
  [Uber Engineering blog](https://www.uber.com/en-US/blog/engineering/),
  [Airbnb Tech Blog](https://medium.com/airbnb-engineering),
  [Netflix Tech Blog](https://netflixtechblog.com/).
  The citation makes clear to the next reader
  that the sizing was informed by a specific-
  scale org's writeup, not adopted wholesale as
  a validated architecture; the earn-its-keep
  test is what converts that signal into a
  local sizing call.

## Acceptance criteria

Your drill output is complete when:

- The `docs/scaling/platform/` directory contains
  the seven artifacts in the shape above.
- The matrix has all 16 cells (4 categories × 4
  stages) populated with investment shape, named
  tooling, DORA impact, and cost line (engineer-
  weeks per year plus SaaS spend range).
- Each per-category deep-dive names the stage-by-
  stage investment, at least one primary-source
  citation per stage, and the at-this-stage
  anti-pattern.
- At least one earn-its-keep result exists for
  the platform-team candidate at your working-
  repo scenario's *current* stage, with all five
  test elements and a decision.
- The deferral list names 3-6
  senior-architect deferrals, 3-4 principal-
  architect deferrals, the CTO's role in those
  decisions, and the trigger for hiring the
  architect.
- Cost lines in the matrix use comp-band-derived
  numbers (in dollars), not abstract fractions
  of engineers.
- The matrix and the per-category deep-dives
  agree; a reader can start with the matrix and
  drill into the deep-dive without a
  contradiction.
- The seven artifacts together can be handed to
  the CFO for the platform-investment slice of
  the annual budget, plus to the VP Eng /
  platform lead for the operational execution,
  without a follow-up round of clarifications.

## What this feeds into

- **Exercise 07** — the delivery-cadence and
  on-call design assumes the platform investments
  named here (progressive rollout for deploy,
  SLI / SLO for observability, runbook-per-
  service for developer platform).
- **The 15-to-50 platform-team charter** — the
  earn-its-keep result from artifact 6 is the
  substrate for the platform-team charter in
  [exercise 03](exercise-03-fifteen-to-fifty-first-em-and-platform-team.md);
  the two exercises should agree if both are
  authored.
- **The lab** — the platform-investment matrix is
  a cross-cutting section of the `docs/scaling/`
  runbook. Every stage-transition slice
  references its column.
- **`mod-108`** — the annual budget cycle
  ([`mod-108`](../../mod-108-cto-ceo-and-board-communication/README.md)
  for the CFO conversation shape) uses the
  cost-line column of the matrix as a
  defensible input.

The platform-investment sizing is the exercise
where the CTO writes down what the org will build,
what it will buy, what it will defer, and what it
will delegate up-track. If the matrix reads like a
big-tech reference stack borrowed from a blog
post, the discipline has drifted; go back to the
earn-its-keep results and re-check whether each
row is genuinely earning its keep at your
current stage. The matrix's success is measured
by whether the DORA numbers hold across the next
transition, not by whether the stack looks
sophisticated.
