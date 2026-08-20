# Exercise 02 — CTO vs. VP Eng vs. Chief Architect Decision Drill

**Module:** `mod-101-cto-role-and-ownership-map`
**Planned time:** ~2 hours
**Chapter this builds on:** [`02-cto-vs-vp-eng-vs-chief-architect-vs-head-of-platform.md`](../02-cto-vs-vp-eng-vs-chief-architect-vs-head-of-platform.md)

## Problem statement

Given a set of ten realistic decision scenarios that arise in
an early-scale engineering org, assign each to the role that
should *own* the decision (CTO, VP Engineering, Chief
Architect, or Head of Platform) and defend the assignment.
Then, for each scenario, state whether that role even *exists*
as a separate seat at your current stage — and if it does not,
name who is playing the hat.

The point of the drill is not to memorise a role rubric. It is
to force explicit judgement about the split boundaries, so
that when the real decisions arrive at your company you have
already rehearsed the argument.

## Requirements

Produce a **decision matrix** (a table plus per-row commentary)
covering the ten scenarios below. Each row must contain:

- The scenario (copy-paste from below).
- The **owning role** — CTO / VP Eng / Chief Architect / Head
  of Platform.
- Whether that role is a **separate seat at your current
  stage** — Yes / No; if No, name the person actually playing
  the hat.
- A **one-sentence defence** — why this role owns the decision
  in the general case, citing chapter 02's role definitions.

### The ten scenarios

1. A senior engineer wants to change the on-call rotation
   from 24×7 primary to a follow-the-sun rotation across two
   time zones. Who owns the decision?
2. A product-engineering team wants to introduce a new
   persistence store (a graph database) for a feature that
   two other teams' features would eventually also use. Who
   owns the decision?
3. The recruiting-loop conversion rate has dropped from
   ~15% to ~5% offer-accept. Who owns the remediation?
4. A director-level candidate is negotiating a
   comp-package variance that would exceed the current band
   by 20%. Who owns the decision?
5. The internal-developer-platform team is proposing a new
   opinionated deployment tool that would replace three
   stream-aligned teams' current deploy scripts. Who owns
   the decision?
6. The Series-B lead investor's technical DD asks for a
   remediation plan for a specific architectural risk. Who
   owns the response?
7. A staff engineer on one team wants to introduce a
   library that would create a hard cross-team runtime
   dependency between two previously independent services.
   Who owns the decision?
8. The engineering-org-wide performance-review cycle needs
   its rubrics updated for the new career-ladder v1. Who
   owns the update?
9. The head of Sales is asking for a customer-facing
   architectural whitepaper to close a large enterprise
   deal. Who owns the whitepaper?
10. The engineering team is asking for a "20% refactor
    budget" (see mod-105) tied to the next roadmap cycle.
    Who owns the decision to allocate it?

### Then — the meta-question

After the ten-row matrix, write a short (150-300 word)
answer to the following:

- For your own startup at its current stage: which of the
  four hats (CTO, VP Eng, Chief Architect, Head of
  Platform) do you play, and which are played by someone
  else? If you play more than one, which is the *hat you
  are worst at* — the one most likely to be the first
  split-hire — and what evidence (attrition, delivery
  cadence, hiring-loop throughput, calendar drift) points
  at that hat rather than one of the others?

## Starter guidance

- If your instinct on a row is "well, it depends" —
  articulate what it depends on and pick the *default*
  owner. The exercise is about explicit judgement, not
  about being clever.
- Distinguish "who is on the hook for the outcome" from
  "who does the work". The Chief Architect might do the
  work on scenario 7; the CTO might still own the decision
  if there is no Chief Architect seat yet.
- Do not invent a "co-owned" answer for every row to avoid
  making a call. Every scenario has a default owner; the
  point is to name it.
- For scenario 10 in particular, be honest about whether
  the refactor budget is a CTO decision (strategy) or a
  VP Eng decision (delivery cadence) — the answer is
  different depending on which side of the split the two
  seats are on at your company.
- Ground the meta-question answer in **evidence you can
  point at**, not in self-deprecation. "I'm bad at people
  management" is not evidence. "My last two hiring loops
  slipped because I did not calibrate the interviewers,
  and my last cycle of performance conversations was
  three weeks late" is evidence.

## Acceptance criteria

Your decision matrix is complete when a reader (typically
your CEO or a mentor) can:

- Read any row and see the assignment plus the defence
  without needing to open chapter 02.
- Read the "separate seat at current stage" column and see
  a coherent picture of your current org: usually, at
  pre-seed and seed, most rows will be Yes for CTO / No for
  the other three, with the "actually playing the hat"
  column pointing at you (or a founding-engineer tech lead).
- Read the meta-question answer and see which hat is
  earmarked for the next split-hire, with evidence.

The output of this exercise should be usable as an input to
[`exercise-03`](exercise-03-personal-stage-by-stage-development-plan.md)
— specifically to the section of the plan that decides
whether the next hire is another engineer or the first EM /
first Chief Architect / first Head of Platform.
