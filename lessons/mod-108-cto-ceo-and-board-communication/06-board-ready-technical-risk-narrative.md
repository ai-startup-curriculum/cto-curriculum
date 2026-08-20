# The Board-Ready Technical Risk Narrative — What Rises to the Board vs. What Stays in Engineering

> "The board is not your risk register. It is your
> *escalation channel* for the risks that leave the
> engineering org's control." — the framing this
> chapter is organised around.

## Motivation

Every board pre-read (chapter 03) has a risks section.
The question of *what belongs in that section* is one
of the most consequential and least-taught pieces of
board-communication craft. Two failure modes are
symmetric and equally costly:

- **Under-reporting.** The CTO reports only the risks
  they already have a plan for and quietly omits the
  ones they do not, because they do not want to alarm
  the board. The board, deprived of the actual risk
  register, is unable to help — and when the omitted
  risk crystallises, the board's confidence in *every
  future CTO risk report* is damaged, including the
  ones the CTO does have a plan for.
- **Over-reporting.** The CTO lifts the full internal
  engineering risk register — 40 items ranging from
  *"Prometheus is on an unsupported version"* to *"we
  have unbounded HIPAA exposure"* — into the board
  deck. The board, unable to distinguish the material
  risks from the operational noise, treats the whole
  register as noise, and the material items get the
  same attention as the operational ones.

The discipline is a *three-class* filter that names
which risks rise to the board and which stay inside
the engineering org, and — critically — the narrative
arc that ties the risks the board *does* see to the
CEO's fundraising narrative without either alarming
the board or hiding real exposure.

## The three risk classes that rise to the board

The three classes of risk that belong in the board
risk section of the pre-read (chapter 03, section 2)
are:

- **Existential technical vulnerabilities.** Risks
  that, if realised, would *materially harm* the
  company as a going concern — a single-vendor
  dependency whose outage would take the product
  offline for more than N hours, a critical
  security exposure with a public CVE and no
  patched path, a load-bearing architectural
  constraint the buyer would discover in DD.
- **Key-person risk.** The register of key persons
  from folder 04 of the DD data room (chapter 04),
  with the current mitigation posture per role. The
  board hears about it *by role*, not by name — the
  names live in the DD data room and the operating
  detail, not in the board deck.
- **Un-scoped compliance obligations.** Any
  compliance obligation the company has *acquired*
  without scoping — a new jurisdiction, a new data
  type, a new customer contract with an unsupported
  commitment, a new integration that changes the
  data-flow diagram. The register lists each, the
  scoping status, and the timeline to move it from
  *acquired* to *scoped*.

Every risk in the board risk section belongs to one
of these three classes. Anything else — a slower-than-
target sprint velocity, a specific engineer's
performance concern, a decision to switch database
vendors — is engineering-org-internal noise and
belongs in an operational review, not the board deck.

## What stays inside the engineering org

The rule is the mirror of the three-class filter:
risks that live inside the engineering org's own
control, whose realisation would harm the engineering
org's execution but not the company as a going
concern, do not rise to the board. Concretely:

- **Sprint- and quarter-level delivery risk.** *"We
  might miss the Q3 SAML SSO ship date."* That is a
  status-report item in the roadmap-progress section
  (Section 1 of the pre-read), not a risk-section
  item. If a Q3 miss materially harms a customer
  commitment already made — that is a different
  matter and lifts the risk.
- **Individual-performance concerns** below the
  founder-team level. These are HR / manager
  concerns, and route through the CEO and (once
  they exist) a People / Ops function, not through
  the board deck.
- **Tooling and process choices.** Choice of a new
  observability vendor, migration off a language
  runtime, refactor of a code sub-tree, adoption of
  a new testing framework. These are engineering-
  process work, not board work.
- **Ongoing DORA-metric fluctuations.** A short-
  duration dip in deploy frequency or an uptick in
  change-failure rate is engineering process; a
  sustained-pattern degradation may lift to the
  board if it crosses into one of the three
  classes.
- **Technical-debt items** below the material
  threshold. The technical-debt portfolio from
  [`mod-105`](../mod-105-technical-debt-as-business-decision/README.md)
  is an operating artifact. Individual items lift to
  the board only when they cross into an existential
  vulnerability (a load-bearing debt that has
  become unbounded) or when the *portfolio* itself
  is being materially re-scoped.

The load-bearing sentence: **an engineering-org-
internal risk becomes a board risk when it crosses
into one of the three classes**, not before. The
CTO's judgment call is where *cross-over* happens;
naming that judgment call in the running risk
register keeps the criterion honest.

## Class 1 — Existential technical vulnerabilities

*Existential* is a strong word and is chosen
deliberately. A risk is *existential* if realisation
would materially harm the company as a going concern —
lose an anchor customer, breach a regulator threshold,
force a fundraise at a distressed valuation, or make
the product unshippable for more than a specified
window. Concretely, the classes that most often
appear in early-stage CTOs' board decks:

- **Foundation-model provider dependency risk.** If
  the product is AI-native and depends on a single
  foundation-model provider (Anthropic, OpenAI,
  Google DeepMind, or a specific open-weights
  stack), the outage or terms-change of that
  provider is an existential technical risk. The
  mitigation is a *fallback* posture named in the
  register.
- **Cloud-provider concentration.** Single-region or
  single-provider deployments where the outage of
  that region / provider would take the product
  offline. This is a graduated risk: at seed, a
  single-region posture is normal and not
  existential unless the customer base has
  contractual multi-region requirements; at
  Series-A, an anchor enterprise customer's DR
  requirement can lift it.
- **Data-loss risk.** Backup posture, point-in-time
  recovery windows, and the specific class of
  incident that would cause customer data loss with
  no recovery path.
- **Critical security exposure.** A published CVE
  affecting a load-bearing dependency with no
  patched path, or a discovered exposure that meets
  the customer- or regulator-notification threshold.
  See mod-107 chapter 05's HIPAA notification
  threshold and chapter 04's GDPR Article 33
  breach-notification obligations.
- **Regulator interaction underway.** Any HHS OCR,
  supervisory-authority, state AG, or FTC
  interaction that has been opened. Even if the
  interaction is expected to resolve favourably,
  the *existence* of the interaction is a board-
  reportable item.
- **Load-bearing architectural constraint.** A
  design choice that would take more than a
  quarter of engineering time to unwind, that a
  buyer or lead investor would name in DD as a
  price-cut lever (chapter 05).

For each existential vulnerability the register
carries:

- The risk in one sentence.
- The realisation impact (what happens if it fires).
- The current mitigation state.
- The trajectory (increasing / stable / decreasing).
- The board ask (informational / advice-sought /
  decision-requested).

An illustrative structured version:

```yaml
# docs/founder-comms/board-risk-register.yaml
existential:
  - id: R-2026-Q3-EX-01
    risk: "Foundation-model provider concentration on primary vendor"
    impact: "24-72 h product outage on primary-vendor incident; product cannot ship next model release without contract renewal"
    mitigation:
      - "Fallback provider integration in flight, expected Q4 GA"
      - "Contract renegotiation with primary vendor in progress"
    trajectory: decreasing
    board_ask: informational
  - id: R-2026-Q3-EX-02
    risk: "SOC 2 Type II observation window at risk of missing anchor customer's Nov 30 deadline"
    impact: "Anchor customer contract at risk if attestation slips past 2026-11-30"
    mitigation:
      - "Fieldwork accelerated with auditor; interim report Sep 15"
    trajectory: stable
    board_ask: advice_sought
```

## Class 2 — Key-person risk

Key-person risk is a board-level concern because it
is one of the few risks whose *mitigation* is
partially outside the CTO's control — it may require
board-approved equity refresh, retention grants, or
board introductions for redundant hires. The board
hears the risk in a specific format:

- The **role** at risk (not necessarily the name — the
  names live in the DD data room and the founders'
  operating detail).
- The **components / responsibilities** the role
  currently owns.
- The **days-to-recover** estimate if the person left
  today (30 days, 60 days, 90 days, 90+ days).
- The **current mitigation** — cross-training,
  documented runbooks, hiring-in-flight, retention
  grant, redundancy in a specific area.
- The **board ask**, if any — most commonly, a
  request for board members to source candidates
  for a redundancy hire, or a request for
  additional refresh grant approval.

A durable board risk section names 2-5 roles at
seed / Series-A. Zero roles named is not a signal
that key-person risk is absent — it is a signal that
the register has not been maintained. Every startup
under 20 engineers has key-person risk; the register
either names it or hides it.

## Class 3 — Un-scoped compliance obligations

The third class is the one CTOs most-often
under-report at the board level, and the one most
likely to become a DD price-cut lever (chapter 05)
or a regulator-triggered incident. The definition:

- The company has *acquired* a compliance
  obligation — through a customer contract, a new
  jurisdiction, a new data type, a new integration,
  or a new vendor.
- The obligation is not yet *scoped* into the
  compliance posture from
  [`mod-107`](../mod-107-founder-scope-security-and-compliance/README.md).
- The gap between the acquired obligation and the
  scoped posture is measurable — in engineer-months
  of work, in third-party audit spend, or in
  timeline against a customer or regulator
  deadline.

Concrete examples:

- A first EU customer has been signed and the
  company does not yet have a documented GDPR
  Article 30 RoPA, or the EU customer's DPO has
  asked questions the current RoPA does not answer.
- The first healthcare customer has been signed
  and the current architecture is in the "PHI-
  adjacent" scope-call (mod-107 chapter 05), but
  the customer has commitments in-contract that
  require PHI-touching-scope controls.
- A new integration was added that changes the sub-
  processor list (mod-107 chapter 08), but the
  customer-facing sub-processor page has not been
  updated within the change-notice window
  contracted with existing customers.
- The Type II observation window has started but
  a control failure has been identified that will
  produce a *qualified opinion* in the report
  unless remediated within N weeks.

The register format is the same as classes 1 and 2:
the risk in one sentence, the realisation impact,
the current mitigation, the trajectory, and the
board ask.

## The narrative arc — tying the risks to the fundraising story

A well-authored risk section does more than list the
risks; it *frames* them inside the CEO's
fundraising narrative. Three narrative patterns work
in practice:

- **The *"here is what we have already de-risked"*
  pattern.** For every material risk on the
  register at the previous board meeting, the CTO
  names its current status — closed, materially
  mitigated, unchanged, or increased. The board
  hears the register as an active management
  instrument, not a passive list.
- **The *"here is what the next round de-risks"*
  pattern.** For risks whose mitigation is
  hire-driven or capital-driven, the CTO names the
  specific investment (in the coming quarter or in
  the round being raised) that closes the risk.
  This ties the risk register directly to the
  fundraising narrative — investors reading the
  board deck see how their capital retires
  specific technical risk.
- **The *"here is what we are asking your help
  with"* pattern.** For risks where the board's
  operator judgment or network is a mitigation —
  candidate introductions for a key-person
  redundancy hire, an intro to a specialist
  compliance advisor, a decision on scope for a
  new attestation — the CTO names the ask
  explicitly.

The load-bearing property: the risk section is
*never* separated from the rest of the pre-read.
Every risk connects to a commitment from Section 1,
a decision in Section 6, or a piece of the
fundraising narrative. Risks that connect to nothing
are either misclassified (they belong in the
engineering-internal register) or under-scoped (the
mitigation has not been thought through).

## Signals that the narrative has drifted

- **The board sees a material risk for the first
  time on the day it crystallises.** The risk was
  either omitted or under-reported in the
  preceding meetings. Every risk register entry
  earns its keep by *forecasting* the crystallisation
  rather than being surprised by it.
- **The board's response to the risk section is
  *"tell us more"* three quarters in a row.** The
  risks are under-specified. Move to the three-
  class format with the structured fields per
  entry.
- **The board's response is *"none of these seem
  material"*.** The engineering-internal register
  is leaking into the board deck. Re-apply the
  three-class filter; move the operational items
  into the operating review.

## Summary

- The board risk section is authored against a
  **three-class filter**: (1) existential
  technical vulnerabilities, (2) key-person risk,
  (3) un-scoped compliance obligations. Nothing
  outside these three classes belongs in the
  board risk section.
- Engineering-org-internal risks — sprint-level
  delivery, individual-performance concerns,
  tooling choices, DORA-metric fluctuations,
  operational technical-debt — stay in the
  operating review. They lift to the board only
  when they cross into one of the three classes.
- Each entry in the register carries a **fixed
  set of fields**: the risk in one sentence, the
  realisation impact, the current mitigation, the
  trajectory since last meeting, and the board
  ask (informational / advice-sought / decision-
  requested).
- The **narrative arc** ties each risk to a
  commitment, a decision, or a piece of the CEO's
  fundraising narrative — *what we have de-risked*,
  *what the next round de-risks*, *what we are
  asking your help with*. Risks that connect to
  nothing are either misclassified or under-
  scoped.
- The **under- vs. over-reporting failure modes**
  are symmetric — omitting risks damages board
  trust when they crystallise; over-including
  operational noise makes the material risks
  invisible.

The exercise for this chapter —
`exercise-06-board-ready-technical-narrative-authoring.md`
— walks the authoring of the risk-engineering slice
of a real (or reference-startup) board deck.
