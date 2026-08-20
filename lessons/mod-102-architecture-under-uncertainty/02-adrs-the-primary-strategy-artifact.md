# Architecture Decision Records — the Primary Strategy Artifact

> Michael Nygard's 2011 essay *Documenting Architecture
> Decisions* names the problem: agile teams are not opposed
> to documentation, they are opposed to *valueless*
> documentation. An ADR is the short, versioned, in-repo
> document that has value.
> ([cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions))

## Motivation

Every startup has a technical strategy. The interesting
question is whether it lives somewhere a new hire, a
technical advisor, a due-diligence reviewer, or the CTO
themselves in six months' time can *read* — or whether it
lives in a mix of tribal memory, one-off Slack threads, and
half-remembered whiteboard photos.

The Architecture Decision Record (ADR) is Michael Nygard's
2011 answer to that problem. It is a short, versioned,
in-repo document that names one meaningful architectural
decision, the context that forced it, the option that was
chosen, and the consequences the team is now living with. The
GitHub-hosted [`adr-tools`](https://github.com/npryce/adr-tools)
CLI (Nat Pryce's implementation of Nygard's template)
codifies the format and is one of the standard tooling paths.

For the pre-seed / seed CTO, ADRs do four load-bearing jobs
at once:

- **Onboarding artifact.** A new engineer who reads the ADRs
  in order understands the decisions the codebase currently
  reflects, why they were made, and — most importantly —
  what has already been ruled out and why.
- **CTO ↔ CEO / board / investor artifact.** An ADR-index in
  the repo is what turns "we made some choices" into "here
  are the twelve load-bearing decisions we have made, why we
  made each one, and what we would have to change to undo
  them". This is what a technical due-diligence reviewer
  reads (see mod-108).
- **Anti-drift mechanism.** When a well-scoped ADR names
  "we chose Postgres over DynamoDB for reasons X, Y, Z", a
  proposal six months later to *also* introduce DynamoDB
  either identifies the reason X, Y, or Z has changed —
  which is a real strategy update — or gets rejected on the
  basis of the original decision. Either outcome beats
  drifting into a two-persistence-store situation nobody
  argued for.
- **Chesterton's fence.** When a future maintainer looks at
  the choice and asks "why on earth did we do it this way?",
  the ADR tells them. The alternative is either respecting
  a decision no one understands or ripping it out and
  rediscovering the reason it was there — often the hard
  way. See mod-105 on the Chesterton's-fence discipline in
  the technical-debt context.

## The Nygard ADR format

Nygard's original format is deliberately short. Four sections
plus a header — the whole ADR should fit on a single screen.
Below is the format, verbatim from the Nygard essay, with
notes on how the pre-seed / seed CTO should use each section.

### Title

Short, imperative, descriptive. "Use Postgres for the primary
transactional data store". Not "Database". Not "How we chose
the database". A well-named ADR title is a self-contained
proposition the reader can agree or disagree with without
reading the body.

Conventionally numbered — `0001-use-postgres-for-primary-datastore.md`,
`0002-adopt-c4-diagrams-for-architecture-communication.md`,
`0003-modular-monolith-first-architecture.md`. The numbering is
append-only; superseded ADRs are not renumbered but marked
`Superseded by ADR-NNNN` (see *Status* below).

### Status

One of: **Proposed** / **Accepted** / **Deprecated** /
**Superseded by ADR-NNNN**. Nothing else.

At pre-seed / seed the workflow is usually: open a
`Proposed` ADR as part of a PR, one or two teammates comment,
the ADR is merged as `Accepted` with the code that implements
it (or in a separate PR that lands the same week). When a
future decision changes the answer, the old ADR gets
`Superseded by ADR-NNNN` and stays in the repo. **Never
delete an ADR**; the historical record is half the value.

### Context

The forces at play — technical, product, organisational,
financial, regulatory. This is where the *why* lives. Two
qualities matter:

- **Concrete, not aspirational.** "We need a database that
  supports transactional writes and joins, and our team of 3
  has Postgres experience but not DynamoDB experience" is
  concrete. "We need a database that scales" is aspirational
  and is not a decision-forcing constraint at pre-seed.
- **Time-stamped.** The context should be honest about the
  stage the company is at when the decision is being made.
  A future reader needs to know whether the decision reflects
  reality-as-of-2026-Q1 or reality-as-of-Series-A. When the
  context clearly no longer holds, the ADR is a candidate for
  supersession.

### Decision

The choice made, stated in the active voice: "We will use
Postgres 16 as the primary transactional data store." One
paragraph. If the decision needs more than one paragraph, it
is probably actually two decisions and should be split into
two ADRs.

### Consequences

The trade-offs the team is now living with — both the
positive ones ("boring, well-understood operational profile;
transactional writes with joins; one persistence store to
run") and the negative ones ("write throughput will cap
somewhere in the low tens of thousands per second per
primary, so a very-write-heavy workload will force a
follow-up ADR"). ISO/IEC 25010 (chapter 04) is a useful
vocabulary for organising this section.

The *Consequences* section is where the ADR proves its worth
six months later. If the consequences were named honestly,
the future ADR that supersedes this one starts from
"consequence B has materialised, and here is the new
decision that addresses it". If they were not named, the
supersession has to first re-derive why the original
decision was made.

## What deserves an ADR

Not every commit deserves an ADR. Nygard's rule of thumb is:
**decisions that a future team will need to understand in
order to safely change the code**. Concretely, for a pre-seed
/ seed startup:

- **Yes:** the primary persistence store (chapter 05);
  monolith-vs-services (chapter 01); the auth vendor
  (mod-103); the deploy target (a specific cloud, a specific
  runtime); the observability stack; the frontend framework;
  the language / runtime for the backend; the async-work
  substrate; the multi-tenancy model; the release-vs-deploy
  strategy (feature flags, canary, blue-green).
- **No:** which JS library formats dates; the CSS strategy
  inside a single component; whether to use `let` or `const`
  in TypeScript. These are code-review conversations, not
  architectural decisions.

A useful test: **if the wrong answer here would require a
quarter or more of engineering work to undo, it is an ADR**.
If the wrong answer would require a Friday-afternoon
refactor, it is not.

The first-year target for most seed-stage startups is
somewhere between 8 and 20 ADRs. Fewer than 8 usually means
decisions are being made but not documented; more than 40
usually means the ADR discipline has drifted into a
change-log for everything that touches the codebase.

## Where ADRs live and how they are referenced

The Nygard-original convention — followed by `adr-tools` and
by MADR ([adr.github.io](https://adr.github.io/)) — is a
`docs/adr/` directory (or `doc/adr/`) in the same repo as
the code, with numbered Markdown files:

```
docs/adr/
  0001-use-postgres-for-primary-datastore.md
  0002-adopt-c4-diagrams-for-architecture-communication.md
  0003-modular-monolith-first-architecture.md
  0004-clerk-for-b2b-auth.md
  README.md        # index; one line per ADR with title + status
```

The `README.md` in that directory is the index — one line per
ADR, in numeric order, with the title and the current status.
This is the artifact the CTO points a technical advisor at.

The ADRs should also be **referenced from the roadmap** —
when the roadmap doc says "Q3: launch usage-based billing",
the roadmap entry links to `ADR-0007: usage-based billing
metering model`. This is the mechanism by which the technical
strategy and the product roadmap stay wired to each other
rather than drifting apart. See mod-108 on how this becomes
the technical-narrative artifact for the board pre-read.

## Worked example

Below is a compact worked example. Note the shape more than
the specifics — the specifics belong to a real decision at a
real startup, not to a generic template.

```markdown
# 0003. Modular monolith as the first architecture

Date: 2026-02-14
Status: Accepted

## Context

- Team is 3 engineers, all backend-strong, all with prior
  Django experience. Nobody on the team has run Kubernetes
  in production.
- Product-market fit is unproven; the domain model has been
  re-shaped twice already since incorporation and is likely
  to be re-shaped again.
- The first 2-3 design partners are pre-launch; peak traffic
  in the next 12 months is measured in hundreds of RPS at
  worst, more likely in the tens.
- The runway calculation supports 18 months at current burn;
  every dollar spent on infrastructure operation is a dollar
  not spent on finding fit.

## Decision

We will build the first architecture as a **single Django
monolith**, deployed as one container to a managed platform
(Fly.io or Render — Fly chosen; see ADR-0004), with internal
module boundaries drawn along domain lines: `identity/`,
`billing/`, `catalog/`, `worker/`. Cross-module calls go
through explicit service classes; a fitness function in CI
enforces that no module imports another module's ORM models
directly.

## Consequences

- **Positive:** one deploy target, one on-call rotation, one
  database, one CI pipeline. Change is cheap; a pivot in the
  pricing or catalog model touches one module.
- **Positive:** the module boundaries make a StranglerFig
  extraction cheap when it is finally worth doing (see
  ADR-000X when we extract billing).
- **Negative:** the primary database is a single point of
  failure. Mitigation: managed Postgres with point-in-time
  recovery (ADR-0006) and read replicas when read load
  requires it.
- **Negative:** an outage of the monolith takes the whole
  product down. Acceptable given current SLO targets (see
  ADR-0009 on the reliability posture).
- **Negative:** the maximum ingest rate of a single monolith
  is bounded. We expect to hit that ceiling at roughly
  10× current traffic, at which point this ADR will be
  superseded by an extraction-plan ADR.
```

Note what this ADR does *not* do: it does not attempt to
justify the choice by appeal to general microservices-vs-
monolith arguments. It anchors the decision in *this team's
context at this stage*, states the decision in one paragraph,
and lists the trade-offs the team is now living with, including
the future condition that would force the ADR to be superseded.

## Common failure modes

- **The retroactive-ADR habit.** ADRs are written weeks or
  months after the decision was implicitly made, at which
  point the context has already faded and the ADR is a
  post-hoc rationalisation rather than a decision record.
  Fix: open a `Proposed` ADR before or with the PR that
  implements the change, not after.
- **The essay-ADR.** ADRs balloon to five pages and lose the
  one-decision, one-page discipline. Fix: if the ADR is
  longer than one screen, either split it or edit it down;
  the reader who needs the depth will read the linked issue
  / RFC / spike report.
- **The dead-index.** The ADR directory exists but the
  `README.md` index has not been updated in six months.
  Fix: automate the index (one-line grep + generate) as part
  of CI, or add a fitness function that fails the build if
  a new ADR is not indexed.
- **The mono-repo, mono-decision anti-pattern.** Every
  decision, however trivial, gets an ADR — dates included,
  and the index has 200 entries. This looks disciplined and
  is actually the same failure mode as the dead-index; no
  one reads a 200-entry list. Fix: apply the "quarter of
  engineering work to undo" test above.
- **The unreferenced-ADR.** ADRs exist but nothing in the
  roadmap or the C4 diagrams links to them. Fix: put the
  link in the roadmap doc and in the C4 diagram legends —
  see chapter 03 on how the C4 System Context diagram
  should point at the load-bearing ADRs.

## Tooling that helps but is not required

The ADR discipline is a habit, not a tool. Tools that help
sustain it, without any of them being load-bearing:

- **`adr-tools`** —
  [github.com/npryce/adr-tools](https://github.com/npryce/adr-tools) —
  Nat Pryce's original CLI. `adr new "title"` creates a
  numbered, dated, filled-in Nygard template.
- **MADR** — [adr.github.io](https://adr.github.io/) — a
  variant on Nygard's format with a slightly more structured
  template; supported by several IDE plugins.
- **`log4brains`** —
  [github.com/thomvaill/log4brains](https://github.com/thomvaill/log4brains) —
  static-site generator that renders the ADR directory as a
  browsable log; useful once you have more than about 15
  ADRs and want an out-of-repo view for stakeholders who
  don't clone the repo.

Do not spend a week choosing between them at the pre-seed /
seed stage. Any of the three, plus discipline, is worth more
than the best choice plus no discipline.

## Summary

- ADRs are the primary technical-strategy artifact at
  pre-seed / seed — one per meaningful decision, versioned
  in the repo, referenced from the roadmap.
- Nygard's four-section format — **Status / Context /
  Decision / Consequences** — is the canonical shape. Keep
  each ADR to one screen.
- The decisions that deserve ADRs are the ones a future
  team needs to understand in order to safely change the
  code. If the wrong answer would take a quarter to undo,
  it is an ADR.
- Store ADRs in `docs/adr/` with an index `README.md`.
  Never delete a superseded ADR; mark it as superseded and
  keep it.
- The most common failure mode is retroactive ADRs written
  after the decision has faded from context. Open the
  `Proposed` ADR before or with the PR that implements the
  change.

The chapter's paired exercise —
[`exercise-02-adr-authoring-for-three-real-decisions.md`](exercises/exercise-02-adr-authoring-for-three-real-decisions.md)
— walks the authoring of three Nygard-format ADRs for real
decisions your (or a real reference) startup is facing this
quarter.
