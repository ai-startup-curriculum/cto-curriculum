# Monolith → Modular Monolith → Services, and the CAP Vocabulary

> "The C in CAP is not the same C as the C in ACID. Read the
> proof carefully and you will see that C in CAP is a very
> specific kind of consistency — linearisability." — paraphrase
> of the clarification Seth Gilbert and Nancy Lynch's 2002
> proof made necessary
> ([groups.csail.mit.edu/tds/papers/Gilbert/Brewer2.pdf](https://groups.csail.mit.edu/tds/papers/Gilbert/Brewer2.pdf))

## Motivation

Two decisions dominate the first year of a startup's
persistence architecture:

- **How many code deployables do we have?** One monolith,
  a modular monolith, or an extracted-services architecture.
  Chapter 01 argued for the modular monolith as the seed
  default.
- **What is the consistency model of our data?** A single
  relational store, a single relational store plus a cache,
  a relational store plus an eventually-consistent
  document / KV store, or multiple stores of different
  kinds with a consistency plan that spans them.

The two decisions are connected. A single-database monolith
is trivially consistent — one primary, one transaction, one
answer. As soon as you extract a second service with its own
data store, or add a second store to the same monolith, you
have a distributed system and the CAP theorem becomes a
constraint on the design.

This chapter names the staged monolith → modular monolith →
services decision, the CAP-theorem vocabulary the CTO uses
to defend the persistence choice, and the eventual-
consistency vocabulary that lets an ADR say more than "we
picked Postgres".

## The staged monolith → services decision

The decision is a *sequence*, not a religious choice. Chapter
01 named the seed-stage default (modular monolith). This
chapter names the sequence and the triggers that move you
along it.

- **Stage 1 — Single monolith, single database.** One
  deployable, one CI pipeline, one on-call rotation, one
  primary database. Module boundaries in code but no
  physical separation. This is the pre-seed default; often
  the seed default too.
- **Stage 2 — Modular monolith, single database.** Same as
  Stage 1 but with the module boundaries enforced by a
  fitness function (see chapter 01), so they do not rot as
  the team grows. This is where most seed-stage startups
  should be by month 6.
- **Stage 3 — First service extracted, still single primary
  database (mostly).** Usually the first extraction is a
  workload that is genuinely different — a long-running
  ingest job, a resource-heavy ML inference endpoint, a
  webhook-receiver that needs different scaling behaviour.
  The StranglerFig pattern (chapter 01) is how the
  extraction is done incrementally.
- **Stage 4 — Multiple services, multiple stores, with a
  cross-store consistency plan.** This is a real
  distributed system and is where the CAP theorem starts to
  bind the design.

Sam Newman's *Building Microservices, 2nd edition*
([samnewman.io/books/building_microservices_2nd_edition](https://samnewman.io/books/building_microservices_2nd_edition/))
is the canonical reference on why the sequence matters and
what the triggers are. His "shift from monolith to services
because of a specific pressure, not because services are
fashionable" framing is the one this module inherits.

### Triggers that move you along the sequence

The right time to extract a service is not "when we hit N
requests per second" — it is when one of the following
pressures actually shows up:

- **The scaling profile diverges.** One workload (webhook
  ingest, ML inference, image processing) needs
  fundamentally different resources — memory, CPU, GPU,
  scale-to-zero, scale-to-1000 — from the rest of the
  monolith, and running the whole monolith at that shape is
  wasteful or infeasible.
- **The team-topology forces it.** Two teams working on the
  same monolith are stepping on each other in the same
  hot files. This becomes a real signal past ~15
  engineers; below that, the modular monolith almost always
  wins on the reasoning cost. See Team Topologies
  ([teamtopologies.com](https://teamtopologies.com/book))
  for the deeper argument, which mod-104 revisits.
- **The failure-isolation profile diverges.** One workload
  has a much lower reliability budget than the rest of the
  system (say, a real-time notification path that must not
  block a payment path), and containing its failures
  requires a separate deploy target.
- **The compliance / data-residency profile diverges.** A
  regulated workload needs its data in a specific region /
  under a specific tenant isolation model, and the
  monolith's default deploy shape cannot honour it.

None of these are "we'll hit them eventually" — they are
all "here is the specific pressure that has arrived, and
here is the ADR that authorises the extraction to relieve
it". Newman's book calls out the *symptom-driven*
extraction pattern by name.

### The two-persistence-store threshold

The single most consequential move along the sequence is the
one that adds the **second persistence store**. Up to that
point, "consistency" is what the database's transactions
give you and the CAP theorem is not a design constraint —
you have one primary and one answer. As soon as you add a
second store — a search index, a cache, a document store, a
data-warehouse read replica, another service's own database
— you have a distributed system and the CAP theorem starts
to bind the design.

This is worth flagging in an ADR when it happens. "ADR-000X:
add Elasticsearch as a search-only read replica of the
Postgres catalog" is not a small decision even if it feels
like plumbing; it is the decision that turns your data
architecture into a distributed one.

## The CAP theorem, precisely stated

Eric Brewer's 2000 PODC keynote conjectured the CAP theorem
([Brewer, 2000](https://sites.cs.ucsb.edu/~rich/class/cs293b-cloud/papers/Brewer_podc_keynote_2000.pdf));
Seth Gilbert and Nancy Lynch proved it in 2002
([Gilbert & Lynch, 2002](https://groups.csail.mit.edu/tds/papers/Gilbert/Brewer2.pdf)).
Brewer's own 2012 retrospective *"CAP Twelve Years Later:
How the Rules Have Changed"*
([IEEE Computer, June 2012](https://sites.cs.ucsb.edu/~rich/class/cs293b-cloud/papers/Brewer_computer_2012.pdf))
is the second reference the CTO should read.

The exact statement — often mis-cited — is:

> In a distributed system in which a network partition can
> occur (P), it is impossible for the system to
> simultaneously guarantee both linearisable consistency
> (C) and availability for every request (A). During a
> partition, the system must choose to sacrifice either C
> or A.

Three points worth internalising, because they are the ones
most CTOs misremember:

- **The C in CAP is linearisability**, not the C in ACID.
  ACID's C is "the transaction preserves invariants";
  CAP's C is "every read sees the most recent successful
  write across the whole distributed system". A store can
  be transactional (ACID) without being linearisable (CAP).
  The Gilbert-Lynch proof is precise about this.
- **P is not optional.** If two nodes are separated by a
  network you do not control (which is every network you do
  not own end-to-end, i.e. every real network), a partition
  can occur. You do not choose to "give up P" in exchange
  for CA; you choose how the system behaves *when P
  happens*.
- **The choice is CP or AP, not "we have all three".** A
  system that claims all three is either not actually
  distributed (it has one node) or is deferring the
  decision until the partition happens and picking badly
  under pressure.

Brewer's 2012 retrospective goes further and points out
that the CP-vs-AP framing is too coarse — real systems make
the trade at the level of individual operations, not the
whole store. This is the *PACELC* refinement Daniel Abadi
proposed
([Abadi, IEEE Computer 2012](https://www.cs.umd.edu/~abadi/papers/abadi-pacelc.pdf)):
in a partition (P) choose A or C; else (E) choose L
(latency) or C (consistency). PACELC is a more useful
vocabulary for real systems and is worth learning after CAP.

## Eventual consistency, vocabulary the CTO needs

Werner Vogels's 2008 *Eventually Consistent*
([allthingsdistributed.com/2008/12/eventually_consistent.html](https://www.allthingsdistributed.com/2008/12/eventually_consistent.html))
is the shortest useful reference on the vocabulary
distributed systems people use for "the store is consistent
eventually, but not right now". The pieces the CTO needs:

- **Strong consistency** — a read returns the last written
  value (in a linearisable store, from anywhere; in a
  sequentially-consistent store, from the same client's
  perspective). Postgres in a single primary is this.
- **Eventual consistency** — if no new updates are made,
  eventually all reads will return the last written value.
  DynamoDB in its default read mode is this. So is a cache
  with TTL-based invalidation.
- **Read-your-writes consistency** — a client's subsequent
  reads see its own writes. Weaker than strong consistency,
  stronger than raw eventual consistency; the property
  most user-facing UX assumes without saying so.
- **Causal consistency** — writes that are causally related
  are observed in order. Useful vocabulary for the
  notification-ordering problem when a second store is
  involved.

Martin Kleppmann's *Designing Data-Intensive Applications*
([dataintensive.net](https://dataintensive.net/)) is the
book-length reference and is worth reading in full at least
once — the parts most immediately load-bearing for the
pre-seed / seed CTO are the chapters on replication,
partitioning, and consistency (roughly chapters 5, 6, 7,
and 9 in the 1st-edition ordering).

## Which store to default to

For most pre-seed / seed startups selling a transactional
B2B product, the defensible default is:

- **Primary transactional store:** a managed relational
  database (Postgres on RDS, Cloud SQL, or Neon; MySQL /
  Aurora if the team has stronger MySQL fluency). Strong
  consistency, transactional writes with joins,
  well-understood operational profile. Boring in the good
  way.
- **Search:** postpone as long as `LIKE` and `ILIKE` queries
  work. When they no longer do, add a Postgres full-text
  search column before you add a second store. When *that*
  no longer works, adopt Meilisearch, Typesense, Elastic,
  or the cloud's managed equivalent as a read-replica; open
  the ADR that names it as a second persistence store.
- **Cache:** postpone as long as the database is fast
  enough. When it isn't, add a request-level in-memory
  cache before you add Redis. When you do add Redis, treat
  it as an ephemeral cache, not a durable store —
  reasoning about the state of a system where the "cache"
  is actually a second source of truth is one of the
  hardest classes of distributed-systems bug.
- **Analytics / warehouse:** postpone as long as `EXPLAIN
  ANALYZE` on the primary is acceptable. When it isn't,
  add a managed warehouse (Snowflake, BigQuery, DuckDB in
  a small deployment) as a read replica; the ADR that
  authorises this is the one that names the reporting
  workload as a distinct workload.
- **AI-native workloads:** vector stores and inference
  endpoints have their own trade-offs; the CTO consumes
  the guidance in mod-103 and — for depth — defers up to
  [`ai-infra-ml-platform`](../../../ai-infra-ml-platform-learning) (level 30).

Every one of these defaults is a stage-appropriate choice,
not a permanent one. Each becomes a superseded ADR when a
specific pressure — a scaling profile, a compliance need, a
data-model change — actually forces the follow-on.

## Where deep multi-store / multi-region architecture goes

Once the system is genuinely distributed (multiple services,
multiple stores, multi-region reads / writes, cross-store
consistency plan), the depth of architectural work required
is above the pre-seed / seed CTO's scope. Concretely, the
following work defers up:

- **Multi-region active-active / active-passive design**,
  and the failure-mode analysis that goes with it, defers
  up to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45).
- **Multi-tenant isolation at scale** — silo vs. pool vs.
  bridge, cross-tenant noisy-neighbour containment — defers
  up to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning).
  See the AWS SaaS Lens
  ([docs.aws.amazon.com/wellarchitected/latest/saas-lens](https://docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html))
  for the canonical vocabulary.
- **Distributed-consensus systems** — deploying and
  operating Raft / Paxos / Zookeeper-class infrastructure
  — defers up to
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55).

The seed-stage CTO's job on these topics is to (a) recognise
that a design is heading into them, (b) name the pressure
that is pushing there in an ADR, and (c) either bring in the
depth (hire, contractor, technical-advisor call) or defer
the design until the pressure is real. Chapter 06's spike
discipline is the mechanism for the "we don't know yet"
case.

## Concrete example: adding search

To make the two-store threshold concrete, walk the ADR
sequence for "we need product search":

- **ADR-000X (Postgres `ILIKE`, no schema change).** Meets
  the requirement for 90% of expected queries; latency
  budget is fine at current data volume. Trade-off named:
  degrades at ~100k product records.
- **ADR-000X+1 (Postgres `tsvector` full-text index).**
  Extends the runway to ~1M records without adding a
  second store. Still one persistence store, still
  strongly consistent, still transactional.
- **ADR-000X+2 (add Meilisearch or Typesense as a
  read-replica search index).** *This* is the two-store
  threshold ADR. The context section names the specific
  pressure (query latency exceeds SLO at N records, or a
  faceted-search feature that Postgres does not do well).
  The consequences section names the CAP-vocabulary
  trade-off — the search index is eventually consistent
  with respect to the primary, we accept read-your-writes
  staleness of up to N seconds on newly-indexed products.

Note how the third ADR is qualitatively different from the
first two. The first two are single-store optimisations;
the third is the decision to become a distributed system,
and the ADR is where the consistency trade-off is named.

## Common failure modes

- **"Microservices from day one".** Chapter 01 covered
  this; it belongs on the failure-mode list here too.
- **Adding a second store as a "cache" and then relying on
  its data.** The Redis-that-became-the-source-of-truth
  anti-pattern. If the second store is load-bearing, it
  deserves an ADR that names it as such and a consistency
  plan.
- **Distributed transactions across services.** Two-phase
  commit across microservice boundaries is a design smell
  at any scale and a symptom of a service boundary drawn
  in the wrong place at startup scale. Draw the boundary
  around the transactional unit; extract the *rest*.
- **"We chose Mongo / DynamoDB because it's web-scale".**
  If the argument for the store is anything other than
  the specific pressure it relieves and the specific
  trade-off it accepts, the ADR does not exist. Reopen it.
- **Confusing ACID's C with CAP's C.** Leads to statements
  like "Postgres is CA in CAP terms", which is
  meaningfully wrong. Read the Gilbert-Lynch proof and the
  Brewer 2012 retrospective.

## Summary

- The monolith → modular monolith → services decision is a
  **sequence**, not a religious choice. Chapter 01's
  modular-monolith default is stage 2 of the sequence;
  stages 3 and 4 are unlocked by specific pressures —
  scaling profile divergence, team-topology divergence,
  failure-isolation divergence, compliance divergence.
- The **two-persistence-store threshold** is the single
  most consequential move along the sequence. Cross it in
  an ADR that names the CAP-vocabulary trade-off, not by
  accident.
- The CAP theorem's exact statement: in a partition, you
  must choose between linearisable consistency (C) and
  availability (A). P is not optional. Real systems make
  the trade per-operation — see PACELC.
- Vocabulary the CTO needs: strong / eventual /
  read-your-writes / causal consistency. Werner Vogels's
  *Eventually Consistent* is the shortest reference;
  Kleppmann's *Designing Data-Intensive Applications* is
  the book-length reference.
- Default persistence: managed Postgres for the primary
  transactional store; postpone the second store as long
  as possible; when you add one, name it in an ADR as
  crossing the distributed-system threshold.
- Deep multi-region, multi-tenant, multi-store
  architecture at scale defers up to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) and
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55).

The exercise for chapter 01
([`exercise-01-monolith-first-vs-services-decision-drill.md`](exercises/exercise-01-monolith-first-vs-services-decision-drill.md))
walks the extraction-vs-modular-monolith decision from the
starting-architecture side; the exercise for this chapter is
the one that pairs it with the consistency-model vocabulary,
covered inside
[`exercise-04-iso-25010-quality-attribute-trade-off-map.md`](exercises/exercise-04-iso-25010-quality-attribute-trade-off-map.md)
and the persistence choice you must defend in
[`exercise-02-adr-authoring-for-three-real-decisions.md`](exercises/exercise-02-adr-authoring-for-three-real-decisions.md).
