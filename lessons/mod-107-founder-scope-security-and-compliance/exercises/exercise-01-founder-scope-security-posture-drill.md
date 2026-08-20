# Exercise 01 — Founder-Scope Security Posture Drill

**Module:** `mod-107-founder-scope-security-and-compliance`
**Planned time:** ~2 hours
**Chapter this builds on:** [`01-founder-scope-security-posture.md`](../01-founder-scope-security-posture.md)

## Problem statement

Author the **one-page founder-scope security posture
memo** for your startup — either your own real startup
or a reference startup you can describe in a paragraph
(product, team size, primary customer profile, current
funding stage, whether the product is AI-native, whether
it handles regulated data). The memo is the artifact you
would send an enterprise design partner who asks *"what
is your security posture?"* before signing a paid
contract.

The point of the drill is not to *build* the posture
(chapters 02–08 walk the artifacts, exercises 02–07
build them). The point is to force yourself to
articulate — from the four founder-scope questions in
chapter 01 — what you already own, what you defer, and
which deferrals are defensible against enterprise
procurement, acquisition-DD, and the first-security-
hire hand-off.

## Requirements

Author a Markdown document at
`docs/compliance/founder-scope-posture.md` (or the
equivalent convention in your working repo).

### Section 1 — Context (200-300 words)

- The startup (product, team size, current stage —
  pre-seed / seed / Series-A, primary customer
  profile, whether AI-native, whether it handles
  regulated data — PII / PHI / financial /
  government).
- The current security state at a glance — what
  exists (SSO, MFA, encryption, audit logs, incident
  response, DPAs, published sub-processor list),
  what does not, and what is in flight.
- The load-bearing customer commitments already made
  (uptime SLA, data-residency promise, notification
  clock, published sub-processor list).

### Section 2 — The four founder-scope questions

One paragraph (150-250 words) per question, from
chapter 01:

- **Q1 — Enterprise-deal risk.** Which controls, if
  absent, would lose you deals this quarter? Name at
  least three, with the specific customer
  conversation or questionnaire item that put each
  on the list.
- **Q2 — Acquisition-DD risk.** Which artifacts, if
  missing at a Series-B DD, would cost the company
  a price cut? Name at least three, with the
  specific DD-checklist item (a16z, buyer-side
  questionnaire) that names each one.
- **Q3 — Hand-off to first security hire.** Which
  parts of the current posture live *only* in the
  CTO's head? Name at least three. For each, name
  the artifact you will produce in the next two
  weeks that moves the decision from head to
  document.
- **Q4 — Legitimate deferrals.** Which security
  investments are you deliberately deferring until
  the first security hire lands? Name at least
  five, with the *why deferrable* rationale from
  chapter 01's deferral list (or a defensible
  alternative). At least one of the five must not
  be from the chapter list — the point is not to
  copy the list but to reason about your own
  context.

### Section 3 — The one-paragraph posture articulation

The paragraph from chapter 01's *"in one paragraph"*
section, filled in with your startup's specifics.
Every clause must have an evidence answer — either
*"in place, evidence at [link]"* or *"on the roadmap,
target date [date], compensating control [what]"*.
Approximate word count: 300-500 words. This is the
answer you can give from memory on a design-partner
call.

### Section 4 — The deferral list handed to the first security hire

A bulleted list of the items you are deferring
(Q4 above), each with:

- The item.
- The current state (what exists, what does not).
- The reason it is deferrable now.
- The trigger that would move it out of the deferral
  list before the first security hire lands (a
  specific customer commitment, a specific incident
  class, a specific compliance driver).

## Starter guidance

- **Answer from calendar and evidence, not from
  intent.** Do not write *"we plan to have MFA
  everywhere"*. Write *"MFA is enforced via Okta on
  every SaaS in scope; production cloud console
  access requires MFA via [vendor]; a workstation
  bypass exists for [role] which we will close by
  [date]"*. If the honest answer is *"we do not
  have it"*, say so — that is what the deferral
  list is for.
- **Read your existing customer contracts before
  writing Q1.** Enterprise contracts often contain
  security exhibits with specific control
  commitments. Any commitment made in a signed
  contract that is not backed by evidence is the
  top item on Q1.
- **Read the a16z technical-DD checklist for Q2.**
  The public version at
  [a16z.com/tech-diligence-checklist](https://a16z.com/tech-diligence-checklist/)
  is the reference. Any category the checklist
  names that your posture is silent on is a Q2
  candidate.
- **Do not conflate Q3 and Q4.** Q3 is *"exists in
  my head, needs writing down"*. Q4 is *"does not
  exist yet, and does not yet need to"*. If you
  find yourself writing the same item in both,
  clarify — either it exists (and needs writing
  down) or it does not (and belongs in the
  deferral list).
- **The deferral list is where credibility lives.**
  A posture memo with no deferral list reads as
  either (a) dishonest or (b) over-scoped. An
  enterprise procurement team that reads *"we
  defer bug-bounty programme, formal threat
  modelling, SIEM, and DPO appointment until the
  first security hire in Q[N]; here is why each is
  deferrable at our scale"* trusts the memo more
  than one that claims universal coverage.
- **The one-paragraph posture articulation is the
  test.** Practice saying it out loud. If any
  clause makes you pause, that clause is not yet
  backed by evidence and belongs on Q3 or Q4.
- **Cite the CAIQ and SIG as the questionnaire
  vocabulary.** The Cloud Security Alliance
  [CAIQ](https://cloudsecurityalliance.org/artifacts/consensus-assessments-initiative-questionnaire-caiq-v4/)
  and the Shared Assessments
  [SIG](https://sharedassessments.org/sig/) are
  the two most-common enterprise vendor-security
  questionnaires; if a clause in your posture
  memo maps to a specific CAIQ / SIG question,
  cite it.

## Acceptance criteria

Your drill output is complete when:

- The posture memo exists at
  `docs/compliance/founder-scope-posture.md` and is
  no more than three pages when rendered.
- Section 1 (context) names startup, stage, product
  shape, team size, primary customer profile,
  AI-native / regulated-data status, and the
  load-bearing customer commitments in under 300
  words.
- Section 2 answers each of the four founder-scope
  questions with the required minimum items (Q1:
  three, Q2: three, Q3: three, Q4: five including
  one non-chapter item).
- Section 3 fills in the one-paragraph articulation
  with concrete vendor names, target dates, and
  evidence references; no clause is a placeholder.
- Section 4 lists every deferral with current
  state, reason for deferability, and trigger to
  move it out.
- The posture memo can be handed to a technical
  reviewer who does not know your startup, and
  they can read it in five minutes and articulate
  your security posture back to you without
  asking a follow-up.
- Every reference to a control or framework in the
  memo cites the primary source (AICPA SOC 2,
  OWASP ASVS, SLSA, GDPR Article X, HHS Security
  Rule reference).

## What this feeds into

- **Exercise 02** — the SOC 2 Type I readiness
  checklist extends the *SOC 2* line from
  Section 3 into a full scope-and-evidence plan.
- **Exercise 03** — the GDPR / CCPA baseline
  extends the *privacy* clauses of Section 3.
- **Exercise 04** — the HIPAA drill extends the
  *PHI-touching / PHI-adjacent* decision from
  Section 1.
- **Exercise 05** — the ASVS L1 scoping drill
  extends the *AppSec* clause of Section 3.
- **Exercise 06** — the SLSA baseline extends the
  *CI/CD integrity* clause of Section 3.
- **Exercise 07** — the vendor DPA / BAA drill
  extends the *sub-processor list* clause of
  Section 3.
- **The module lab**
  (`lab-01-publish-a-founder-scope-security-and-compliance-package`)
  consolidates this memo with exercises 02–07
  into a single `docs/compliance/` sub-tree.
- **Capstone [`project-102`](../../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package)**
  turns the sub-tree into the polished founder-
  scope compliance package.

The drill's discipline is *articulating the
posture out loud before you build it*. If any
clause of Section 3 makes you pause, that clause
is the highest-leverage thing to fix this quarter.
