# MonolithFirst and Evolutionary Architecture

> "Almost all the successful microservice stories have started
> with a monolith that got too big and was broken up. Almost
> all the stories where I've heard of a system that was built
> as a microservice system from scratch, it has ended up in
> serious trouble." — Martin Fowler, *MonolithFirst*
> ([martinfowler.com/bliki/MonolithFirst.html](https://martinfowler.com/bliki/MonolithFirst.html))

## Motivation

The first architecture the CTO ships is not the architecture
the company will still be running when it exits. It cannot be —
product-market fit is unproven, the domain model is still
shifting under weekly customer conversations, the team is 1-8
engineers, and every dollar of runway spent on premature
structure is a dollar not spent on the discovery work that
either finds fit or doesn't. This is the situation almost every
component of *Building Evolutionary Architectures*
([Ford, Parsons, Kua](https://www.oreilly.com/library/view/building-evolutionary-architectures/9781491986356/))
was written to name.

Two failure modes are common at this stage. Both cost the same
thing — runway — and both are avoidable if the CTO enters the
seat with a clear default.

- **Over-engineering.** The CTO builds a microservices platform
  on Kubernetes with a message bus, an event store, and a
  service mesh in the first quarter, on the theory that
  "we'll need it eventually". The team spends the seed round
  operating infrastructure instead of finding fit. Fowler's
  *MonolithFirst* essay is the canonical write-up of why this
  is expensive at pre-seed / seed.
- **Under-engineering as an alibi.** The CTO ships a single
  Rails / Django / Next.js codebase with no module boundaries,
  no ADRs, no fitness functions, and no plan for extracting
  the first service later. This is fine until it isn't; by
  the time the codebase is 300 KLOC and every change ripples
  across every feature, the extraction is a rewrite. Fowler's
  companion essay *StranglerFigApplication*
  ([martinfowler.com/bliki/StranglerFigApplication.html](https://martinfowler.com/bliki/StranglerFigApplication.html))
  is the canonical write-up of the recovery path — which is
  much cheaper if you did *not* skip the module boundaries
  in the first place.

This chapter names the default architecture at pre-seed / seed,
the evolutionary-architecture vocabulary that guards it, and
the *cheap to change* invariant that both defaults are pointed
at.

## The default: a modular monolith with strangler-fig-ready seams

For the vast majority of pre-seed and seed startups, the right
first architecture is a **modular monolith** — one deployable,
one relational database, one repository, but with internal
module boundaries drawn deliberately along domain lines and
with the seams that would let you extract a module into a
service later.

Concretely, in a Django / Rails / Next.js / FastAPI codebase,
this looks like:

- One deploy target (a container image or a serverless
  bundle), one CI pipeline, one on-call rotation.
- One relational database (Postgres is a defensible default —
  see chapter 05 for the CAP-vocabulary defence). Schema
  organised by domain module (e.g. `billing`, `identity`,
  `catalog`) with foreign keys crossing module boundaries
  only where the domain genuinely requires it.
- Application code organised by domain module, not by
  technical layer. `billing/` contains its models, services,
  handlers, and background jobs; `identity/` contains
  theirs. Cross-module calls go through a *narrow* interface
  (a service class, a domain event) rather than reaching
  into another module's models directly.
- A single background-job runner (Sidekiq, Celery, BullMQ,
  or the equivalent for your language) rather than a
  message-bus platform.
- Feature flags for the release-vs-deploy split — so that
  merging code is not the same event as exposing behaviour
  to users.

This is *not* a "microservices-lite" architecture; it is a
monolith with the seams drawn so that when the strangler-fig
extraction is worth doing later, it can be done incrementally
rather than as a rewrite.

## Why "cheap to change" is the load-bearing invariant

At pre-seed / seed, the single non-negotiable property of the
architecture is that it must be *cheap to change*. This
sub-ordinates most of the other architectural properties you
might reach for.

- **Not scale.** You do not have the traffic to require
  scale-oriented architecture. If you do, that is a lucky
  problem and you can afford to hire (or defer up — see
  chapter 06 and the boundary to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning))
  to fix it.
- **Not extreme reliability.** You need to be reliable enough
  that customers do not fire you and that the first design
  partner keeps calling; you do not need three-nines or
  four-nines yet. See chapter 04 on how ISO/IEC 25010's
  reliability sub-characteristics let you reason about
  "reliable enough" without over-committing.
- **Not framework purity.** If Django's ORM and Postgres and
  Rails-flavoured background jobs let you ship the next
  customer commitment on Friday, the fact that a cleaner
  hexagonal architecture exists on paper is not the
  argument for adopting it this quarter.

*Cheap to change* is what lets you take the next customer
conversation, learn that the pricing model is different from
the one you assumed, and re-model the domain in a week rather
than a quarter. It is what lets the seed CTO delete a feature
that is not being used without triggering a two-week
regression-testing pass. It is what makes the pivot survivable.

Everything in this module — ADRs, C4 diagrams, quality-
attribute trade-offs, staged extraction, spikes with kill
criteria — is in service of this invariant. Every choice you
make that raises the cost of the next change is a choice you
should be able to defend.

## Evolutionary architecture and fitness functions

*Building Evolutionary Architectures* names the mechanism by
which an architecture stays cheap to change over time: **fitness
functions** — executable checks that assert the architectural
properties you cannot afford to lose as the system evolves.

Fitness functions are not the same as unit tests. Unit tests
assert that a piece of code does what it says. Fitness
functions assert that a *system-level architectural property*
still holds. Concretely, for a pre-seed / seed startup:

- **Module-boundary fitness function.** Assert that the
  `billing/` module never imports directly from
  `catalog/models`. Tools like ArchUnit (Java), Dependency
  Cruiser (JS/TS), `import-linter` (Python), or a simple
  language-agnostic AST script in CI will fail the build if
  the assertion is violated.
- **Cold-start-time fitness function.** Assert that the app
  boots in under N seconds on a clean environment. A regression
  here is usually the first signal of accidental complexity
  creeping into module dependencies.
- **Migration-safety fitness function.** Assert that every
  database migration is expand-then-contract-safe (adds
  columns and backfills before removing anything), so that
  deploys can be rolled back without data loss.
- **Vendor-lock fitness function.** Assert that only the
  `infra/` module imports the cloud SDK, so that a
  build-vs-buy re-decision in mod-103 does not require a
  cross-cutting rewrite.

A fitness function is not "aspiration written on a whiteboard".
It runs in CI, it fails the build when violated, and it is
the mechanism by which the ADR that says "we want to keep
billing and catalog decoupled" is enforced against the drift
that would otherwise erode it. Chapter 04's exercise walks the
authoring of three of these; the *Building Evolutionary
Architectures* book is the deeper reference.

## StranglerFig later — the extraction pattern the modular monolith is set up for

The modular monolith is not the *final* architecture. The
seam-drawing is what makes the *StranglerFig* extraction cheap
when it is finally worth doing.

Fowler's StranglerFig pattern
([martinfowler.com/bliki/StranglerFigApplication.html](https://martinfowler.com/bliki/StranglerFigApplication.html))
takes its name from the strangler-fig vine that grows around
an existing tree, gradually replacing it. Applied to software:

- You do not stop the world and rewrite. You put a routing
  layer (an API gateway, a reverse proxy, or feature flags)
  in front of the module you want to extract.
- You build the replacement alongside the original,
  intercepting one endpoint or one background-job kind at a
  time and routing it to the new implementation.
- You keep both alive until the last consumer of the old
  path is gone, then delete the old implementation.

This is the pattern chapter 05 revisits when it discusses when
service extraction is worth the cost. It is also the pattern
mod-105 (technical debt) revisits when it discusses
deprecate-vs-rewrite decisions on load-bearing legacy code —
the same pattern applies at both levels.

The key insight for the pre-seed / seed CTO is: **you do not
need to run a StranglerFig extraction yet, but you do need to
architect the monolith so that one is possible later**. That
is what the module boundaries and the narrow cross-module
interfaces buy you. Skipping them because "we'll refactor when
we need to" is the *under-engineering as an alibi* failure
mode named above; the refactor never happens because it has
become a rewrite.

## Concrete example: the pricing-model pivot

To make the *cheap to change* invariant concrete, consider a
typical seed-stage pivot: a B2B SaaS company launches with
per-seat pricing. Three months in, the first three enterprise
prospects all ask for usage-based pricing instead.

- **In a modular-monolith codebase with the billing seam
  respected** — the change is bounded to the `billing/`
  module. New pricing rules, new invoice generation, new
  usage-metering hooks. The `catalog/` and `identity/`
  modules do not know the billing model has changed. Two
  weeks of work; the pivot is survivable.
- **In an accidentally-cross-cutting codebase** — pricing
  logic has leaked into the catalog module, the identity
  module, the reporting module, and three background jobs.
  The change touches every module and every test file. Two
  quarters of work; the pivot happens under pressure and
  ships with regressions.
- **In a premature microservices architecture** — pricing
  logic is in the billing service, the entitlements
  service, the reporting service, and cached in the API
  gateway. The change requires coordinated deploys across
  four services and a data-migration plan for the read
  models. Two quarters of work *and* an availability
  incident when the first coordinated deploy misses a
  dependency.

The first outcome is not luck. It is a direct consequence of
the CTO having chosen a modular monolith with respected
seams as the default architecture, and having enforced the
seams with a module-boundary fitness function so they did
not silently rot.

## Summary

- The default architecture at pre-seed / seed is a **modular
  monolith with strangler-fig-ready seams** — one
  deployable, one database, deliberate module boundaries.
  See Fowler's *MonolithFirst* and *StranglerFigApplication*
  for the canonical write-ups.
- The load-bearing invariant is **cheap to change**, not
  scale, not extreme reliability, not framework purity.
  Everything else in this module is in service of that
  invariant.
- Evolutionary architecture protects the invariant over
  time with **fitness functions** — executable CI checks
  that assert system-level architectural properties (module
  boundaries, boot time, vendor isolation, migration
  safety). See *Building Evolutionary Architectures*
  (Ford, Parsons, Kua).
- The modular monolith is not the final architecture. It
  is the architecture the StranglerFig extraction pattern
  is *cheap to apply against later*. Skipping the module
  boundaries because "we'll refactor when we need to" is
  the failure mode that turns the extraction into a
  rewrite.

The chapter's paired exercise —
[`exercise-01-monolith-first-vs-services-decision-drill.md`](exercises/exercise-01-monolith-first-vs-services-decision-drill.md)
— walks six ambiguous starting-architecture scenarios and
asks for an explicit monolith / modular monolith / services
call for each. The exercise for chapter 05 revisits the
extraction decision from the other direction.
