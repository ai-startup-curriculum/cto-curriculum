# Team Topologies at 5, 15, and 25 Engineers

> "For fast flow, you need only four fundamental team
> types: **stream-aligned**, **platform**, **enabling**,
> and **complicated-subsystem**." — Matthew Skelton and
> Manuel Pais, *Team Topologies*
> ([teamtopologies.com/book](https://teamtopologies.com/book)).

## Motivation

Once the founding-team stage passes and there are more
than a handful of engineers, the CTO is no longer
deciding "who is the next hire?" as an isolated question.
They are deciding what *team* the next hire joins, what
that team *owns*, what it *does not* own, and *who else*
it must talk to in order to ship.

Get these decisions right and each new hire slots into a
team that already has a clear charter, a clear ownership
boundary, and a clear interface to its neighbours. Get
them wrong and you produce two failure modes the field
has been documenting since the 1970s:

- **Conway's Law backfires** — the system architecture
  becomes an accidental artifact of an accidental org
  chart, and every roadmap item requires a
  three-team-plus-a-Slack-channel coordination dance
  to ship. Melvin Conway's original 1968 paper is at
  [melconway.com/Home/Committees_Paper.html](https://www.melconway.com/Home/Committees_Paper.html).
- **Everything-is-everyone's-team** — no team owns
  anything specifically. Every incident is un-owned,
  every roadmap item is claimed by two teams and blamed
  on the third, and the CTO is the resolution mechanism
  for every ambiguity. This is the anti-pattern the
  Skelton-and-Pais book was written against.

*Team Topologies* names a small vocabulary — four team
types and three inter-team interaction modes — that lets
the CTO reason about org shape at each stage without
inventing new terminology at every hire. This chapter
applies that vocabulary to the three most consequential
transitions in the pre-Series-B life of an engineering
org: **five engineers**, **fifteen engineers**, and
**twenty-five engineers**.

## The four team types (very brief refresher)

The *Team Topologies* vocabulary — read the book itself
at [teamtopologies.com/book](https://teamtopologies.com/book)
for the full treatment; a short public summary is at
[teamtopologies.com/key-concepts](https://teamtopologies.com/key-concepts).

- **Stream-aligned team** — a team aligned to a
  single, valuable stream of work: a product area, a
  customer segment, a specific business capability.
  Owns end-to-end delivery from customer request to
  production. The *default* team type; other team types
  exist only in service of stream-aligned teams.
- **Platform team** — provides an internal platform (a
  set of self-service capabilities) that stream-aligned
  teams consume without having to think about the
  underlying complexity. Reduces cognitive load on
  stream-aligned teams. Earns its keep when the
  platform capabilities are visibly *pulled* by
  stream-aligned teams, not *pushed* by the platform
  team's own conviction.
- **Enabling team** — a small team of specialists (SRE,
  security, DX, ML platform, data infra) that helps
  stream-aligned teams acquire missing capabilities via
  time-boxed engagements. Explicitly *not* a permanent
  home for the capability — the goal is to *transfer*
  the capability to the stream-aligned team and then
  disengage.
- **Complicated-subsystem team** — a team dedicated to
  a subsystem whose complexity requires specialist
  knowledge most engineers do not have (a compiler, a
  learned ranker, a physics simulator, a video codec,
  a novel cryptographic scheme). Exists so
  stream-aligned teams can use the subsystem without
  having to become experts in it.

And the three **interaction modes** — the shapes of
communication between teams:

- **Collaboration** — two teams work closely together
  for a bounded period to discover new patterns.
  High-bandwidth, high-cost; use sparingly.
- **X-as-a-Service** — one team consumes something
  another team provides, through a clear interface.
  Low-bandwidth, low-cost; the default when the
  interface is stable.
- **Facilitating** — one team temporarily helps another
  team learn or adopt something. The natural mode for
  enabling teams.

Explicit interaction modes are what stop the "everyone
talks to everyone about everything" default. The CTO's
job is to name, for every pair of teams that must
interact, *which* of the three modes applies.

## Five engineers — you are one stream-aligned team

At five engineers (typically two founders + three
founding engineers, per chapter 01's plan and chapter 03's
profile), the correct topology is:

- **One stream-aligned team.**
- **No platform team.**
- **No enabling team.**
- **No complicated-subsystem team.**

The whole team is a single stream-aligned team, aligned
to the *product* as the stream. Everyone owns the whole
product surface end-to-end. Ownership is by
subject-matter competence, not by team boundary — the
back-end person owns the API, the ML person owns the
ranker, the full-stack person owns the demo flow, but
they all live in one team, one standup, one on-call
rotation.

Two temptations to resist at five:

- **Do not create a platform team.** At five engineers,
  the "platform" is one person's Terraform files and one
  person's CI setup. Making that a team gives it a
  charter, a headcount growth path, and a set of
  incentives to build platform capabilities nobody has
  asked for. The platform capabilities the team needs
  at five are best owned as *one engineer's shared
  responsibility* on the same stream-aligned team.
- **Do not create a "data team" of one.** A single data
  engineer with no team is either a stream-aligned
  engineer with a data specialism (fine, no separate
  team needed) or an isolated capability with no
  customer inside the company (a headcount waste that
  reads like a functional org).

The correct *interaction* at five engineers is a single
in-person / in-Slack conversation. Interaction modes
between teams do not apply because there is only one
team. The CTO's role is IC leader of the team + primary
technical decision-maker.

Cognitive-load caveat: **do not exceed one team past 6-8
ICs reporting to a single lead.** The Skelton / Pais
book is direct that a stream-aligned team past ~8-9
people starts to fragment on cognitive load —
subsystems accumulate that any given team member no
longer holds in their head. That is the trigger for
chapter 05's first-EM / first-tech-lead conversation, and
for the transition to the fifteen-engineer shape.

## Fifteen engineers — two stream-aligned teams plus an enabling role

At fifteen engineers, the single stream-aligned team has
fractured under cognitive load. The correct topology
now is:

- **Two stream-aligned teams**, split along the *most
  natural product / customer boundary you already have*.
  Not along a technical layer (front-end team vs.
  back-end team) — that produces the exact
  cross-cutting coordination cost the vocabulary is
  designed to prevent. Split along product surfaces
  (e.g. "acquisition-and-onboarding" vs.
  "power-user-tools") or customer segments
  (e.g. "self-serve" vs. "enterprise").
- **One enabling role or partial-team**, typically an
  SRE / DevEx / platform-oriented engineer or two, whose
  charter is to *help* the two stream-aligned teams
  acquire capabilities they are missing — better CI,
  better observability, faster incident response — and
  to transfer those capabilities back rather than owning
  them permanently.
- **Still no dedicated platform team.**
- **Still no complicated-subsystem team**, unless the
  product has one — an ML pipeline that is genuinely a
  compiler-like specialism, a video-processing kernel,
  a novel cryptographic protocol — in which case the
  team is one or two engineers and its interface to the
  stream-aligned teams is X-as-a-Service.

The interaction modes now start to matter:

- Between the two **stream-aligned teams**: default to
  **X-as-a-Service** at whatever shared interfaces they
  have (API contracts, shared data schemas, shared
  auth). Fall back to **Collaboration** for bounded
  cross-cutting initiatives (a shared feature launch, a
  platform migration).
- Between the **enabling role** and the stream-aligned
  teams: **Facilitating**. The enabling engineer sits
  with a team for a sprint or two to land a capability,
  then rotates out.
- Between the **complicated-subsystem team** (if it
  exists) and the stream-aligned teams: **X-as-a-Service**
  at a versioned interface, always.

This is the org shape where the CTO first stops being
IC leader of every conversation. Each stream-aligned
team needs a **tech lead** (chapter 05); the enabling
role reports to the CTO directly (usually) until it
grows into a team; the two-team boundary is where
Conway's Law starts biting.

Two temptations to resist at fifteen:

- **Do not create a platform team yet.** A "platform
  team" at fifteen engineers has three engineers and a
  charter to build capabilities nobody has actually
  pulled from them. It is a solution looking for a
  problem, and the six months before it earns its keep
  are six months of stream-aligned throughput not
  shipped. Wait for the pull-signal at ~25.
- **Do not split along technical layers.** "Front-end
  team, back-end team" is a technical-layer split. It
  reproduces the layered architecture as an org chart
  and requires every feature to be coordinated across
  two teams. Split by product / customer stream so each
  team is end-to-end.

## Twenty-five engineers — the platform team starts to earn its keep

At twenty-five engineers, the topology grows into:

- **Three to five stream-aligned teams**, each 4-6
  engineers, each with a clear product / customer
  boundary and a tech lead or first-line EM.
- **One platform team** of 3-5 engineers, providing a
  set of self-service capabilities (a paved deployment
  path, a standard observability integration, a shared
  data-warehouse pipeline, a shared auth SDK, a shared
  feature-flag setup) that the stream-aligned teams
  *pull* from.
- **Optionally, one enabling team** of 1-3 engineers,
  specialising in a capability the stream-aligned teams
  need transferred (SRE, security, ML platform, data
  infra), separate from the platform team.
- **A complicated-subsystem team** if the product has
  one and the specialism is not covered by an existing
  team.

Twenty-five engineers is the threshold at which the
**platform team earns its keep**. Below that, the cost
of dedicating 3-5 engineers to platform work exceeds
the throughput multiplier the platform gives the
stream-aligned teams. Above that, the reverse: without
a dedicated platform team, every stream-aligned team
re-invents its own deployment / observability / data
plumbing, and the resulting inconsistency creates a
maintenance tax and an onboarding tax that eats more
than the platform team's headcount would.

The signal that the platform team is earning its keep is
**stream-aligned team engineers voluntarily adopting the
platform capabilities**. The signal that it is not is
the reverse — platform team publishing internal blog
posts about capabilities nobody is using. The remedy for
the latter is a serious conversation about whether the
platform team is solving a real problem, and about
which problem it should solve instead.

Interaction modes at twenty-five:

- **Stream-aligned ↔ stream-aligned**: **X-as-a-Service**
  at shared interfaces. **Collaboration** for bounded
  initiatives. Never permanent collaboration — that is
  Conway's Law biting.
- **Stream-aligned ↔ platform**: **X-as-a-Service** —
  the platform is consumed via SDKs, UIs, and
  self-serve interfaces, not via tickets to the platform
  team.
- **Stream-aligned ↔ enabling**: **Facilitating**, with
  an explicit disengagement condition ("we will sit
  with your team for one quarter and land the ML
  training pipeline, then rotate out").
- **Stream-aligned ↔ complicated-subsystem**:
  **X-as-a-Service** at a versioned interface, always.

## The Conway's Law lens

Conway's Law says that a system's architecture inevitably
mirrors the communication structure of the organisation
that produces it (Conway 1968 — [melconway.com/Home/Committees_Paper.html](https://www.melconway.com/Home/Committees_Paper.html)).
The *Team Topologies* corollary — sometimes called the
**inverse Conway manoeuvre** — is that you can use this
to your advantage: **design the team topology to match
the architecture you want**, and the architecture will
follow.

Concretely at each stage:

- **At 5** — one stream-aligned team producing a
  well-modularised monolith (see [`mod-102` chapter
  05](../mod-102-architecture-under-uncertainty/05-monolith-modular-monolith-services-and-cap.md)).
- **At 15** — two stream-aligned teams producing two
  modules with a clear internal interface (a modular
  monolith with two well-defined slices, or an early
  services split at the seam the org boundary is at).
- **At 25** — 3-5 stream-aligned teams producing 3-5
  well-defined services (or 3-5 slices of a well-
  modularised monolith), and a platform team producing
  the shared substrate underneath.

If the architecture the team is producing at 25 doesn't
look like what the topology predicts — for example the
platform team is producing a set of capabilities nobody
is using, and the stream-aligned teams are each running
their own parallel infrastructure — the topology is
wrong, not the architecture. Fix the topology first.

## The **complicated-subsystem** exception at AI-native startups

An AI-native startup with a specific ML pipeline as its
moat (the "domain ML pipeline — Build" row from
[`mod-103` chapter 01](../mod-103-build-vs-buy-and-platform-economics/01-build-vs-buy-as-portfolio-decision.md))
often creates a **complicated-subsystem team** before
it creates a platform team — sometimes at 10-15
engineers. That is correct: the complicated subsystem is
the product's differentiator, and its specialism cannot
be spread across every stream-aligned team.

The interaction mode with that team is **X-as-a-Service**
at a versioned interface — the ranker, the training
pipeline, the fine-tuning harness — and the stream-
aligned teams consume it without having to become
ML-platform engineers themselves. This is exactly the
pattern the book describes for complicated-subsystem
teams, and the pattern that [`ai-infra-ml-platform`](../../../ai-infra-ml-platform-learning)
(level 30) is the peer-track owner for at scale.

## Failure modes

- **The premature platform team.** A platform team
  before 20-25 engineers pulls throughput away from
  stream-aligned teams without a compensating
  multiplier. Fix: wait for the pull-signal from
  stream-aligned teams; solve platform needs as
  *one engineer's shared responsibility* until then.
- **The technical-layer split.** Front-end team,
  back-end team, mobile team, data team — a set of
  teams organised around technology instead of streams.
  Every feature is a three-team hand-off. Fix: split
  along product / customer streams; the front-end and
  back-end engineers are on the same stream-aligned
  team.
- **The permanent enabling team.** An enabling team
  that was set up to help two stream-aligned teams
  learn observability, still exists two years later,
  and now owns observability *permanently*. That is a
  platform team masquerading as an enabling team. Fix:
  either transfer the capability out and disband, or
  formally re-charter as a platform team with a
  self-service surface.
- **The Collaboration-as-default topology.** Every team
  is in a permanent collaboration with every other
  team. Meetings dominate. Fix: name the interaction
  mode explicitly per team-pair. Where the interface is
  stable, downgrade Collaboration to X-as-a-Service.
- **The un-owned system.** A system in production that
  no team owns. Every incident on it defaults to
  whoever last touched it. Fix: name an owning team,
  even if it is nominally-owned by a stream-aligned team
  as a temporary tenancy. Un-ownership is the failure
  mode incidents amplify.

## Summary

- The **four team types** from Skelton and Pais's *Team
  Topologies*
  ([teamtopologies.com/book](https://teamtopologies.com/book))
  — stream-aligned, platform, enabling, complicated-
  subsystem — plus the **three interaction modes** —
  Collaboration, X-as-a-Service, Facilitating — are
  the vocabulary the CTO reasons about org shape with.
- At **5 engineers** the topology is **one
  stream-aligned team**; no platform team, no enabling
  team, no complicated-subsystem team unless the
  product has one.
- At **15 engineers** the topology is **two
  stream-aligned teams plus an enabling role or
  partial-team**; still no permanent platform team;
  split along product / customer streams, not
  technical layers.
- At **25 engineers** the topology adds a **platform
  team** that starts to earn its keep by giving
  stream-aligned teams a self-service substrate they
  voluntarily adopt; interaction between platform and
  stream-aligned teams is **X-as-a-Service**.
- **Conway's Law** (Conway 1968 —
  [melconway.com/Home/Committees_Paper.html](https://www.melconway.com/Home/Committees_Paper.html))
  means the architecture will follow the topology; use
  the **inverse Conway manoeuvre** to design the
  topology for the architecture you want.
- Failure modes: premature platform team, technical-
  layer split, permanent-enabling-team, Collaboration-
  as-default, un-owned systems.

The chapter's paired exercise —
[`exercise-04-team-topologies-mapping-for-three-stages.md`](exercises/exercise-04-team-topologies-mapping-for-three-stages.md)
— walks the drawing of the 5 / 15 / 25 topology for your
(or a real reference) startup, with interaction modes
labelled per team-pair. Chapter 05 covers the
promote-vs-hire decisions the topology triggers (first
EM, first tech lead, first VP Eng); chapter 06 covers
the org chart / career-ladder / comp-band artifacts the
topology commits to on paper. The 25 → 50 → 150
transitions live in [`mod-106`](../mod-106-scaling-org-and-stack/README.md).
