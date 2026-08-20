# Exercise 01 — Monolith First vs. Services Decision Drill

**Module:** `mod-102-architecture-under-uncertainty`
**Planned time:** ~2 hours
**Chapter this builds on:** [`01-monolith-first-and-evolutionary-architecture.md`](../01-monolith-first-and-evolutionary-architecture.md)
(and, for the trigger vocabulary, [`05-monolith-modular-monolith-services-and-cap.md`](../05-monolith-modular-monolith-services-and-cap.md))

## Problem statement

Given six deliberately-ambiguous starting-architecture
scenarios that a pre-seed / seed CTO might reasonably face on
day one, make an explicit call for each: **single monolith,
modular monolith with strangler-fig seams, or extracted
services**. Defend each call against Fowler's *MonolithFirst*
default and against the extraction-trigger vocabulary from
chapter 05.

The point of the drill is not to memorise "the right answer".
It is to force the trade-off to be named, so that when a real
version of one of these scenarios shows up at your startup
you have already argued through the shape of the argument
with a clear head.

## Requirements

Produce a **decision matrix** (a table plus per-row
commentary) covering the six scenarios below. Each row must
contain:

- The scenario (copy-paste from below).
- Your **starting-architecture call** — one of: `Single
  monolith` / `Modular monolith` / `Modular monolith + one
  extracted service` / `Two or more extracted services`.
- The **two ISO/IEC 25010 characteristics** (see chapter 04)
  you are actively trading toward with the call, and the
  **one** you are actively trading away.
- The **specific pressure** from chapter 05 that would
  trigger the next extraction step (scaling-profile
  divergence, team-topology divergence, failure-isolation
  divergence, compliance divergence) — or "no expected
  extraction inside 12 months" if you would not extract at
  all inside the first year.
- A **one- to two-sentence defence** — why this call, not
  the more-services-shaped or less-services-shaped
  neighbour.

### The six scenarios

1. **B2B SaaS, 3 engineers, one design partner.** A
   pre-seed startup with 3 engineers (all backend-strong,
   all with Django experience) is building a B2B workflow
   tool. One design partner, no revenue, no launched
   product. Expected traffic in the first 12 months: tens
   of RPS at peak. What is the starting architecture?

2. **Consumer mobile, 5 engineers, waitlist of 20k.** A
   seed-stage consumer-mobile startup with a React Native
   app, a backend, and a machine-learning-heavy
   recommendation feature. Team is 5 engineers — 2 mobile,
   2 backend, 1 ML. Waitlist of 20,000 users; expected
   launch traffic in the low-thousands of RPS with
   real-time recommendation latency below 300ms p95. What
   is the starting architecture?

3. **Regulated fintech, 4 engineers, first bank customer.**
   A seed-stage fintech selling into US regional banks.
   First customer is a signed enterprise deal with a
   90-day security review, SOC 2 Type I expected within 6
   months, and specific data-residency requirements. Team
   is 4 engineers, none with prior Kubernetes production
   experience. What is the starting architecture?

4. **AI-native product, 2 engineers, foundation-model
   dependency.** A pre-seed AI-native product where the
   core value is a fine-tuned foundation-model orchestrated
   with retrieval-augmented generation over customer
   documents. Team is 2 engineers, one with strong
   Python-backend chops and one with an ML background. No
   customers yet; first paid pilot expected in Q3. What is
   the starting architecture?

5. **Vertical-SaaS platform absorbing a legacy product.**
   A seed-stage vertical-SaaS company just acquired a small
   legacy PHP product with real customers and real revenue
   (~$500k ARR). Team is 6 engineers total, 2 of whom came
   with the acquisition. The plan is to migrate the legacy
   customers onto the new platform over 12 months without
   downtime. What is the starting architecture *for the new
   platform*, given the legacy product is in the picture?

6. **Two founders, no engineers, MVP in a no-code tool.** A
   pre-seed startup at the earliest possible stage — two
   non-technical founders, no engineers hired, an MVP built
   in Bubble / Retool / Airtable to prove the workflow with
   the first three design partners. The founders have
   raised a small pre-seed to hire two engineers. What is
   the starting architecture the first engineering hires
   should build toward, and how does the answer differ
   from scenarios 1-5?

### Then — the meta-question

After the six-row matrix, write a short (200-400 word)
answer to the following:

- Which of the six scenarios is closest to *your* startup's
  current situation (or the real reference startup you are
  working against)? What single fact about your situation
  differs most from that scenario, and how does that
  difference change your starting-architecture call?
- If you are running the actual monolith you called for in
  the closest scenario, name the **first fitness function**
  (chapter 01) you would add to CI this quarter to keep the
  seams from rotting. Cite the module boundary it protects
  and how the check would fail the build.

## Starter guidance

- If your instinct on a scenario is "well, it depends" —
  articulate what it depends on and pick the *default*
  answer. The exercise is about explicit judgement, not
  about being clever.
- Do not invent a "microservices-lite" middle answer for
  every row. Chapter 01's four options are deliberately
  distinct; pick one.
- The two ISO/IEC 25010 characteristics you are trading
  toward should be *explicit* — "Maintainability and
  Reliability" is not enough; "Maintainability (specifically
  modifiability) and Reliability (specifically
  recoverability)" is the level of precision the ADR
  authoring in exercise 02 will demand.
- For scenario 5, the honest answer probably involves the
  StranglerFig pattern from chapter 01 in a specific way.
  Name it.
- For scenario 6, the honest answer probably says
  something about *when* to introduce module boundaries
  rather than just *whether*. Name the trigger.
- Ground the meta-question answer in **evidence you can
  point at**, not in aspiration. "We want to be
  maintainable" is not evidence. "Our billing module and
  our identity module currently share an ORM base class
  that leaks assumptions across the boundary" is evidence.

## Acceptance criteria

Your decision matrix is complete when a reader (a co-founder,
a technical advisor, a mentor) can:

- Read any row and see the starting-architecture call plus
  the trade-off characteristics without needing to open
  chapter 01 or chapter 04.
- See in the trigger column which specific pressure would
  make the answer move — so that when the pressure arrives
  at your company, the row is already the ADR context
  section.
- Read the meta-question answer and see which fitness
  function you would add to guard the seams — specific
  enough that a second engineer could implement it from
  the description.

The output of this exercise feeds directly into
[`exercise-02-adr-authoring-for-three-real-decisions.md`](exercise-02-adr-authoring-for-three-real-decisions.md);
your starting-architecture call and the trade-off you named
here should show up almost verbatim as ADR-0001 in that
exercise's output.
