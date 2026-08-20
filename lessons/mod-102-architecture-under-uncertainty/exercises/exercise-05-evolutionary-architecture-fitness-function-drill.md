# Exercise 05 — Evolutionary-Architecture Fitness-Function Drill

**Module:** `mod-102-architecture-under-uncertainty`
**Planned time:** ~2 hours
**Chapter this builds on:** [`01-monolith-first-and-evolutionary-architecture.md`](../01-monolith-first-and-evolutionary-architecture.md)
(specifically the *evolutionary architecture and fitness
functions* section)

## Problem statement

Author and (if you have a codebase to point at) **land**
three **executable fitness functions** that guard the
load-bearing architectural invariants your (or a real
reference) startup cannot afford to lose over the next 12
months. Each fitness function must run in CI, fail the
build when the invariant is violated, and point back at
the ADR (from exercise 02) that authorises the invariant.

The point of the drill is not to write test scaffolding. It
is to make the mechanism from *Building Evolutionary
Architectures* (Ford, Parsons, Kua) concrete — the
mechanism by which the ADR that says "we chose Postgres and
we want to stay on one persistence store" is actually
enforced against the drift that would otherwise erode it,
so that at the next stage transition the invariant is
either still true or has been *explicitly* superseded.

## Requirements

Author **three fitness functions**, each covering a
different class of invariant. Do **not** author three
fitness functions covering the same class (three
module-boundary checks is one fitness function repeated
three times, not three fitness functions).

### The three classes to cover

Pick one fitness function from each of the following three
classes.

**Class 1 — Module / dependency boundary.** A fitness
function that asserts one module of the codebase does not
depend on another in a way that would erode the
strangler-fig seams from chapter 01.

- Example: `billing/` may not import from `catalog/models`;
  cross-module calls must go through a named service class
  in `catalog/services.py`.
- Tools that make this straightforward: ArchUnit (Java),
  Dependency Cruiser (JS/TS —
  [github.com/sverweij/dependency-cruiser](https://github.com/sverweij/dependency-cruiser)),
  `import-linter` (Python —
  [import-linter.readthedocs.io](https://import-linter.readthedocs.io/)),
  or a small language-agnostic AST script.

**Class 2 — Operational / performance budget.** A fitness
function that asserts a system-level operational property
does not silently regress — usually a budget that would
signal accidental complexity if crossed.

- Example: app cold-start time under N seconds on a clean
  environment; container image size under N MB; startup
  memory footprint under N MB; test suite runs in under N
  minutes.
- Tools: hyperfine
  ([github.com/sharkdp/hyperfine](https://github.com/sharkdp/hyperfine))
  or the language ecosystem's benchmark harness, wrapped in
  a CI step that fails on threshold.

**Class 3 — Cross-cutting concern.** A fitness function
that asserts a cross-cutting property the ADRs from
exercise 02 depend on staying true.

- Examples: only `infra/` imports the cloud SDK
  (vendor-lock invariant from chapter 01); every database
  migration is expand-then-contract-safe; every HTTP
  handler emits a structured log line with a trace ID;
  no secret string literals in the repo (protected by
  gitleaks or trufflehog
  [github.com/gitleaks/gitleaks](https://github.com/gitleaks/gitleaks)).

### For each fitness function

Author both the **code** and a short **spec** (a one-page
Markdown file next to it) with:

- **Invariant** — one sentence, stated in the active
  voice, that the fitness function protects. "The billing
  module does not import from `catalog/models`."
- **ADR it protects** — the ADR (from exercise 02, or from
  your existing ADR set) that authorises the invariant.
  If the invariant is not backed by an ADR, either open
  one or delete the fitness function — orphaned fitness
  functions rot fast.
- **How the check runs** — command, expected exit code,
  CI stage it lives in, expected duration. A fitness
  function that runs on a nightly cron rather than on
  every PR is much less useful; call this out if the
  check has to be nightly (e.g. because it depends on a
  perf baseline that a PR budget can't afford).
- **What "fail the build" looks like** — an example of
  the error message, so that a future engineer seeing the
  failure knows what invariant they just broke and where
  to read about it.
- **Kill criterion** — the condition under which this
  fitness function itself should be *deleted* (usually:
  the ADR it protects has been superseded, or the
  invariant is no longer load-bearing). Fitness functions
  that stay in CI after their invariant is obsolete are
  the reason many teams distrust the discipline.

### Where the code and spec live

Suggested layout — extend the `docs/adr/` and
`docs/architecture/` layout from earlier exercises:

```
docs/
  fitness/
    01-module-boundary-billing-catalog.md   # spec
    02-cold-start-budget.md
    03-vendor-isolation.md
    README.md                                # index
tests/fitness/
    test_module_boundary.py                  # code
    test_cold_start_budget.py
    test_vendor_isolation.py
.github/workflows/
    fitness.yml                              # CI stage
```

The exact tooling / directory names are yours to choose;
what matters is that the fitness suite runs in CI and the
specs are alongside the code.

### Then — the meta-question

After the three fitness functions and their specs, write a
short (200-400 word) answer to:

- Which of the three invariants was hardest to write a
  fitness function for? Was it because the invariant
  itself was fuzzy (in which case the underlying ADR
  needs sharpening), because the tooling was awkward (in
  which case name the alternative you would try next), or
  because the invariant genuinely cannot be automated at
  this stage (in which case name the *manual* review
  step — a checklist item in the PR template, a rotation
  duty — that stands in for it until it can be)?
- Name the **next three fitness functions** you would add
  over the coming two quarters if this discipline were
  sustained. This becomes your fitness-function backlog
  and pairs with the ADR backlog from exercise 02.

## Starter guidance

- Read the *Building Evolutionary Architectures* (Ford,
  Parsons, Kua) chapter on fitness functions if you can
  get to the book; the O'Reilly summary at
  [oreilly.com — Building Evolutionary Architectures](https://www.oreilly.com/library/view/building-evolutionary-architectures/9781491986356/)
  is the canonical reference and the ThoughtWorks
  articles on the topic
  ([thoughtworks.com — Evolutionary architecture](https://www.thoughtworks.com/en-us/insights/blog/microservices/evolutionary-architecture))
  are the shortest primer.
- Fitness functions are *not* unit tests. A unit test
  asserts that a piece of code does what its name says.
  A fitness function asserts that a *system-level
  architectural property* still holds. If the failure of
  your fitness function reads like "an assert in
  `test_billing.py` failed", you have written a unit
  test.
- Make the failure message *educational*. A fitness
  function that fails with `AssertionError: False is not
  True` teaches nothing. A fitness function that fails
  with `Module 'billing' imports 'catalog.models' — this
  breaks the strangler-fig seam authorised by
  ADR-0003; either revise the design or supersede the
  ADR` teaches the next engineer.
- Do not aim for full coverage of every invariant. Three
  well-chosen fitness functions that stay green (or
  fail-loudly and get fixed) are worth twenty
  aspirational checks that get skipped in CI.
- If your codebase does not exist yet, author the specs
  and stub the code. The specs alone are the more
  valuable artifact; a first engineering hire can
  implement the checks from the specs on day two.

## Acceptance criteria

Your fitness-function set is complete when a reader (a
first engineering hire, a technical advisor, or you
six months from now) can:

- Read the three spec pages and see which invariants the
  codebase protects and why each matters — with a direct
  link to the ADR from exercise 02.
- See the fitness functions run in CI (or, if the
  codebase does not exist yet, see the CI-stage sketch
  and the stub code for each).
- Read a failure message from any one of the three and
  know both what invariant they just violated and where
  to read about why it matters.
- See the kill-criterion line on each spec and
  understand under what condition this specific check
  will be retired.

The output of this exercise is the mechanism that turns
the ADRs from exercise 02 from documents-on-a-shelf into
enforced-in-CI architectural properties. Chapter 01's
"cheap to change" invariant, in operational form.
