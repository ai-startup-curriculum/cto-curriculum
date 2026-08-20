# Exercise 04 — ISO/IEC 25010 Quality-Attribute Trade-off Map

**Module:** `mod-102-architecture-under-uncertainty`
**Planned time:** ~2 hours
**Chapter this builds on:** [`04-iso-25010-quality-attribute-trade-offs.md`](../04-iso-25010-quality-attribute-trade-offs.md)

## Problem statement

Rank the eight (or nine, in the 2023 revision) ISO/IEC 25010
product-quality characteristics for your (or a real
reference) startup at its current stage, and identify the
**two characteristics you are actively trading away this
quarter**. Then, for each of the traded-away
characteristics, name the specific pressure that would
force you to re-open the trade.

The point of the drill is not to produce a ranking as a
poster. It is to force the trade-off vocabulary from
chapter 04 into the same shape a technical due-diligence
reviewer, a first engineering hire, or a technical advisor
would expect to see it in — and to make the reopening
trigger visible enough that the next stage transition
doesn't take you by surprise.

## Requirements

Produce a **one-page trade-off map** containing all four of
the following.

### 1. Current-stage anchor

- The company's funding stage (`IDEA / PRE-SEED / SEED /
  SERIES-A / GROWTH / MATURE`), engineering headcount, and
  the module-01 rung from [`mod-101`](../../mod-101-cto-role-and-ownership-map/)
  the CTO is currently on.
- One-sentence description of the product (who buys it,
  what it does).
- One-sentence description of the load-bearing customer
  commitment this quarter — the thing that would break
  the customer relationship if you missed it. This is the
  anchor the trade-off ranking is against.

### 2. Ranked characteristics

Rank all eight (or nine) ISO/IEC 25010 characteristics —
Functional Suitability, Performance Efficiency,
Compatibility, Interaction Capability, Reliability,
Security, Maintainability, Portability (plus Flexibility if
you include the 2023 addition) — from most to least
prioritised, for **your current stage**.

Format:

```
| Rank | Characteristic | One-sentence justification |
|------|----------------|----------------------------|
| 1    | Maintainability | Product-market fit is unproven; the load-bearing invariant is cheap-to-change. |
| 2    | Functional Suitability | The design partner will not renew without the workflow they asked for. |
| ...  | ...            | ...                        |
```

The one-sentence justification is what turns the ranking
from opinion into argument. If the justification could be
copy-pasted onto another startup's ranking, it is not
specific enough.

### 3. The two characteristics you are actively trading away

Pick the **two** lowest-ranked characteristics from the
table above and expand each into a short paragraph (~100
words) with:

- **What the trade-off currently looks like** — what
  specific quality of the system today reflects the fact
  that you are trading this characteristic down.
- **What the near-term cost is** — the concrete cost of
  having this characteristic at its current level for the
  next 1-2 quarters.
- **What the reopening trigger is** — the specific
  condition (a customer requirement, a scale threshold, a
  compliance event, a stage transition, a specific hire)
  that would force you to re-rank this characteristic
  upward and re-open the affected ADRs from exercise 02.

Example (illustrative, not to be copied verbatim):

> **Portability.** We are running on AWS-specific managed
> services (RDS Postgres, SQS, Cognito). Moving off AWS
> today would take roughly one engineer-quarter. Near-term
> cost is acceptable — we are not seeing customer demand
> for a specific alternative cloud, and the productivity
> win of managed services is worth ~1 engineer-month per
> quarter to us. Reopening trigger: a signed enterprise
> customer whose data-residency requirements force
> deployment into a region or environment AWS does not
> serve, at which point we open ADR-00XX on the isolation
> strategy.

### 4. The ADR pointer table

Cross-reference your top-3 and bottom-2 ranked
characteristics against the ADRs you authored in
[`exercise-02`](exercise-02-adr-authoring-for-three-real-decisions.md).

Format:

```
| Characteristic | Rank | Which ADR names this trade-off explicitly |
|----------------|------|-------------------------------------------|
| Maintainability | 1    | ADR-0001, ADR-0003 (both name modifiability positively) |
| ...            | ...  | ...                                       |
```

If a top-ranked characteristic has **no** ADR that names it,
that is the exercise's most useful finding — you have a
strategic priority you have not written down. Add a row and
name the ADR you would author to fix it.

### Then — the meta-question

After the ranking, the two traded-away paragraphs, and the
ADR pointer table, write a short (200-400 word) answer to:

- If the same exercise were run again at the *next* stage
  transition your company is pointing at (per your
  [`mod-101`](../../mod-101-cto-role-and-ownership-map/)
  exercise-04 sequencing), which two characteristics
  would you expect to *move up* in the ranking, and why?
  Which of the ADRs from exercise 02 would you expect to
  be superseded as a consequence?

## Starter guidance

- Read the ISO/IEC 25010:2023 characteristic list once
  before you rank
  ([iso.org/standard/78176](https://www.iso.org/standard/78176.html)
  or the more browsable
  [iso25000.com](https://iso25000.com/index.php/en/iso-25000-standards/iso-25010)).
  The vocabulary matters — using "reliability" when the
  actual concern is "recoverability" muddles the
  discussion.
- Do not include ties. "Maintainability and Reliability
  are equally important" is almost never true at pre-seed
  / seed, and forcing yourself to pick one first surfaces
  the honest priority.
- The two-characteristics-you-are-trading-away framing is
  where most of the exercise's insight lives. Resist the
  urge to argue that you are not really trading anything
  away. If you cannot name any characteristic you are
  trading down, either you are optimising for a
  characteristic no one has articulated (write it down),
  or your ADRs are not yet resolving trades (revisit
  exercise 02).
- Be honest about the reopening trigger. "When we grow"
  is not a trigger. "When we sign the first customer
  requiring in-region EU data storage" is a trigger.
- The AWS Well-Architected Framework
  ([aws.amazon.com/architecture/well-architected](https://aws.amazon.com/architecture/well-architected/))
  and the SEI ATAM
  ([sei.cmu.edu — ATAM](https://insights.sei.cmu.edu/library/architecture-tradeoff-analysis-method-collection/))
  are useful adjacent vocabularies if you want deeper
  reading; ISO/IEC 25010 alone is enough for the
  exercise.

## Acceptance criteria

Your trade-off map is complete when a reader (a
co-founder, a technical advisor, a due-diligence reviewer)
can:

- Read the current-stage anchor and immediately understand
  the stage and the load-bearing customer commitment.
- Read the ranking table and follow which quality
  characteristics matter most this quarter and *why*
  (not "because they matter" but "because of this specific
  situation").
- Read the two traded-away paragraphs and understand what
  the near-term cost is and what would force the trade to
  reopen.
- Cross-reference the ranking to the ADRs from exercise 02
  and see either a matching ADR *or* the gap that needs
  to become the next ADR.

The output of this exercise feeds directly into the
Consequences section of every subsequent ADR you author,
and into the paired [lab-01](../README.md#lab) architecture
package once the lab prompt is scaffolded.
