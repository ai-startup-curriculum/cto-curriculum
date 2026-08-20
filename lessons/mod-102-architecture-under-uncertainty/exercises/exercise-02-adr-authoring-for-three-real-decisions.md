# Exercise 02 — ADR Authoring for Three Real Decisions

**Module:** `mod-102-architecture-under-uncertainty`
**Planned time:** ~3 hours
**Chapter this builds on:** [`02-adrs-the-primary-strategy-artifact.md`](../02-adrs-the-primary-strategy-artifact.md)

## Problem statement

Author three Nygard-format Architecture Decision Records for
**real, currently-open** architectural decisions your (or a
real reference) startup faces this quarter. Put them in a
`docs/adr/` directory in a real (or scratch) repo. Each ADR
must stand up to the "quarter-of-engineering-work-to-undo"
test from chapter 02.

The point of the drill is not to write template artifacts. It
is to build the muscle of turning a currently-fuzzy
architectural thought into a versioned, defensible,
one-screen document that a future reader (an engineering
hire, a technical advisor, a due-diligence reviewer, or
you-six-months-from-now) can consume without asking a
follow-up question.

## Requirements

Produce **three ADRs** in Nygard's four-section format —
Status / Context / Decision / Consequences. Each ADR must
be:

- **One screen or less** (roughly 300-600 words, plus
  headings). If it is longer, edit it down.
- **Numbered and dated** — `0001-<slug>.md`,
  `0002-<slug>.md`, `0003-<slug>.md`.
- **Committed to a real repo** (your startup's, a scratch
  repo you create for the exercise, or a fork of a public
  reference — the constraint is that it is in git, not on
  a Google Doc).
- **Indexed** — a `docs/adr/README.md` with a one-line
  entry per ADR (title + status).

### The three decisions

Choose one from each bucket. **Do not choose three from the
same bucket** — the exercise is about breadth of decision
type, not depth of one class.

**Bucket A — starting-architecture decision.** Something in
the shape of "we will build a modular monolith first" or "we
will use Postgres as the primary transactional store". This
one should be closely coupled to your exercise-01 output.

- Example choices: primary persistence store; deploy target
  (Fly.io / Vercel / EKS / etc.); backend language +
  framework; the monolith / modular-monolith / services
  call from exercise 01.

**Bucket B — vendor / build-vs-buy decision.** Something in
the shape of "we will use $VENDOR for $CAPABILITY rather
than build it ourselves". This ADR is where the mod-103
material (which is the module after this one) starts to
land; authoring the ADR here lets mod-103 build on real
context.

- Example choices: auth (Clerk / WorkOS / Auth0 / Firebase
  Auth); payments (Stripe / Adyen); observability (Datadog
  / Honeycomb / Grafana Cloud); email (Postmark / SES);
  feature flags (LaunchDarkly / GrowthBook / self-hosted);
  foundation-model API (OpenAI / Anthropic / Bedrock /
  self-hosted).

**Bucket C — cross-cutting-concern decision.** Something in
the shape of "we will handle $CROSS_CUTTING_THING this way
across the codebase, and here is why". These are the ADRs
that most often go undocumented and then become the tribal
memory that new hires bounce off.

- Example choices: multi-tenancy model (silo / pool /
  bridge); release-vs-deploy strategy (feature flags,
  canary, blue-green); error taxonomy and observability
  contract; async-work substrate (Celery / Sidekiq / SQS /
  serverless functions); the API-versioning strategy
  (URL-versioned, header-versioned, none); the
  identity-and-permission model (RBAC / ABAC / relationship-
  based).

### For each ADR

- **Title** — imperative, descriptive, one line. "Use
  Postgres for the primary transactional data store." Not
  "Database". Not "How we chose the database".
- **Status** — `Accepted` for at least one of the three;
  `Proposed` is acceptable for the other two if the
  decision is genuinely still in review.
- **Context** — concrete, time-stamped, specific to your
  situation. Name at least three forces at play. If the
  section reads as if it could be copy-pasted onto another
  startup's ADR, it is not concrete enough.
- **Decision** — one paragraph, active voice, one choice.
- **Consequences** — grouped `Positive / Negative /
  Deferred`, using ISO/IEC 25010 vocabulary from chapter
  04 to name the quality-attribute trade-off. At least
  one *negative* consequence per ADR — an ADR with only
  positive consequences has not resolved the trade.

### Plus — the index

Author `docs/adr/README.md` with one line per ADR in the
form:

```
- [ADR-0001](0001-<slug>.md) — Use Postgres for primary transactional store — Accepted (2026-08-20)
- [ADR-0002](0002-<slug>.md) — Adopt Clerk for B2B auth — Proposed (2026-08-20)
- [ADR-0003](0003-<slug>.md) — Feature-flag every user-visible release — Accepted (2026-08-20)
```

### Then — the meta-question

After the three ADRs and the index, write a short (200-400
word) answer to the following:

- Of the three decisions you authored, which one felt
  hardest to write down? Was it because the decision itself
  was not yet resolved (in which case a **spike** — see
  chapter 06 and exercise 06 — is the right next artifact),
  or because you had never articulated the *trade-off* the
  decision was making (in which case chapter 04's ISO/IEC
  25010 vocabulary is what unblocks the writing)?
- Name the **next three ADRs** you would author over the
  coming quarter if this discipline were sustained, with
  a one-line reason each. This becomes your ADR backlog.

## Starter guidance

- Choose decisions that are **actually open at your
  startup** or would be open at a real reference startup
  you understand. Made-up ADRs read like made-up ADRs.
- The Nygard essay
  ([cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions))
  is short. Read it once before you start; re-read the
  Consequences section discussion before you edit each of
  your three ADRs.
- Consider using
  [`adr-tools`](https://github.com/npryce/adr-tools) — a
  single `brew install adr-tools` gets you `adr new
  "title"` which creates the numbered, dated, filled-in
  template. Not required, but the workflow is smooth.
- If you find yourself writing "TBD" in the Consequences
  section, the decision is not yet ADR-shaped. Convert it
  to a spike charter (exercise 06) instead of trying to
  force it.
- If two of your three ADRs are covering the same
  underlying decision at different levels of detail, they
  are one ADR — pick the level of detail your future
  reader needs and edit the other down or delete it.
- Reference the C4 diagrams from exercise 03 (or the
  diagrams you already have) — every ADR that changes the
  Container-level shape of the system should have a
  parallel diagram update in the same PR.

## Acceptance criteria

Your three ADRs are complete when a reader (a technical
advisor, a first engineering hire, a due-diligence reviewer
doing a first pass) can:

- Read each ADR standalone and understand *what was
  decided*, *why*, and *what the team is now living with*
  without asking a follow-up question.
- Read the index and see the current state of the three
  decisions at a glance.
- Reproduce the trade-off (which ISO/IEC 25010
  characteristics the decision optimises for and which it
  trades away) from the Consequences section.
- Identify at least one specific condition per ADR under
  which the decision would be superseded — that is, name
  the future state that would open the follow-up ADR.

The output of this exercise feeds directly into the
[lab-01 architecture package](../README.md#lab) once that
prompt is authored, and into mod-103 where the Bucket-B
ADR becomes the anchor for the vendor-selection scorecard
work.
