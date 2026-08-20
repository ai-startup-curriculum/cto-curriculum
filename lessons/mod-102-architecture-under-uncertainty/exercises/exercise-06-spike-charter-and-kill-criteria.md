# Exercise 06 — Spike Charter and Kill Criteria

**Module:** `mod-102-architecture-under-uncertainty`
**Planned time:** ~2 hours
**Chapter this builds on:** [`06-spikes-and-kill-criteria.md`](../06-spikes-and-kill-criteria.md)

## Problem statement

Author a **one-page spike charter** for a **real, currently-
open** architectural question at your (or a real reference)
startup — the kind of question that cannot honestly be
written as an ADR yet because a specific piece of evidence
is missing. Then negotiate the charter, at least mentally,
against the six sections from chapter 06 until each section
would stand up to a co-founder, a first engineering hire, or
a technical advisor pushing back on it.

The point of the drill is not to run the spike. It is to
build the muscle of *chartering the spike* — because the
kill criterion, the time-box, and the "which ADR does this
unblock" question are the parts most seed-stage teams skip
and then regret. The team that writes a well-formed spike
charter finds the answer in a bounded amount of calendar;
the team that skips the charter finds itself six weeks in,
still arguing.

## Requirements

Produce **one spike charter**, in Markdown, in the
`docs/architecture/spikes/` directory of a real (or scratch)
repo. The charter must have all six sections from chapter 06.

### The six sections

**1. Question.** One sentence, ending in a question mark,
that the spike exists to answer. If your first draft is not
a question, rewrite it until it is.

- Test: at the end of the spike, can the answer be stated
  as "yes / no / and here is the specific condition"? If
  not, the question is not spike-shaped.

**2. Decision it unblocks.** Which ADR (from exercise 02,
your ADR backlog, or a new open decision) is waiting for the
spike's answer. Cite the specific ADR by number or by title.

- If no ADR is waiting on the answer, the spike is a
  personal-interest project rather than a risk-reduction
  spike. Either move the ADR into your backlog first or
  reconsider whether this is spike-shaped work.

**3. Success criterion.** The specific evidence that would
let the ADR be written in one direction. Include:

- The measurement or observation itself — concrete,
  numeric where possible.
- The environment / dataset / configuration the
  measurement runs against — representative enough that a
  future reader trusts the number.
- Where the evidence lives at the end of the spike (the
  spike report, a benchmark harness, a screenshot in a
  branch's PR description).

**4. Kill criterion.** The specific evidence that would end
the spike early, either because the answer is clearly *no*
or because the spike is clearly not going to converge
inside its time-box. State at least **two** distinct
conditions:

- One or more **outcome-based** kill conditions — measured
  facts that would end the spike (a latency threshold
  breached, a required feature not supported, a cost
  ceiling exceeded).
- At least one **process-based** kill condition — the
  spike is not making progress even in setup terms (e.g.
  "1.5 elapsed days without a working staging
  environment"; "2 engineer-days with no benchmark
  running").

The kill criterion is the load-bearing section. If you
cannot articulate it, the question is not spike-shaped —
try to re-word the question so that a kill criterion
becomes obvious.

**5. Time-box.** Concrete duration in engineer-days /
engineer-weeks, and an absolute deadline. "3 engineer-days,
elapsed by 2026-09-05" — not "as long as it takes" and not
"until we know".

- Sanity check: the spike should cost roughly 5-10% of the
  work it de-risks. If the spike is longer than that, the
  spike is competing with the work for calendar; if the
  spike is much shorter, you may be under-scoping the
  question.

**6. Deliverable.** What the spike leaves behind so that the
answer is inspectable after the spike ends:

- A **spike report** (2-3 pages) in
  `docs/architecture/spikes/SPIKE-NNNN-<slug>.md`, with
  the question, method, evidence collected, and
  recommendation.
- A **throwaway spike branch** in git, prefixed `spike/`,
  containing the code that ran the experiment. State
  explicitly that this code is not to be merged; the
  production implementation is built from scratch informed
  by the report.
- Optionally, a **benchmark harness** or a **cost
  estimate spreadsheet** committed to the repo so the
  measurement can be re-run when the context changes.

### Plus — the owner and the review

Every spike charter names an **owner** (usually a single
engineer, sometimes the CTO themselves for load-bearing
decisions) and a **reviewer** (usually the CTO if the
owner is an engineer, or a co-founder / technical advisor
if the owner is the CTO). The reviewer's job is to hold
the owner accountable to the time-box and the kill
criterion.

### Then — the meta-question

After the charter, write a short (200-400 word) answer to:

- What would this decision look like if you *did not* spike
  it and instead wrote the ADR now, based on best current
  understanding? What is the specific worst-case cost of
  being wrong in that ADR? Compare that cost to the cost
  of running the spike. If the spike is more expensive
  than the worst case of being wrong, cancel the spike
  and write the ADR; if not, the spike is authorised.
- Is the question you are asking one that *any* bounded
  spike can answer, or is the depth required beyond a
  seed-stage CTO's scope? If the latter — usually a
  multi-region, multi-tenant, or high-scale
  distributed-systems question — name the higher-level
  track this defers up to (either
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  or
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning))
  and describe the depth-import mechanism (a hire, a
  contractor, a technical-advisor call). See chapter 06.

## Starter guidance

- Choose a question that is **actually open** at your
  company or the reference startup you are working
  against. "Can Postgres handle our workload?" is a real
  spike question if you have a specific workload. "Should
  we use SQL or NoSQL?" is not; that is a strategy
  discussion that becomes an ADR when the workload is
  specified.
- Read the Extreme Programming spike glossary entry
  ([extremeprogramming.org/rules/spike.html](http://www.extremeprogramming.org/rules/spike.html))
  once before you start — the definition is short and
  worth having in your head.
- Do not skip the kill criterion because it is the hardest
  section. It is the hardest section *because* it is the
  most useful; teams that consistently pre-commit kill
  criteria find that their spikes converge; teams that
  don't find that they don't.
- If your question is really "should we adopt Kubernetes?"
  and your kill criterion is really "the CTO changes their
  mind" — the question is a strategy question, not a spike.
  Convert it to an ADR or defer.
- Sanity check the time-box against the calendar. A spike
  authorised for 3 engineer-days that is planned across
  three engineers over 4 elapsed weeks (each doing 1
  afternoon) almost never converges. Prefer a single
  engineer on a compressed elapsed schedule.
- If the spike unblocks a decision on multi-region,
  multi-tenant, or distributed-consensus architecture,
  reconsider whether the question is even spike-shaped —
  the depth required often exceeds the pre-seed / seed
  CTO's scope (see chapter 06's deferring-up section).

## Acceptance criteria

Your spike charter is complete when a reader (the owner, a
reviewer, the CEO watching runway) can:

- Read the Question section and understand exactly what
  will be answered by the end of the spike.
- Read the Decision it unblocks section and see the
  concrete ADR the answer feeds.
- Read the Success and Kill criteria and know the exact
  conditions under which the spike ends — with either
  answer state definitive.
- Read the Time-box and know exactly when the spike ends
  in calendar terms.
- Read the Deliverable section and see what artifacts will
  exist after the spike is over.
- Identify the owner and reviewer without ambiguity.

The output of this exercise is one artifact; the more
important output is the muscle of *chartering* the spike,
which the CTO will reach for many times over the first
year. The paired [lab-01](../README.md#lab) architecture
package includes the current open spike charters
alongside the ADRs and diagrams; this exercise's output
seeds that section.
