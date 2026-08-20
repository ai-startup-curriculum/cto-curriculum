# Spikes with Kill Criteria — Risk-Reduction under Uncertainty

> The Extreme Programming spike-solutions page
> ([extremeprogramming.org/rules/spike.html](http://www.extremeprogramming.org/rules/spike.html))
> names the pattern: a small, focused program written to
> answer a question or explore a technical risk, not to
> ship product. In this module, that "small, focused
> program" is paired with an explicit kill criterion.

## Motivation

Not every architectural decision is ready to be an ADR. Some
of the most consequential decisions the seed-stage CTO faces
cannot honestly be written as an ADR yet, because the team
does not have enough information to name the trade-off. The
question is real, the choice matters, but the *evidence
required to choose* does not exist inside the team's current
understanding.

Two failure modes are common in this situation:

- **Deciding without evidence.** The CTO picks the option
  that feels right, writes an ADR that reads well, and
  discovers three months later that the assumed constraint
  ("Postgres full-text search will scale to our workload")
  was wrong. The ADR is superseded under crisis pressure
  rather than as a planned iteration.
- **Deciding by argument until the deadline forces a
  decision.** The team spends four weeks debating the
  choice in Slack and in whiteboard sessions. No new
  evidence enters the conversation because no one is
  running the experiment that would generate it. Eventually
  a customer commitment forces the decision and it is made
  by the loudest voice in the room.

The **spike** — a time-boxed, evidence-generating experiment
with an explicit kill criterion — is the mechanism that
avoids both. The vocabulary comes from the Extreme Programming
tradition — the reference definition is at
[extremeprogramming.org/rules/spike.html](http://www.extremeprogramming.org/rules/spike.html)
and is expanded in Kent Beck's *Extreme Programming
Explained*. The term is now widely used across agile / lean
vocabularies.

Some teams write "prototype" or "PoC" and mean the same
thing. The term matters less than the discipline: a spike is
a **finite-duration experiment** with a **question it exists
to answer** and a **kill criterion** that says when the
answer is "no".

## The shape of a well-formed spike charter

A spike charter is a one-page document. It has six sections;
they can be a template in the same `docs/architecture/`
directory the C4 diagrams and ADRs live in (chapters 02 and
03).

### 1. Question

One sentence, ending in a question mark, that the spike
exists to answer.

- Good: "Can Postgres `tsvector` full-text search meet our
  p95 latency SLO (< 200ms) at 1M product records with
  faceted filtering?"
- Bad: "Investigate search". This is not a question; it is
  a task assignment. A team can spend an unbounded amount
  of time on "investigate search" and never converge.

The test: at the end of the spike, can you answer the
question with "yes / no / and here is the specific
condition"?

### 2. Decision it unblocks

Which ADR is waiting for the spike's answer. This anchors
the spike in a real strategic decision rather than in
open-ended curiosity.

- Good: "Unblocks ADR-000X (add Meilisearch as a
  read-replica search index) — if the spike's answer is
  yes, we do not need Meilisearch this quarter and the
  ADR is not opened."
- Bad: "Might be useful later". A spike that unblocks no
  decision is not a spike; it is a personal-interest
  project. Kill it, or at least separate it from the
  spike lane.

### 3. Success criterion

The specific evidence that would let the ADR be written in
one direction — usually the "keep the simpler option"
direction.

- Good: "p95 latency ≤ 200ms measured on a representative
  1M-row synthetic dataset with the two most common query
  shapes, on the current RDS instance class, over a
  10-minute sustained load."
- Bad: "The performance is acceptable". Whose acceptance?
  Measured how? On what data?

### 4. Kill criterion

The specific evidence that would end the spike early — either
because the answer is clearly no, or because the spike is
clearly not going to reach a definitive answer inside its
time-box.

- Good: "Any of the following ends the spike: (a) p95
  latency > 500ms at 500k rows, (b) any single query
  timing out beyond 5s, (c) the required Postgres
  configuration exceeds the current instance class's
  memory limit."
- Good: "Two full days elapsed without a benchmark harness
  in place." (This is a *process* kill criterion — spikes
  that cannot start the experiment within a certain
  fraction of the time-box almost never converge.)

The kill criterion is the load-bearing part. A spike
without one is a research project.

### 5. Time-box

How long the spike is authorised to run. Concrete duration,
in engineer-days.

- Good: "3 engineer-days, elapsed inside the current
  sprint." Or "1 engineer-week, elapsed by 2026-03-15."
- Bad: "Until it's done." Spikes must have a *before* time
  and an *after* time; otherwise they are architecture-
  team research, not risk reduction.

Time-box discipline is what makes the spike cheaper than
the alternative (arguing indefinitely without evidence).
The industry rule of thumb is that a spike should be at
most 5-10% of the estimated cost of the work it de-risks;
above that ratio, the spike is competing with the work
itself for calendar.

### 6. Deliverable

What the spike leaves behind so that the answer is
inspectable. Usually one or more of:

- A short **spike report** (2-3 pages, in
  `docs/architecture/spikes/`) with the question, the
  method, the evidence collected, and the recommendation.
- A **benchmark harness** in the repo, runnable by
  anyone, so the measurement can be re-run when the
  context changes.
- A **thrown-away prototype branch** with a `SPIKE-` prefix
  in the branch name, so the reader can inspect the code
  without it being interpretable as production-ready.

The deliverable is *not* production code that has to be
kept. XP is explicit: spike code is discarded, and the
production implementation is built from scratch with the
knowledge the spike produced. Keeping spike code as
production code is a common failure mode that turns the
spike into a rewrite-under-pressure. If the spike code is
so clearly right that you want to keep it, open a
follow-up story — do not let the spike leak into
production silently.

## Where spikes fit in the decision workflow

Spikes are one of three things a decision can be doing at
any moment:

- **ADR (chapter 02)** — the decision is ready; the
  trade-off is nameable; the choice is defensible against
  the current stage.
- **Spike (this chapter)** — the decision is not ready
  because a specific piece of evidence is missing; the
  spike is the experiment that would produce it.
- **Deferred** — the decision is not currently pressing;
  the team has bigger things to work on; the decision will
  be picked up when the pressure arrives. Deferrals should
  themselves be written down (a short "we are deliberately
  not deciding this yet, and here is what would force us
  to" note in the ADR index).

The pathological state is a decision that is neither an
ADR nor a spike nor a deferral — a decision the team is
arguing about, week after week, with no experiment planned
and no time-box in place. That state consumes calendar,
morale, and eventually customer commitments, without
producing evidence.

## Choosing when to spike

Not every uncertainty is worth a spike. Two properties
qualify a decision for the spike lane:

- **The cost of being wrong is high.** The decision is
  hard to reverse — a persistence-store choice, a
  frontend framework, a build-vs-buy call on a
  cross-cutting vendor. If the wrong answer only costs a
  Friday-afternoon refactor, an ADR based on best current
  understanding is cheaper than a spike.
- **The evidence is cheap to generate.** A benchmark
  harness for search performance takes 3 days; a spike
  for "will our product-market fit hold in this vertical"
  takes 6 months. The former is a spike; the latter is a
  strategy question that lives outside the CTO's decision
  lane and belongs in the CEO / CPO conversation.

The two properties together define the *shape* of a
spike-worthy question: a load-bearing architectural
decision where a bounded experiment can produce the
evidence that would let the ADR be written in one
direction.

## Kill discipline

The kill criterion is where the spike discipline stands or
falls. Two rules:

- **The kill criterion is agreed *before* the spike
  starts.** Once the spike is running, sunk-cost bias
  will push the team to keep going past the point where
  the answer is already no. The pre-committed kill
  criterion is the only defence.
- **When the kill criterion fires, the spike is killed
  the same day.** Not "let's give it another day"; not
  "let's try one more configuration". The kill criterion
  fired; the answer is no; the ADR is written in the
  other direction (or a follow-up spike is chartered
  with a different question).

The team that consistently kills spikes when the kill
criterion fires learns to trust the spike discipline.
The team that pushes past the kill criterion "just one
more day" trains itself out of the discipline; the
next spike will have no kill criterion because the
team knows kill criteria are theatre.

## Deferring up to senior / principal architect

Some open architectural questions are above the pre-seed /
seed CTO's scope. A spike will not converge inside the
CTO's calendar, and the correct move is to defer the
question up rather than run a spike.

- **Depth beyond a bounded experiment.** Questions where
  the evidence requires weeks of a senior specialist's
  time (multi-region failover topology; a real
  consensus-protocol comparison; a serious multi-tenant
  isolation design) are not spikes. Defer up to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) or
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55).
- **Depth requiring on-call operational experience the
  team does not have.** If nobody on the team has run the
  proposed technology in production, the spike will
  produce a working prototype and no operational
  intuition. Bring in a technical advisor or a specialist
  contractor; hire the depth if the decision is
  load-bearing enough. See mod-104 on the
  hire-vs-contractor decision.

The seed-stage CTO's job on these deferrals is to name
them explicitly in the ADR index — "deferred up to
architect-level scope, gate: this hire" — rather than
having them silently drift into "we'll figure it out
later" state.

## Concrete example: the "can we skip Kubernetes?" spike

To make the shape concrete, walk a well-formed spike
charter that many seed-stage CTOs would recognise.

```markdown
# SPIKE-0002 — Can we run our workload on Fly.io Machines?

Date: 2026-02-20
Time-box: 3 engineer-days, elapsed by 2026-02-28

## Question

Can our current backend workload — a Django app, a Celery
worker, and a scheduled beat process — run on Fly.io
Machines with acceptable operational ergonomics and cost,
so that we can defer adopting Kubernetes for the first year?

## Decision it unblocks

Unblocks ADR-0004 (deploy target). If the spike's answer
is yes, ADR-0004 chooses Fly.io Machines and we do not
adopt Kubernetes this year. If no, ADR-0004 chooses
managed Kubernetes (EKS / GKE) instead.

## Success criterion

All of:
- Deploy the current app + worker + beat to a Fly staging
  environment.
- End-to-end request latency at current staging load is
  within 20% of current production.
- Deploy-and-rollback works within 5 minutes end-to-end.
- Monthly cost estimate at current traffic profile is
  within 30% of current AWS spend.

## Kill criterion

Any of:
- Fly Machines cannot host the beat process without a
  workaround that adds operational surface area we would
  not accept.
- Deploy-and-rollback exceeds 15 minutes with no clear
  fix.
- Any critical production feature (background jobs,
  scheduled jobs, request-scoped auth) does not have a
  clean path on the platform.
- 1.5 elapsed days pass without a working staging
  environment.

## Deliverable

- Spike report at `docs/architecture/spikes/SPIKE-0002-fly-io.md`
  with question, method, evidence, recommendation.
- Throwaway spike branch `spike/fly-io-poc`.
- Cost estimate spreadsheet.

## Owner

CTO. Time-box overlaps with the ADR-0004 authoring lane;
if the spike is killed, ADR-0004 defaults to managed
Kubernetes with a note that the alternative was ruled out
by SPIKE-0002.
```

Note the shape: one question, one decision the answer
unblocks, concrete success and kill criteria, a
time-box, and an owner. The spike is authorised because
the ADR needs the evidence; the spike is bounded because
the ADR is on the roadmap.

## Common failure modes

- **The unbounded spike.** Time-box unspecified or
  quietly extended. Fix: enforce the time-box at the
  charter level and treat "we need another day"
  requests as re-charters that require re-authorisation.
- **The absent kill criterion.** Only a success criterion
  is defined; the spike keeps running until it succeeds
  or the CTO tires of it. Fix: refuse to authorise
  charters without a kill criterion. If the team cannot
  articulate the kill criterion, the question is not
  spike-shaped.
- **The keep-the-spike-code failure mode.** The spike
  succeeds; someone merges the spike branch into main
  because "it works". The prototype becomes production
  under load-bearing conditions it was never designed
  for. Fix: an explicit rule in the spike template that
  the code is thrown away, and a production implementation
  built from scratch informed by the spike report.
- **The disguised strategy question.** A "spike" that is
  really "should we pivot our product to a different
  vertical" and is going to run for two quarters. Fix:
  spikes are for architectural questions with a bounded
  experiment; strategy questions belong in the CEO /
  CPO conversation.
- **The spike-that-should-have-been-a-hire.** The team
  runs a series of spikes on multi-region failover for
  three months, all inconclusive. Fix: recognise that
  the depth required is above the seed-stage CTO's
  scope; defer up (see above) or bring in the depth.

## Summary

- Spikes are the primary risk-reduction mechanism when an
  architectural decision is not yet writable as an ADR.
  Vocabulary comes from Extreme Programming; the
  discipline is now standard across agile practices.
- A well-formed spike charter has six sections: **Question
  / Decision unblocked / Success criterion / Kill
  criterion / Time-box / Deliverable**.
- The **kill criterion** is load-bearing. Agree it
  *before* the spike starts and kill the spike the same
  day the criterion fires. Teams that push past the kill
  criterion train themselves out of the discipline.
- Spikes are *not* the same as prototypes-that-become-
  production. Spike code is thrown away; the production
  implementation is built from scratch with the knowledge
  the spike produced.
- Questions that require depth beyond a bounded experiment
  are not spike-shaped; defer them up to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  (level 45) or
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
  (level 55), or bring in the depth via hire /
  contractor.

The chapter's paired exercise —
[`exercise-06-spike-charter-and-kill-criteria.md`](exercises/exercise-06-spike-charter-and-kill-criteria.md)
— walks the authoring of a one-page spike charter for a
real open architectural question, including the kill
criterion. Chapter 05's staged extraction decision and
chapter 04's trade-off map are the two most common
sources of spike-worthy questions.
