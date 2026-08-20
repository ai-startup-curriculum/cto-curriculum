# The 0→5 Transition — First Repo, First CI, First Tests

> "Everything you do in your first year is easier to
> change than you think — except the things that aren't."
> The four things that aren't, at the 0→5 stage, are the
> **repo layout**, the **branching model**, the **CI
> pipeline**, and the **dev-environment convention**.
> Each of them sets a default the team will still be
> paying for at 15 engineers.

## Motivation

Zero to five engineers is the phase in which the CTO is
still writing production code every day and the "process"
is *"whoever is closest to the problem fixes it"*. There
is no dedicated build engineer, no on-call rotation, no
sprint. Everything works because the room is small enough
that the missing structure is invisible.

Two failure modes dominate this stage:

- **No process at all.** The founder-CTO leans on the
  small-team invisibility of the missing structure. There
  is no repo convention (the second engineer starts a new
  repo because the first repo is *"a mess"*), no shared
  dev-environment script (each new hire spends a week
  getting the app to run), no CI pipeline (tests exist
  but only run on the CTO's laptop). At engineer #6 the
  team hits a velocity cliff because every one of these
  gaps starts costing real hours per week, and the debt
  compounds before anyone recognises the pattern.
- **Premature process.** The founder-CTO copies the
  process from their last job — the one that had a
  hundred engineers, a release-train, a two-week sprint,
  a QA team, and a full-time SRE oncall. The team of
  three tries to enact a governance layer meant for a
  hundred; the process consumes a full engineer's worth
  of time; no product ships; a co-founder pushes back
  and the process is thrown out entirely, over-correcting
  the other way.

The zero-to-five job is neither. It is the *minimum*
process that makes the team's next transitions cheap —
and specifically the four decisions in this chapter's
title, because those are the ones the team cannot
easily change once they are in place.

## The four decisions that set unrecoverable defaults

Most 0-5 decisions are easily reversible. You can rename
a service, swap a linter, change a code-review reviewer.
The four decisions below are different — they are the
ones that shape everything the team does with the
codebase from that point forward, and each of them has a
well-known "we tried to change it at 20 engineers, it
took a quarter and broke morale" reversal story.

The four decisions:

1. **Repo layout** — monorepo vs. multi-repo (vs. the
   hybrid of a few grouped repos).
2. **Branching model** — trunk-based vs. GitFlow vs.
   release-train.
3. **CI pipeline** — what runs on every push, and how
   fast it has to be.
4. **Dev-environment convention** — how a new hire (or a
   returning engineer on a new laptop) gets the app
   running.

Each of these is treated below. The chapter closes with
DORA-as-baseline from day one and the failure-mode
diagnostic.

## Decision 1 — Repo layout

The repo layout question at 0-5 engineers is *not* the
Google-scale monorepo question. It is the much smaller
question: **when engineer #4 starts a new service, does
it go in the same repo or a new one?**

Three shapes to know:

- **Single monorepo** — one repo, all services, all
  frontends, all shared libraries. The Software
  Engineering at Google chapter on version control and
  branch management
  ([abseil.io/resources/swe-book](https://abseil.io/resources/swe-book))
  is the canonical treatment of the shape at scale. At
  0-5 engineers the appeal is: one clone, one CI config,
  one code search, atomic cross-service refactors.
- **Multi-repo** — one repo per service. Appeal: strong
  independence, easy to open-source a component, clean
  per-repo access control, familiar to engineers with a
  microservices background.
- **A few grouped repos** — one repo per rough
  bounded-context (product, platform, infrastructure).
  Halfway house that many startups converge on.

The 0-5 default: **start with a monorepo**. Reasons —
the team is too small to run the multi-repo tax (each
new repo needs its own CI config, its own dependency
management, its own release wire); cross-service refactors
are frequent at this stage as the domain is still being
learned (see
[`mod-102` chapter 01](../mod-102-architecture-under-uncertainty/README.md)
on the monolith-first / evolutionary-architecture posture);
and the "atomic commit across two services" property is
worth more than the theoretical independence.

The single well-known counter-argument: a team that
knows it will need language-heterogeneity from day one
(a Python data-science slice alongside a TypeScript
application) sometimes finds the monorepo tooling
awkward. Even here the default is usually still a
monorepo — the tooling gap is smaller than the multi-
repo tax at 5 engineers — but it is worth being explicit
about the trade-off in the decision record. See
[`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/README.md)
on the ADR discipline.

The reversal cost is real: converting a multi-repo estate
into a monorepo at 20 engineers is a quarter of one
engineer's time; converting a monorepo into multi-repo is
usually smaller but still weeks. Neither is a decision
you want to make twice.

## Decision 2 — Branching model

Three models to know, and one honest default:

- **Trunk-based development** — everyone commits to
  `main` (or short-lived feature branches merged within
  a day). Canonical reference:
  [trunkbaseddevelopment.com](https://trunkbaseddevelopment.com/)
  (Paul Hammant). This is the model the DORA program's
  *Accelerate*
  ([itrevolution.com/product/accelerate](https://itrevolution.com/product/accelerate/))
  finds correlates with high-performing engineering
  organisations across the four keys.
- **GitFlow** — long-lived `develop` and `main`
  branches, `release/*`, `hotfix/*`, `feature/*`.
  Original 2010 post by Vincent Driessen at
  [nvie.com/posts/a-successful-git-branching-model](https://nvie.com/posts/a-successful-git-branching-model/).
  The post itself carries a 2020 note from the author
  explicitly discouraging its use for continuously-
  deployed web applications and recommending trunk-based
  instead.
- **Release-train** — trunk-based development with a
  scheduled "train" cut every N days that becomes the
  production release. Used at larger orgs where the
  deploy has a heavier release process attached (mobile
  apps, on-premise software, regulated releases).

The 0-5 default: **trunk-based, deploy from `main`**.
Reasons — the team is small enough that a merge conflict
is a five-minute conversation, not a rebasing marathon;
`main` is stable if CI is fast enough; the model
generalises directly to the CI/CD posture DORA measures.
GitFlow's staging complexity is dead weight at this
scale, and the model's author has publicly recommended
against it for the SaaS shape most startups have.

Explicit call-out: trunk-based development *is* a
discipline. It requires that CI on `main` is green and
fast enough that a broken build is a "stop the line"
event. If the CTO cannot commit to that (see decision
3), trunk-based will drift into "everyone pushes to
`main` and it's broken half the time", which is worse
than any of the three models. Chapter 05 on DORA gives
the measurement the discipline is defended against.

Release-train shape becomes relevant if the deploy is
non-continuous — a mobile app, an embedded firmware, a
regulated deploy. Even there, trunk-based is the
underlying model; the train is just the cut-and-release
cadence layered on top.

## Decision 3 — CI pipeline

At 0-5 engineers the CI pipeline is the *smallest thing
that will grow with the team without a rewrite*. The
critical properties:

- **Runs on every push** — not on a nightly cron, not
  "on merge to `main`". Every push. Otherwise you cannot
  do trunk-based development safely.
- **Fast enough** — the *Accelerate* / DORA finding is
  that lead-time-for-changes is a top-quartile predictor
  of organisational performance. Concretely, if the CI
  loop is longer than ~10 minutes at 0-5 engineers, you
  are already burning the team's velocity. Aim for
  under 5 minutes at this stage.
- **Reproducible** — the CI environment must match the
  dev environment. If the tests pass locally and fail
  in CI, or vice versa, the pipeline is not doing its
  job.
- **Runs the tests that matter** — a linter is not
  tests; a build is not tests. See "First tests that
  actually run in CI" below.

Concretely, the 0-5 CI pipeline is usually one of
GitHub Actions
([docs.github.com/actions](https://docs.github.com/en/actions))
or GitLab CI
([docs.gitlab.com/ee/ci](https://docs.gitlab.com/ee/ci/))
or CircleCI. Which vendor is a minor decision — the
important discipline is:

- One workflow file at the repo root.
- Runs on every push and every pull request.
- Runs lint, build, unit tests, and any integration
  tests you have.
- Fails visibly in the pull-request UI (nobody
  merges a red build).
- Reports pipeline duration and success rate — this is
  the raw material for the DORA Lead Time and Change
  Failure Rate numbers chapter 05 covers.

A short worked example — GitHub Actions, single job,
matches the 0-5 shape:

```yaml
name: ci
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      - run: npm ci
      - run: npm run lint
      - run: npm run build
      - run: npm test -- --coverage
```

That workflow is under 20 lines, runs on every push,
takes ~2-5 minutes on a typical Node application, and
gives you the raw data for DORA. It will still be the
core of the CI pipeline at 15 engineers, at which
point matrix strategies, parallelism, and caching will
have grown around it.

## Decision 4 — Dev-environment convention

The dev-environment question at 0-5 engineers is *"can
a new engineer, on a laptop they were handed yesterday,
get the app running today?"* If the answer is *"only
after four days of stumbling through a Notion doc that
was last updated eight months ago"*, the convention is
missing.

Three shapes commonly used at this scale:

- **Container-based** — `docker compose up` runs the
  full stack. Canonical reference at
  [docs.docker.com/compose](https://docs.docker.com/compose/).
  Cheap, works on any platform Docker runs, matches
  production if production is containerised.
- **Nix / Devbox / mise / asdf** — declarative
  environment. Nix at
  [nixos.org](https://nixos.org/) and Devbox at
  [jetify.com/devbox](https://www.jetify.com/devbox);
  mise at [mise.jdx.dev](https://mise.jdx.dev/) and
  asdf at [asdf-vm.com](https://asdf-vm.com/).
  Higher up-front cost, but reproducible across machines
  and OS versions.
- **Cloud dev environments** — GitHub Codespaces
  ([github.com/features/codespaces](https://github.com/features/codespaces))
  or Gitpod
  ([gitpod.io](https://www.gitpod.io/)). Zero-setup
  from the engineer's perspective, at the cost of
  monthly per-seat spend and a network dependency.

The 0-5 default: **`docker compose` (or the equivalent
one-command bring-up) plus a Twelve-Factor-App-style
environment-variable configuration**
([12factor.net](https://12factor.net/)). Ship it in the
repo. New hire runs one command; if that command does not
produce a working stack, that is a bug the team fixes
before the hire's second day.

The Twelve-Factor App reference above is the load-bearing
one: configuration in environment variables, dev / prod
parity, port-binding, disposable processes. Even in 2026,
seventeen years after the original writeup, most 0-5
teams that get burnt by dev-environment drift are
teams that broke a Twelve-Factor rule (usually dev-prod
parity or config-in-code).

## First tests that actually run in CI

The "first tests" decision is a discipline, not a tool
choice. Three shapes to insist on at 0-5:

- **Unit tests for the domain logic** — the pure
  functions and modelling code that other tests will be
  layered on. Fast (milliseconds per test), no I/O,
  runs in every push.
- **A small integration slice** — end-to-end or
  API-level, covering the golden path of the primary
  product flow. Slower (seconds per test), hits a real
  database (containerised), runs in every push.
- **A smoke test that actually deploys** — a CI job
  that builds the deployable artifact, boots it, and
  sends one real request. The most valuable single
  test in a 0-5 codebase, because it catches the
  configuration drift the unit tests cannot see.

Two anti-patterns to name:

- **The mocked integration test** — an "integration
  test" that mocks out the database, the queue, the
  HTTP client. Runs fast, passes reliably, catches
  nothing. See the [`mod-105`](../mod-105-technical-debt-as-business-decision/README.md)
  discipline on empty tests as an inadvertent-reckless
  debt item.
- **The manual QA gate** — every merge waits on a
  human to click through the app. At 3 engineers this
  is fine; at 8 engineers it becomes the single
  bottleneck and the DORA Lead Time regresses
  dramatically. Automate the smoke test.

The 0-5 test suite does *not* need coverage targets, a
mutation-testing infrastructure, or a QA team. It needs
to run on every push in under five minutes and to fail
loudly when the golden path breaks. Everything else
grows on top of that substrate.

## DORA-as-baseline from day one

DORA's four keys — Deployment Frequency, Lead Time for
Changes, Change Failure Rate, and Mean Time to Restore
— are the topic of chapter 05. The 0-5 point is
smaller: **you should be measuring them from day one,
even if the numbers are trivial**. Reasons:

- Deployment Frequency at 0-5 engineers is *"how many
  merges to `main` produced a production deploy this
  week"*. Trivial to compute, and the number will
  regress the moment the team introduces a manual
  approval gate. Measuring it early gives you the
  before-and-after when someone proposes that gate.
- Lead Time for Changes at 0-5 is *"time from first
  commit on a branch to production"*. Trivial to
  compute from git history + deploy log, and the
  number will regress the moment CI slows down.
- Change Failure Rate at 0-5 is *"how many of the
  last twenty deploys required a rollback or a
  hotfix"*. Requires a lightweight "rollback / hotfix"
  tag on the commit; do it now, at 3 engineers, so the
  tag is habitual by 15.
- MTTR at 0-5 is *"how long from noticing the
  incident to a fix in production"*. At 0-5 the
  primary incident-notification path is a customer
  email or the CTO looking at the dashboard, and
  MTTR is measured in hours. Measure it anyway.

None of these need a dashboard vendor at 0-5. A
spreadsheet the CTO updates weekly is sufficient. The
point is that the *ritual* — measure, report, discuss —
is in place before the team is large enough that the
ritual is uncomfortable to introduce. See chapter 05
for the failure modes to guard against as the numbers
become more visible.

## Failure modes at the 0-5 stage

The two named failure modes, with concrete symptoms:

- **No-process at 0-5.** Symptoms: engineer #4's
  onboarding takes two weeks; a merge to `main` breaks
  the app on Fridays; every deploy is a slack post that
  starts *"is anyone touching X?"*. The CTO knows about
  it, but the room is small enough that fixing the
  symptom is cheap and the *pattern* is invisible until
  engineer #6 hits the cliff. The remedy is not more
  process; it is the four decisions in this chapter,
  authored explicitly, in the working repo.
- **Premature-process at 0-5.** Symptoms: a two-week
  sprint with three-hour planning meetings; a
  release-train with a QA sign-off gate; an "engineering
  standards" document that runs to forty pages. The
  CTO's last job's process, imported wholesale.
  Consumes an engineer per week in process overhead;
  produces no visible product velocity; over-corrects
  in a founder pushback and the whole thing is thrown
  out. The remedy is a *minimum* process — the four
  decisions here — and the deliberate deferral of the
  5→15 decisions (chapter 02) until the team hits the
  actual size.

The 0-5 posture: *"the smallest set of decisions that
will still be right at 15 engineers, and no more."*

## Summary

- The 0-5 phase is IC-plus-founder with no dedicated
  process staff. The trap is *"no process"* on one
  side and *"the process from my last job"* on the
  other.
- Four decisions set unrecoverable defaults:
  **repo layout**, **branching model**, **CI
  pipeline**, and **dev-environment convention**.
- Default **monorepo** — the multi-repo tax exceeds
  the monorepo tooling gap at 0-5, and cross-service
  refactors are frequent as the domain is being
  learned. See
  [`mod-102` chapter 01](../mod-102-architecture-under-uncertainty/README.md)
  on the monolith-first / evolutionary-architecture
  posture.
- Default **trunk-based development**, deploying from
  `main`. Reference:
  [trunkbaseddevelopment.com](https://trunkbaseddevelopment.com/).
  GitFlow is explicitly *not* recommended by its
  author for continuously-deployed web software; the
  2020 note on the original Driessen post
  ([nvie.com/posts/a-successful-git-branching-model](https://nvie.com/posts/a-successful-git-branching-model/))
  is direct about this.
- CI runs on every push, in under 5 minutes, produces
  the raw signal for the DORA numbers, and matches
  the dev-environment. GitHub Actions / GitLab CI /
  CircleCI are all fine; the vendor is not the
  decision.
- Dev-environment is a **one-command bring-up**
  (`docker compose up` or equivalent), with
  **Twelve-Factor**
  ([12factor.net](https://12factor.net/)) config
  discipline.
- Tests: unit tests on domain logic, a small
  integration slice, a smoke test that actually
  deploys. No mocked-out integration tests. No manual
  QA gates.
- **Measure DORA from day one**, even when the
  numbers are trivial. The ritual is what matters at
  this stage; chapter 05 covers the interpretation.
- The two failure modes — **no process** and
  **premature process** — both remedy to *"the
  smallest set of decisions that will still be right
  at 15 engineers"*. Author the four decisions
  explicitly, in the working repo, as short ADRs
  (see [`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/README.md)).

The chapter's paired exercise —
[`exercise-01-zero-to-five-first-process-drill.md`](exercises/exercise-01-zero-to-five-first-process-drill.md)
— walks you through authoring the four decisions as ADRs
for a hypothetical (or real) pre-seed startup, with the
justification each choice will still make sense at 15
engineers.

Chapter 02 walks the 5→15 transition — the point at
which the small-team-invisibility of the missing
process gives out and the team needs its first tech
lead, on-call rotation, RFC process, and engineering
handbook.
