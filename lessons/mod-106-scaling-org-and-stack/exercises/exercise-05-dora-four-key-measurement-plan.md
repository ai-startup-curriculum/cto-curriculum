# Exercise 05 — DORA Four-Key Measurement Plan

**Module:** `mod-106-scaling-org-and-stack`
**Planned time:** ~2 hours
**Chapter this builds on:** [`05-dora-four-keys-as-signal.md`](../05-dora-four-keys-as-signal.md),
supported by the delivery-cadence work in
[`02-five-to-fifteen-first-structure.md`](../02-five-to-fifteen-first-structure.md)
and [`07-delivery-cadence-and-on-call.md`](../07-delivery-cadence-and-on-call.md)
that turns the numbers into a ritual, plus
[`mod-105`](../../mod-105-technical-debt-as-business-decision/README.md)
on the debt portfolio the numbers feed back into.

## Problem statement

Author a **DORA four-key measurement plan** as a
`docs/dora/` sub-tree in the working repo. The plan
names, for each of the four metrics, the concrete
data source, the collection frequency, the reporting
cadence, and the *team-owns-the-number* ritual — plus
an explicit **anti-goal-ification section** that
names how you will keep the numbers from becoming
targets.

The exercise's discipline is not the *choice* of
metrics — the DORA four are the choice, cited in the
chapter — nor a novel measurement approach. The
discipline is authoring the plan in enough concrete
detail that it can be handed to the team and executed
next Monday, and that the anti-goal-ification section
is honest about the specific pressure that would push
these numbers toward becoming an OKR (the CFO who
wants a KPI, the board that wants a scoreboard, the
new engineering hire from a metrics-first culture).

## Requirements

Directory shape:

```
docs/dora/
  README.md                 # overview and links (this file's twin)
  deployment-frequency.md   # per-metric plan (artifact 1)
  lead-time-for-changes.md  # per-metric plan (artifact 2)
  change-failure-rate.md    # per-metric plan (artifact 3)
  mean-time-to-restore.md   # per-metric plan (artifact 4)
  anti-goal-ification.md    # artifact 5
  ritual.md                 # artifact 6 — the per-stage ritual
```

### `docs/dora/README.md`

One page. Sections:

- **Purpose.** One paragraph on why the org
  measures the four. Cite
  [dora.dev](https://dora.dev/), the annual *State
  of DevOps Report* at
  [dora.dev/research](https://dora.dev/research/),
  and Forsgren / Humble / Kim's *Accelerate*
  ([itrevolution.com/product/accelerate](https://itrevolution.com/product/accelerate/)).
- **The four keys**, one sentence each, linking to
  the per-metric file. Grouped into speed
  (Deployment Frequency, Lead Time for Changes)
  and stability (Change Failure Rate, MTTR).
- **A signal, not a goal.** One paragraph pointing
  at `anti-goal-ification.md` and quoting
  Strathern
  ([oro.open.ac.uk/22183](https://oro.open.ac.uk/22183/))
  on the metric-becomes-target failure mode.
- **Where the numbers live.** The dashboard URL
  (or the placeholder for it), the vendor / tool
  (Grafana, LinearB, Sleuth, Jellyfish, or the
  Google Cloud
  `four-keys` reference implementation at
  [github.com/GoogleCloudPlatform/fourkeys](https://github.com/GoogleCloudPlatform/fourkeys)),
  and the owner of the dashboard.
- **Where the numbers are read.** Pointer to
  `ritual.md`.

### Per-metric plan (artifacts 1-4)

Each of the four `*.md` files has the same shape,
one page:

- **Definition.** The DORA definition, exact,
  citing
  [dora.dev/research](https://dora.dev/research/).
  Do not paraphrase; quote.
- **Data source.** The concrete system(s) the
  number comes from. Concrete: not *"the CI
  system"* but *"GitHub Actions workflow runs
  labelled `deploy-production` on the `main`
  branch of `services/api`"*. Where the data lives
  (a query against the deploy log, an incident
  tracker export, a labelled git-commit stream)
  and how you extract it.
- **Collection frequency.** Continuously (event-
  driven from a webhook), hourly (a scheduled
  aggregation job), daily (a nightly ETL), weekly.
  Name the choice and defend it — the collection
  frequency has to be finer than the reporting
  frequency to be useful.
- **Reporting cadence.** Where the number shows
  up and how often. The team dashboard (real-
  time); the weekly cadence-metrics reading in
  planning (chapter 05 ritual for 5-15 and
  15-50); the monthly aggregate reviewed by the
  CTO / VP (15-50 and above); the quarterly
  board pre-read
  ([`mod-108`](../../mod-108-cto-ceo-and-board-communication/README.md)
  for the shape).
- **Team-owns-the-number ritual.** *Who* looks at
  the number, *when*, and *what conversation* the
  number is expected to start. Concrete: *"the
  weekly Monday planning; the EM (or tech lead
  at 5-15) walks through the four numbers in
  under 5 minutes; the team discusses only the
  numbers that changed materially since the
  prior week; changes get an action item or a
  note in the retro doc, not a mandate to
  improve"*.
- **Failure-mode watchlist for this metric.** 2-4
  bullets on how *this specific number* is most
  likely to get gamed or misread. For Deployment
  Frequency, the artificial-split-of-a-coherent-
  change failure mode from chapter 05. For MTTR,
  the close-the-incident-when-the-alert-quiets
  failure mode. Etc.
- **Related metrics the number should be read
  against.** For Deployment Frequency, always
  read with Change Failure Rate (the speed /
  stability pair). For MTTR, read with Change
  Failure Rate and the incident count. This
  section is the local defence against failure
  mode 2 (single-metric fixation).
- **Reference(s).** The DORA / *Accelerate*
  citation, plus the tool-specific documentation
  for whatever computes the number for your team.

Per-metric guidance for the data-source section:

- **`deployment-frequency.md`** — the CI/CD
  system's deploy log. Options: GitHub Actions
  ([docs.github.com/actions](https://docs.github.com/en/actions)),
  GitLab CI / CD
  ([docs.gitlab.com](https://docs.gitlab.com/ee/ci/)),
  CircleCI ([circleci.com](https://circleci.com/)),
  Argo CD
  ([argo-cd.readthedocs.io](https://argo-cd.readthedocs.io/en/stable/)),
  Spinnaker
  ([spinnaker.io](https://spinnaker.io/)). Count
  deploys per unit time to production.
- **`lead-time-for-changes.md`** — the correlation
  of git-history and the deploy log. Time from a
  commit's *first* push to that commit landing in
  production. The
  [github.com/GoogleCloudPlatform/fourkeys](https://github.com/GoogleCloudPlatform/fourkeys)
  reference implementation shows one shape for
  this join.
- **`change-failure-rate.md`** — a labelled
  incident stream. Common shapes: incident.io
  ([incident.io](https://incident.io/)),
  PagerDuty ([pagerduty.com](https://www.pagerduty.com/)),
  a Jira / Linear label, or a `hotfix:` /
  `rollback:` commit-message convention that CI
  can count. Name the exact label / convention.
- **`mean-time-to-restore.md`** — the incident
  tracker's open-to-closed duration, with the
  discipline of *not closing until resolved*.
  Reference the DORA program's more-recent
  *failed-deployment-recovery-time* wording if
  you want to distinguish from generic MTTR.

### Artifact 5 — Anti-goal-ification plan

`anti-goal-ification.md` — one page. This is the
plan that keeps the four numbers as a diagnostic
rather than a scoreboard. Sections:

- **The three failure modes** — recap the chapter
  05 vocabulary in your own words:
  goal-ification (Goodhart /
  Strathern
  [oro.open.ac.uk/22183](https://oro.open.ac.uk/22183/)),
  single-metric fixation, cross-team benchmarking.
- **The rules the team commits to.** 4-6
  concrete rules. Suggested set:
  - **No DORA number as an OKR or performance-
    review target.** Named.
  - **The four numbers are read as a set, always
    together.** No single-metric conversation.
  - **DORA numbers are within-team trends,
    never a leaderboard.** No cross-team ranking.
  - **The elite / high / medium / low bands are
    a situating tool, not a target.** Consult
    the current [dora.dev/research](https://dora.dev/research/)
    for the current-year cutoffs, and use them
    only for the annual *"are we in the same
    zip code as our peer set"* check.
  - **A number that moves gets a discussion,
    not an intervention.** The discussion asks
    *"what changed and why"* before any
    action.
- **The specific pressure this plan will face.**
  2-3 bullets naming the pressure sources you
  actually expect. Suggested: the CFO who wants
  a KPI to put in the board pre-read; the board
  member who benchmarks against another portfolio
  company; the new engineering hire from a
  metrics-first culture who wants to *"drive
  Deployment Frequency to elite"*. For each,
  the response — usually a re-articulation of
  the *signal-not-goal* framing plus a pointer
  to the annual DORA report's own guidance.
- **The escalation.** If a stakeholder demands
  DORA-as-target and will not accept the
  *signal-not-goal* framing, what does the CTO
  do? Options: the board narrative in
  [`mod-108`](../../mod-108-cto-ceo-and-board-communication/README.md);
  a paired presentation of DORA plus the SPACE
  ([queue.acm.org/detail.cfm?id=3454124](https://queue.acm.org/detail.cfm?id=3454124))
  and DevEx
  ([queue.acm.org/detail.cfm?id=3595878](https://queue.acm.org/detail.cfm?id=3595878))
  frames to shift the conversation.

### Artifact 6 — The per-stage ritual

`ritual.md` — one page. The chapter 05 per-stage
ritual, written as a runbook for *your* team's
current and next stage:

- **Current stage** (0-5, 5-15, 15-50, or
  50-150). Named.
- **Current ritual.** Concrete: who reads the
  numbers, when, with what audience, and what
  conversation follows. From chapter 05's per-
  stage table — the 0-5 spreadsheet, the 5-15
  cadence-meeting dashboard, the 15-50 team-
  owned numbers with monthly aggregate, or the
  50-150 per-team dashboard plus quarterly board
  pre-read.
- **Next-stage ritual.** What changes at the
  next transition. Concrete deltas: new
  audience, new cadence, new tooling
  requirement.
- **The trigger that moves the ritual to the
  next stage.** Named. Usually the team-size
  threshold plus a specific signal (the
  aggregate number is no longer meaningful
  because the teams have diverged; the
  weekly-cadence reading is now too big for
  one meeting).

## Starter guidance

- **Start from the concrete data source, not
  the definition.** The definition is the easy
  part; the load-bearing exercise is naming
  *exactly* which query against which system
  produces the number. If you cannot name the
  query today, the number is not yet measurable,
  and the plan should say so honestly (with a
  named prerequisite).
- **The `four-keys` reference implementation is
  the load-bearing read for the computation
  logic.** Read
  [github.com/GoogleCloudPlatform/fourkeys](https://github.com/GoogleCloudPlatform/fourkeys)
  even if you use a vendor tool. The source
  shows exactly what data the four keys
  actually need, which will save you a
  vendor-evaluation round.
- **The team-owns-the-number ritual is the
  hardest section to write.** *"The team reads
  the numbers weekly"* is a placeholder, not a
  ritual. *"Every Monday at 10am, the EM opens
  the four-key dashboard on the shared screen
  during the 30-minute planning meeting; the
  EM walks the four numbers in 5 minutes; the
  team discusses any number that changed by
  more than one bucket since the last reading;
  the discussion is captured in the retro
  doc"* is a ritual. Aim for the second
  shape.
- **The anti-goal-ification section is the
  section CTOs skip.** Do not skip it. The
  pressure to turn DORA into a KPI is real —
  from the CFO, the board, the new hire from
  a metrics-first culture — and the response
  needs to exist in writing before the
  pressure arrives. Read the annual DORA
  report's own guidance on this framing before
  authoring; the DORA program's own posture is
  *signal, not goal*.
- **Do not pick numeric targets, even
  informally.** *"We aspire to daily deploys"*
  is a target dressed as an aspiration; the
  chapter 05 posture is that the number is a
  diagnostic. If daily deploys are the right
  practice, the practice is what you commit
  to (feature flags, trunk-based development,
  short PRs); the deploy frequency will follow.
  If you write down a target, you have
  already fallen into failure mode 1.
- **Read all six files together at the end.**
  The four per-metric plans should reference
  the ritual doc; the ritual doc should
  reference the four per-metric plans; the
  anti-goal-ification doc should reference the
  ritual; the README should link to all five.
  If the six do not cross-reference, they are
  six documents rather than one plan.

## Acceptance criteria

Your drill output is complete when:

- The `docs/dora/` directory contains the six
  files in the shape above.
- Each per-metric file names an exact data
  source (specific system, specific query /
  label / convention), a collection frequency,
  a reporting cadence, and a team-owns-the-
  number ritual with concrete language (see
  the starter-guidance example).
- Each per-metric file names 2-4 failure modes
  specific to *that* metric and 1-2 related
  metrics the number is read against.
- The anti-goal-ification file names all three
  failure modes from chapter 05, 4-6 concrete
  rules the team commits to, and 2-3 specific
  pressure sources with the response.
- The ritual file names the current stage,
  the current ritual with concrete audience /
  cadence / conversation shape, the next-
  stage ritual, and the transition trigger.
- No DORA number appears as a target, an OKR,
  or an aspirational band anywhere in the plan.
  If a reader could infer *"the team is aiming
  for elite"* from the plan, revise.
- The plan can be handed to the EM or tech
  lead and executed next Monday without a
  follow-up round of clarifications.

## What this feeds into

- **Exercise 06** — the platform-investment
  sizing per stage is calibrated against the
  DORA numbers this plan measures. A rising
  CI wall-clock manifests as a rising Lead
  Time; the platform investment is the
  response.
- **Exercise 07** — the delivery-cadence spec
  is the ritual container for the DORA
  reading. The weekly cadence-metrics reading
  is the artifact that turns this measurement
  plan into a conversation.
- **`mod-105`** — the tech-debt portfolio
  ([mod-105 chapter 06](../../mod-105-technical-debt-as-business-decision/06-debt-inventory-and-portfolio-decision-log.md))
  is where a chronically-elevated Change
  Failure Rate or MTTR gets its named debt
  items; the refactor budget
  ([mod-105 chapter 04](../../mod-105-technical-debt-as-business-decision/04-refactor-budget-tied-to-roadmap.md))
  funds the remediation.
- **`mod-108`** — the board pre-read at
  50-150 (see chapter 05's per-stage ritual)
  includes the DORA aggregate with narrative
  context. The measurement plan is the
  substrate the pre-read is built on.
- **The lab** — the DORA measurement plan is
  a cross-cutting section of the
  `docs/scaling/` runbook, cited by each of
  the four stage-transition slices.

The DORA measurement plan is the exercise where
the CTO writes down how the org will *know* how
its delivery is doing. If the plan reads like a
scoreboard, the discipline has drifted; go back
to the anti-goal-ification section and re-work.
The plan's success is measured by whether the
team trusts the numbers enough to reason with
them, not by whether the numbers are elite.
