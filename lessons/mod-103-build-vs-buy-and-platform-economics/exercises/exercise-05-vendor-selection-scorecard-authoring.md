# Exercise 05 — Vendor-Selection Scorecard Authoring

**Module:** `mod-103-build-vs-buy-and-platform-economics`
**Planned time:** ~2 hours
**Chapters this builds on:** [`06-vendor-selection-scorecard.md`](../06-vendor-selection-scorecard.md), with references from [`05-radar-and-cncf-landscape-as-references.md`](../05-radar-and-cncf-landscape-as-references.md)

## Problem statement

Author a full vendor-selection scorecard for **one real,
currently-open vendor decision** at your (or a real
reference) startup. Score 3-4 realistic options against
weighted criteria that include — non-negotiably — the
**switching-cost**, **vendor-trajectory-risk**, and
**OSS-fallback** columns from chapter 06. Land the choice
in an ADR that references the scorecard, and update the
corresponding row on your build-vs-buy matrix (exercise
01).

The point of the drill is to move from feature-matrix
comparison to *risk-adjusted* comparison — a scorecard
that a due-diligence reviewer, a lead investor, or a
future maintainer can read and either agree with or
disagree with *specifically* (rather than "why did you
pick that vendor?").

## Requirements

Produce a **scorecard file** (Markdown, in `docs/vendor-
scorecards/` or equivalent in your repo), an **ADR** that
consumes the scorecard, and an **updated matrix row**.

### Choosing the vendor decision

Pick a decision that is **currently open** or was
recently made at your (or a real reference) startup. The
decision must:

- Be from one of the "buy" rows of your build-vs-buy
  matrix (exercise 01).
- Have at least **3 realistic options** worth scoring —
  not a decision where the answer is over-determined (a
  Postgres-vs-MongoDB call at a Postgres-experienced
  team is not a real 3-option decision; a
  Datadog-vs-Grafana-Cloud-vs-self-hosted-Prometheus call
  usually is).
- Have material switching cost — a decision where
  moving off later would take at least a few
  engineer-weeks. Scorecards on trivially-swappable
  decisions are exercise-in-form; the value is on the
  sticky ones.

Suggested categories: identity, observability, data
warehouse, feature flags, foundation-model layer, CI/CD.

### The scorecard

Author it in the shape of the chapter-06 example. Minimum
structure:

- **Header** — vendor decision being scored, date, ADR
  link.
- **Weighted criteria** — 6-10 criteria, weights summing
  to 100%, with a paragraph under the table justifying
  the weights.
- **Threshold criteria** — separate list of any
  criteria that are filters (a vendor scoring below N on
  this criterion is *out*, regardless of the weighted
  total). Common examples: BAA availability for
  HIPAA-covered use, DPA availability for EU customers,
  data-residency in a specific region.
- **Options** — 3-4 realistic candidates. At minimum:
  the incumbent-of-mindshare in the category, the
  strongest alternative, and either a cloud-managed
  variant on your existing cloud *or* a self-hosted OSS
  variant.
- **Per-option scoring** — 1-5 on each criterion, with a
  one-line justification per cell. No un-justified cells;
  a score without a justification is opinion, not a
  scorecard.
- **The three non-negotiable columns.** Every scorecard
  must include:
  - **Switching cost** — engineer-quarters to move off,
    from the chapter-06 taxonomy (data migration,
    integration re-plumbing, compliance re-attestation,
    team re-training, customer-perceptible surface
    change).
  - **Vendor-trajectory risk** — 24-36 month horizon,
    with the signals from chapter 06 (acquisition
    exposure, pricing revision history, segment pivot
    risk, business collapse risk, product deprecation
    risk).
  - **OSS-fallback path** — score against how close the
    open-standard or open-source alternative is, using
    the chapter-06 examples (OIDC / Keycloak,
    OpenTelemetry / Grafana stack, OpenFeature /
    GrowthBook, Iceberg + Trino, Kubernetes, open-weight
    models + vLLM).

- **Weighted total** — per-option, computed.
- **Recommendation paragraph** — the option chosen and
  why the weighted total (plus any threshold-criteria
  filtering) supports it. If the top two options are
  within a small margin, name explicitly what tie-breaker
  decided the call.

### Radar / Landscape citation

Include at least one citation to either the ThoughtWorks
Technology Radar or the CNCF Landscape in the scorecard's
Context or criteria section, applied correctly per the
chapter-05 three-line test:

- The specific edition or retrieval date.
- The specific ring / status / category the citation is
  from.
- **Why the citation's reasoning applies to your
  situation** (this is the load-bearing sentence).

If neither the Radar nor the Landscape has a relevant
entry for your category, note that explicitly (this is
itself useful information).

### The ADR

Author (or update) the Nygard-format ADR that this
scorecard resolves. Requirements:

- **Title** — imperative, specific. "Use $VENDOR for
  $CAPABILITY".
- **Context** — links to the scorecard file, the
  build-vs-buy matrix row, and any other relevant ADRs.
- **Decision** — one paragraph, active voice.
- **Consequences** — Positive / Negative / Deferred,
  using ISO/IEC 25010 vocabulary where relevant. Name
  the lock-in accepted, the vendor-trajectory risk being
  underwritten, and the OSS-fallback path being reserved.
- **Reopening trigger** — the observable condition that
  would force the scorecard to be re-run.

### The matrix update

Update the corresponding row on your build-vs-buy matrix
(exercise 01) to reflect the scorecard's outcome. Add
(if absent) columns or annotations for switching cost and
OSS fallback, so the portfolio view is honest about
these dimensions across the matrix.

### The meta-question

After the scorecard, ADR, and matrix update, write
**200-400 words** answering:

- Which criterion was the **hardest to weight** — the
  one where you weren't sure whether to spend 10% or
  20% of the budget? Why?
- Did the weighted total tell you the answer, or was
  the answer over-determined by a threshold criterion
  (a BAA that only one option offers, a
  data-residency requirement that only one option
  serves)? If threshold-determined, was the scoring
  exercise still useful, and how?
- If you ran this same scorecard again in **12 months**,
  which criterion's weight would you expect to *change
  most* — and what stage transition or event would drive
  the reweight?

## Starter guidance

- **Do not fill in scores from vendor marketing.**
  Every vendor's website has a comparison chart showing
  they win. Score against your own criteria, sourcing
  from the vendors' docs, TOS, DPA, pricing pages, and
  status pages — not their comparison decks.
- **Weight before you score.** If you score first and
  weight afterwards, you will reverse-engineer weights
  that produce the answer you already preferred.
  Publish the weights (and reasoning) *first*, then
  score against them.
- **Publish the reasoning for the weights.** A
  scorecard whose weights sum to 100% but whose
  reasoning is invisible is a scorecard the reader
  can't disagree with specifically. One or two
  sentences per weight is enough.
- **Double your first switching-cost estimate.** The
  compliance re-attestation, team re-training, and
  customer-perceptible surface work will take longer
  than you first think. See chapter 06.
- **Be honest about vendor-trajectory risk.** If your
  chosen vendor was recently acquired, was recently
  through a licence change, or is materially outside
  your segment focus, name that in the score — don't
  round up because you already like the vendor.

## Acceptance criteria

Your scorecard bundle is complete when a reader (a
co-founder, a first engineering hire, a technical
advisor, a lead investor, a technical due-diligence
reviewer) can:

- Read the scorecard standalone and understand which
  vendor was chosen, against which weighted criteria,
  and *why the weighted total plus threshold criteria
  produced that answer*.
- Follow the ADR link to the durable one-page
  decision record and the matrix link to the portfolio
  view.
- Read the three non-negotiable columns (switching
  cost, vendor-trajectory risk, OSS fallback) and see
  that the CTO has reasoned about the *risk* of the
  choice, not just its features.
- Follow the Radar or CNCF Landscape citation and see
  that it is applied correctly (three-line test) —
  not treated as an authority.
- Read the reopening-trigger and know the specific
  condition under which the scorecard would be re-run.
- Read the meta-paragraph and see the CTO has
  identified where the reasoning is weakest and what
  future event would move the answer.

The output of this exercise closes out the artifact chain
for at least one vendor decision: matrix row → ADR →
scorecard. The scorecard is the artifact that turns the
matrix row from a portfolio note into a defensible
decision instrument. Together, the five exercises produce
the depth reference for the vendor-strategy strand of the
capstone
[`project-101`](../../../projects/project-101-first-year-technical-strategy-for-one-seed-startup)
first-year technical-strategy package.
