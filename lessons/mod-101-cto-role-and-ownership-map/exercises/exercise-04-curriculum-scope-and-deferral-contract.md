# Exercise 04 — Curriculum Scope and Deferral Contract

**Module:** `mod-101-cto-role-and-ownership-map`
**Planned time:** ~2 hours
**Chapter this builds on:** [`03-startup-track-pathway-coverage-map.md`](../03-startup-track-pathway-coverage-map.md)

## Problem statement

Draft a **deferral contract** for your own startup — a
one-page document that names, for each pillar of the
AI-startup pathway, (a) which peer or higher-level track
owns the depth in that pillar, (b) who at your company is
consuming that depth, and (c) which questions you will
explicitly *route out* of the CTO seat rather than
answering yourself.

The deferral contract is the artifact that lets a
co-founder, an investor, or a new hire see — at a glance
— where the boundary of the CTO seat sits at your
company. It also protects you: if a question in someone
else's pillar arrives on your desk and the contract says
"CEO owns", you have a document to point at, not a
conversation to re-open every time.

## Requirements

Produce a **one-page deferral contract** (roughly 400-800
words) containing all of the following. The output should
be legible to your CEO / co-founder, not just to you.

### 1. Scope in — what the CTO seat owns at your company

Reproduce, in your own words, the "This repo owns" list
from [`CURRICULUM.md`](../../../CURRICULUM.md), tailored
to your company's current stage. Cross out (or drop) any
items that do not yet apply — e.g. if you have not yet
crossed the SOC 2 threshold, mod-107 is scope but the
attestation itself is not yet in flight.

At the end of this section, state — in one sentence — the
current-quarter *ownership priority* the CTO seat is
delivering against (usually the largest live problem from
[`exercise-01`](exercise-01-cto-ladder-self-assessment.md)
or [`exercise-03`](exercise-03-personal-stage-by-stage-development-plan.md)).

### 2. Peer-track deferrals — who owns each other pillar

Fill in the following table for your specific company.
Every row must have a named owner (not "TBD" and not "the
team"). If the pillar has no dedicated owner yet at your
stage, name the current best proxy (usually the CEO for
Strategy / Finance / GTM at pre-seed and early seed) and
flag the row as *interim*.

| Pillar | Owning peer track | Named owner at your company | Interim? | Handoff trigger |
|---|---|---|---|---|
| Product | `cpo-curriculum` | | | Hiring the first PM |
| Strategy / CEO | `founder-ceo-curriculum` | | | (usually never — the CEO owns Strategy indefinitely) |
| People / Ops | `startup-operations-governance-curriculum` | | | Hiring the first Head of People |
| Finance | `startup-finance-fundraising-curriculum` | | | Hiring the first CFO or Head of Finance |
| GTM / Sales | `startup-product-gtm-curriculum` | | | Hiring the first Head of Sales / GTM |
| Governance | `startup-operations-governance-curriculum` | | | Depends — often stays with the CEO until Series-B |

The **Handoff trigger** column names the event at which
the current interim owner will hand the pillar off to the
peer-track owner. This is the mechanism that keeps the
contract honest as the company grows.

### 3. Higher-level-track deferrals — what will graduate up

Name the higher-level tracks that will inherit the next
chapter of the ladder past this repo, and — for each —
the trigger at which you will start routing questions
there rather than answering them yourself. Use the list
from chapter 03:

- [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning) (level 45).
- [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning) (level 55).
- [`ai-infra-principal-engineer`](../../../ai-infra-principal-engineer-learning) (level 50).
- [`chief-ai-officer`](../../../chief-ai-officer-learning) (level 70) — if you are the AI executive of an AI-native company.
- `startup-exit-curriculum` (level 40) — for M&A / exit.

For each, one line: *"Route to [track] when [trigger]"*.
If your company is still at rung (a) or (b), most of
these triggers will be "not yet applicable" — write that
explicitly rather than leaving them blank.

### 4. Sideways deferrals — engineering-craft depth

Name the peer engineering tracks the AI-native CTO
consumes depth from without owning:

- [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning) (level 30) — day-two management craft.
- [`ai-infra-mlops`](../../../ai-infra-mlops-learning) (level 25) — MLOps depth.
- [`ai-infra-ml-platform`](../../../ai-infra-ml-platform-learning) (level 30) — ML platform depth.
- [`ai-risk-engineer`](../../../ai-risk-engineer-learning) (level 25) — AI safety / risk-engineering depth.

For each, one line: *"Consumed by [named engineer role
at your company, or 'not-yet-hired [role]']; CTO makes
the build-vs-buy and platform-selection calls
(mod-103)."*

### 5. Out of scope — routed to specialists, not to a track

Name the specialists you route to for the following:

- Legal opinion → counsel.
- External audit attestation → CPA firm (SOC 2 / ISO 27001).
- Specialist advisor scope — patent, immigration, tax, PR crisis, executive coaching, etc.

For each: name the actual firm / person you would route
to today, or explicitly write "*not-yet-retained; will
retain when [trigger]*". Do not leave the specialist
column blank — the contract has to survive a Series-B
technical DD, which will ask.

### 6. Review cadence

State the cadence at which the contract will be
re-reviewed with the CEO (and, if relevant, the board).
Quarterly is a sensible default. Name the specific
calendar slot.

## Starter guidance

- The peer-track routing table (section 2) is the
  load-bearing artifact. Spend the majority of the two
  hours getting the named owners right — not on prose.
- If a row has no owner other than you at your current
  stage, do *not* leave it blank and do *not* silently
  claim the pillar. Write "interim: CTO" or "interim:
  CEO" with a handoff trigger, so the interim status is
  legible.
- The contract is a *joint* artifact with the CEO. If the
  CEO disagrees with any row, the answer is a
  conversation before you finalise, not a
  fait-accompli. Mod-108 covers the decision-rights map
  this contract slots into.
- Do not invent case studies or metrics to justify the
  scope-in list. Base it on your company's real product,
  real stage, and real headcount.
- If a specialist is "not-yet-retained", state the
  trigger to retain them (e.g. "will retain counsel
  before first employee handbook", "will retain a CPA
  firm before signing our first enterprise deal that
  contractually requires SOC 2").

## Acceptance criteria

Your deferral contract is complete when:

- A reader (CEO, investor, new hire) can see, on a single
  page, what the CTO seat owns and what it does not, at
  your company's current stage.
- Every peer-track row has a named owner (not blank, not
  "TBD"). Interim rows are flagged and have a handoff
  trigger.
- Every higher-level-track row has either a routing
  trigger or an explicit "not yet applicable".
- Every out-of-scope row has either a named specialist or
  a "not-yet-retained + trigger" note.
- The review cadence has a calendar slot, not a vague
  intention.
- The CEO has seen the draft and either co-signed or
  named the specific rows they want to revise. (If you
  cannot get CEO review before finalising this exercise,
  submit the draft with a note stating the review is
  pending and the target date.)
