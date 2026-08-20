# Reading the ThoughtWorks Technology Radar and the CNCF Landscape as References

> The ThoughtWorks Technology Radar and the CNCF Landscape
> are the two most-cited industry reference artifacts for
> technology choice at the seed-to-Series-A stage. Both are
> useful. Neither is an adopt-list. The seed-stage CTO reads
> them the way an investor reads a market map — as a
> vocabulary and an orientation, not as a recommendation to
> shop from.

## Motivation

Two artifacts show up repeatedly in seed-stage technology
conversations:

- **The ThoughtWorks Technology Radar**
  ([thoughtworks.com/radar](https://www.thoughtworks.com/en-us/radar)) —
  a twice-yearly report grouping *techniques*, *platforms*,
  *tools*, and *languages & frameworks* onto four rings
  (**Adopt**, **Trial**, **Assess**, **Hold**), authored by
  a rotating group of ThoughtWorks senior technologists
  based on the projects the firm is running that quarter.
- **The CNCF Landscape**
  ([landscape.cncf.io](https://landscape.cncf.io/)) — a
  visual map of the projects and vendors in the cloud-
  native ecosystem, maintained by the Cloud Native Computing
  Foundation, categorised by function (orchestration &
  scheduling, service proxy, security & compliance,
  observability, database, streaming, and so on) and
  annotated with each project's CNCF status (**Graduated**,
  **Incubating**, **Sandbox**) or vendor / member
  affiliation.

Both are excellent reference material. Both are also
regularly mis-used in ways that undermine the actual
decision the CTO is trying to make.

- The Radar is read as a shopping list: "we should adopt
  everything in the Adopt ring". It isn't — the Radar is
  ThoughtWorks's opinion about what their consultants are
  seeing work on their consulting engagements, and
  ThoughtWorks's project mix is not your startup's product.
- The Landscape is read as a marketing exercise: "our
  competitor's logo is in the Landscape and ours isn't, so
  we should submit". It isn't a marketing exercise; it's a
  functional map. Being *in* the Landscape doesn't validate
  a project, and being *not in* the Landscape doesn't
  invalidate one.

The rest of this chapter is how to read both artifacts as
what they are — a vocabulary, a functional map, and a
starting point for the actual selection work that lives in
chapter 06's scorecard.

## The ThoughtWorks Technology Radar — how to read it

### The rings

ThoughtWorks publishes their own definitions of the rings
([thoughtworks.com/radar/faq](https://www.thoughtworks.com/en-us/radar/faq)),
but the shape is:

- **Adopt** — "we feel strongly that the industry should be
  adopting these items." ThoughtWorks is putting the item
  into production on client engagements without reservation.
- **Trial** — "worth pursuing. Important to understand how
  to build up this capability." ThoughtWorks is using the
  item on client engagements, expects it to be a strong
  candidate for Adopt in future editions.
- **Assess** — "worth exploring with the goal of
  understanding how it will affect your enterprise."
  ThoughtWorks is watching and experimenting, not yet
  putting it in production.
- **Hold** — "proceed with caution." ThoughtWorks has
  observed problems with the item in practice.

The load-bearing thing to understand about the rings: **they
are not a maturity ladder**. An item does not need to
progress Assess → Trial → Adopt over successive editions to
be worthwhile. A project can jump straight to Adopt (it
suits ThoughtWorks's engagements well) or drop straight to
Hold (a failure mode has emerged).

### The blips

Each ring contains *blips* — individual items in the four
categories (techniques, platforms, tools, languages &
frameworks). A blip can move ring-to-ring between editions,
stay in place ("no change"), or drop off entirely (implicitly
"still recommend, no update this edition"). The Radar
publishes each edition's blip diff — read the diffs, not
just the current snapshot, to understand how the industry
opinion is *moving*.

### What the Radar is actually useful for at seed

The Radar is useful for the seed-stage CTO in three narrow
ways:

- **Vocabulary hygiene.** If your team is arguing about
  service mesh, event sourcing, feature flags, or
  documentation-as-code, the Radar's blip on that item is
  a shared, dated, one-paragraph reference that grounds the
  discussion in current industry practice. Cite the Radar
  in the ADR context section
  ([`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/02-adrs-the-primary-strategy-artifact.md))
  as one data point.
- **Weak signal on abandonment.** A tool your team is
  considering that shows up in Hold — with a specific
  reason — is a signal worth paying attention to, even if
  you decide to use the tool anyway. The Hold explanation
  is often the failure mode you would otherwise discover
  the hard way.
- **Discovery.** Blips in the Assess and Trial rings are
  often the earliest widely-cited industry note on a
  category that will matter in a year. Reading the Radar
  regularly is a cheap way to be aware of the direction
  the ecosystem is moving before it is urgent.

### What the Radar is not useful for

- **A shopping list.** "Everything in Adopt is a good
  choice for us" is not a defensible statement. The Radar
  is ThoughtWorks's context, not yours.
- **Vendor selection within a category.** The Radar has
  opinions on techniques and platforms; it does not run
  a per-vendor comparison of the sort chapter 06's
  scorecard is designed for. When the Radar says "adopt
  feature-flagging" it is not saying "adopt LaunchDarkly
  over GrowthBook".
- **A substitute for reading primary sources.** The Radar
  is a well-curated pointer to primary sources, not a
  substitute for them. Follow the blip's link, read the
  underlying paper or documentation, form your own view.

### The three-line test

A useful discipline: **when you cite the Radar in an ADR,
you should be able to write three lines explaining (1) which
edition the citation is from, (2) which ring the blip was
in, and (3) *why the Radar's reasoning applies to your
situation*.** If you cannot write the third line, the
citation is aesthetic and should come out.

## The CNCF Landscape — how to read it

### What the Landscape actually is

The Landscape ([landscape.cncf.io](https://landscape.cncf.io/))
is a visual, filterable, live-updated map of the cloud-native
ecosystem — projects, vendors, and standards — grouped by
function into categories such as *application definition &
image build*, *orchestration & scheduling*, *service proxy*,
*service mesh*, *observability*, *storage*, *database*,
*streaming & messaging*, *security & compliance*, and so on.

Two properties of the Landscape are load-bearing:

- **Inclusion is not endorsement.** A project or vendor is
  in the Landscape if they meet the Landscape's inclusion
  criteria ([landscape.cncf.io/about](https://landscape.cncf.io/about))
  — cloud-native, open-source (or, for members,
  cloud-native and CNCF-affiliated), meeting basic
  metadata quality. Inclusion does not mean CNCF has
  chosen or blessed the project.
- **The CNCF-project status ring is the endorsement layer.**
  Projects that have been contributed to the CNCF as
  Foundation projects go through a maturity ladder:
  **Sandbox** (early stage, hosted for community growth),
  **Incubating** (established adoption, governance, and
  contribution activity), **Graduated** (mature, widely
  deployed, meets the CNCF's graduation criteria at
  [github.com/cncf/toc/blob/main/process/graduation_criteria.md](https://github.com/cncf/toc/blob/main/process/graduation_criteria.md)).

Kubernetes ([kubernetes.io](https://kubernetes.io/)),
Prometheus ([prometheus.io](https://prometheus.io/)),
Envoy ([envoyproxy.io](https://www.envoyproxy.io/)),
Fluentd ([fluentd.org](https://www.fluentd.org/)),
containerd ([containerd.io](https://containerd.io/)),
Helm ([helm.sh](https://helm.sh/)), and Argo
([argoproj.github.io](https://argoproj.github.io/)) are
among the CNCF's Graduated projects — the canonical list
lives at [cncf.io/projects](https://www.cncf.io/projects/)
and is the authoritative source.

### What the Landscape is actually useful for at seed

- **Functional discovery.** "What are the options in the
  observability category?" or "what does a modern service-
  proxy category look like?" — the Landscape's category
  view is the fastest way to see the ecosystem at a
  glance.
- **Graduation status as a *risk signal, not a
  correctness signal*.** A Graduated project has cleared
  the CNCF's governance and adoption bar — non-trivial
  contributor base, security process, published cadence.
  For a load-bearing infrastructure dependency at seed,
  preferring a Graduated project over a Sandbox project of
  otherwise similar function is a sensible bias. It is not
  a promise of fitness for your use case.
- **A map of what "vendor-neutral" looks like in a
  category.** The Landscape distinguishes CNCF projects
  from member companies from non-member vendors, which
  helps the CTO see whether a category is anchored by a
  vendor-neutral standard or dominated by a specific
  vendor.

### What the Landscape is not useful for

- **A "best of" list within a category.** Two projects in
  the same category with the same CNCF status can be very
  different in maturity, adoption, and fitness. The
  Landscape does not rank within categories.
- **A completeness guarantee.** The Landscape does not
  include every project in the ecosystem — SaaS-first
  vendors, projects outside the cloud-native umbrella, and
  new entrants are often absent. Absence is not evidence
  of failure.
- **A CNCF endorsement of member companies.** Member
  companies pay to be members. Membership is a signal of
  commitment to cloud-native, not an endorsement of any
  specific product they sell.

### The graduation-status filter

A pragmatic seed-stage bias: for any load-bearing
infrastructure component you will operate yourself, **prefer
CNCF Graduated (or comparable-maturity OSS Foundation)
projects over Sandbox-tier projects unless you have a
specific reason to accept the maturity delta**. The
graduation criteria — number of independent contributors,
production adopters, published security process, governance
model — are exactly the properties that predict whether the
project will still be receiving critical bug fixes in three
years. See the CNCF graduation criteria
([github.com/cncf/toc/blob/main/process/graduation_criteria.md](https://github.com/cncf/toc/blob/main/process/graduation_criteria.md))
for the specifics.

Adjacent foundations to check for maturity signal:

- **Apache Software Foundation** —
  [apache.org](https://apache.org/) — has its own
  incubator → top-level-project ladder. Apache Kafka,
  Apache Iceberg, Apache Airflow, Apache Spark, Apache
  Superset are all top-level projects with similar
  maturity signal to CNCF Graduated.
- **Linux Foundation** family
  ([linuxfoundation.org](https://www.linuxfoundation.org/)) —
  parent of CNCF, plus many adjacent foundations (LF AI &
  Data, OpenSSF for supply chain, etc.).
- **OpenJS Foundation** — [openjsf.org](https://openjsf.org/)
  — the JavaScript ecosystem's equivalent, hosting Node.js,
  Express, jQuery, and others.

## When neither reference is enough

Both the Radar and the Landscape are pointers, not answers.
The actual choice — WorkOS vs. Auth0 vs. Keycloak, Datadog
vs. Grafana Cloud vs. self-hosted Prometheus, BigQuery vs.
Snowflake vs. Redshift — is chapter 06 territory. The
scorecard is the artifact that resolves the choice by naming
your specific criteria, weighting them, and forcing the
comparison against those criteria rather than against
industry-in-general.

A useful sequence:

- **Use the Landscape to enumerate the category.** "What
  options exist for feature flags with an OSS fallback?"
  — the Landscape's Application Definition & Development
  category, plus a quick search of feature-flag OSS
  outside the Landscape, gives you the option set.
- **Use the Radar to spot signals on the specific options.**
  "Has the Radar flagged any of these in Hold, or moved
  any into Adopt this edition?" A five-minute filter.
- **Then run the scorecard** (chapter 06) against your
  weighted criteria to pick the option and record the ADR.

## Concrete example: the "the Radar says adopt" ADR failure

An ADR that reads "we chose $VENDOR because the ThoughtWorks
Technology Radar has it in Adopt" is a failing ADR. The Radar
citation is a data point, not the argument. The reader —
future engineering hire, technical due-diligence reviewer —
cannot re-derive the trade-off from that sentence.

A stronger form of the same citation:

> The 2025 volume 32 Radar
> ([thoughtworks.com/radar](https://www.thoughtworks.com/en-us/radar))
> has "OpenTelemetry" in Adopt with the note that OTel has
> become the vendor-neutral instrumentation standard. This
> matches our own OSS-fallback criterion (chapter 06 of
> mod-103): we want the option to swap the observability
> backend later without re-instrumenting the application.
> The Radar citation is one input; the deciding factor is
> the swappability our scorecard weights heavily.

The specific edition, the specific note, and — critically —
*your own reasoning that consumes the citation* are all
present. The ADR now stands up to a reader who has never
heard of the Radar.

## Common failure modes

- **The shopping-list Radar read.** Adopting things because
  they are in Adopt, without checking whether the reasoning
  applies. Fix: apply the three-line test above.
- **Landscape-vs-fitness confusion.** Inferring that a
  project is a good choice from its presence in the
  Landscape. Fix: read the category, then evaluate the
  specific project against your scorecard criteria
  (chapter 06).
- **Status-inflation.** Treating Sandbox-tier projects as
  equivalent to Graduated projects for load-bearing
  infrastructure choices. Fix: use graduation status as a
  risk signal explicitly in the scorecard.
- **Stale-reference-set.** Building an ADR-in-2027 that
  cites the Radar from 2023 and the Landscape from a
  screenshot in someone's slide deck. Fix: cite the
  edition and the retrieval date; re-check on ADR
  supersession.
- **Absence-of-signal treated as negative signal.** A
  project that is not in the Landscape or on the Radar is
  not disqualified. The universe of software is much
  larger than either. Fix: use both as *sources of positive
  signal*, not filters against everything else.

## Adjacent industry references worth knowing

- **Gartner Magic Quadrant / Forrester Wave** — analyst
  quadrants aimed at enterprise buyers. Useful if the
  buyer segment you sell into cares about analyst
  positioning (mid-market and enterprise procurement
  processes often do). Both are paywalled; both are worth
  knowing exist even if you do not have direct access.
- **The State of DevOps Report** (formerly Puppet /
  DORA / Google Cloud) —
  [dora.dev/research/](https://dora.dev/research/) — the
  research the DORA four keys come from
  ([`mod-106`](../mod-106-scaling-org-and-stack/) picks
  this up as the delivery-performance measurement
  reference).
- **Stack Overflow Developer Survey** —
  [survey.stackoverflow.co](https://survey.stackoverflow.co/) —
  annual, developer-facing, useful as a lagging indicator
  of tool popularity across the practitioner community.
- **JetBrains State of Developer Ecosystem** —
  [jetbrains.com/lp/devecosystem](https://www.jetbrains.com/lp/devecosystem/) —
  another annual developer-facing survey; useful as a
  cross-check.

None of these is authoritative; all of them are useful as
one input in a well-cited ADR context section.

## Summary

- The **ThoughtWorks Technology Radar** is a twice-yearly
  ThoughtWorks-opinion snapshot on techniques, platforms,
  tools, and languages. The rings — **Adopt / Trial /
  Assess / Hold** — are not a shopping list; they are one
  data point, dated and context-bounded.
- The **CNCF Landscape** is a visual functional map of
  the cloud-native ecosystem. Inclusion is not
  endorsement; **the CNCF-project graduation status
  (Sandbox / Incubating / Graduated) is the endorsement
  layer**, and Graduated status is a useful risk signal
  for load-bearing infrastructure choices.
- Neither reference is a substitute for the
  vendor-selection scorecard (chapter 06). Use them to
  **enumerate the category** and **spot weak signals**,
  then run the scorecard against your own criteria.
- When you cite the Radar or the Landscape in an ADR,
  cite the **edition / retrieval date**, the **specific
  ring or status**, and — most importantly — **the
  reasoning that carries the citation into your specific
  situation** (the three-line test).

The chapter's paired exercise is embedded in chapter 06's
scorecard-authoring exercise
([`exercise-05-vendor-selection-scorecard-authoring.md`](exercises/exercise-05-vendor-selection-scorecard-authoring.md)),
which requires citing at least one Radar entry and one
Landscape category correctly in the ADR context section
that motivates the scorecard.
