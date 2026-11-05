# Exercise 07 — Delivery Cadence and On-Call Design

**Module:** `mod-106-scaling-org-and-stack`
**Planned time:** ~3 hours
**Chapter this builds on:** [`07-delivery-cadence-and-on-call.md`](../07-delivery-cadence-and-on-call.md),
extending the 5-to-15 on-call rotation and
blameless-post-mortem template from
[`02-five-to-fifteen-first-structure.md`](../02-five-to-fifteen-first-structure.md)
(and [exercise 02](exercise-02-five-to-fifteen-transition-playbook.md))
to the 15-to-50 and 50-to-150 shape, and cross-
referencing the DORA measurement plan from
[exercise 05](exercise-05-dora-four-key-measurement-plan.md)
and the tech-debt portfolio in
[`mod-105`](../../mod-105-technical-debt-as-business-decision/README.md).

## Problem statement

Author the **four operational artifacts** that make
up the delivery-cadence and on-call substrate — as a
`docs/on-call/` sub-tree (plus a
`docs/planning/cadence.md` for the cadence spec) in
the working repo:

1. **Delivery-cadence spec** — one page. The weekly
   rhythm, the three-loop planning cadence, and the
   kanban-vs-sprint call for your team.
2. **On-call rotation v1 (or v2 if extending)** — a
   short sub-tree. Roster, primary / secondary /
   escalation, page path, handoff, comp, runbook
   convention.
3. **Blameless post-mortem template** — one page.
   The six-section template with the discipline
   language for the *what went badly* section.
4. **Incident-response playbook** — one page.
   Triage / response / resolution, plus the
   incident-command-system pattern at 50-150.

The four artifacts together are what the team
executes week after week and hour by hour when a
page fires. The chapter's discipline is that each is
a written document — the artifact is the memory. A
new hire reads the four documents on their first day
and is then a functioning member of the team without
any tribal on-boarding.

## Requirements

Directory shape:

```
docs/
  planning/
    cadence.md              # artifact 1
  on-call/
    README.md               # rotation (artifact 2)
    page-path.md            # what pages / what does not
    handoff-template.md     # weekly handoff document
    comp.md                 # stipend / PTO / comp adjustment
    runbook-convention.md   # runbook-per-service discipline
    post-mortem/
      template.md           # artifact 3
      archive/
        README.md           # empty archive with naming convention
    incident-response.md    # artifact 4
```

If your working-repo scenario has already authored
the 5-to-15 versions of the on-call rotation and
post-mortem template (from
[exercise 02](exercise-02-five-to-fifteen-transition-playbook.md)),
this exercise *extends* them to the 15-to-50 or
50-to-150 shape rather than duplicating them.
Reference the earlier files explicitly.

### Artifact 1 — Delivery-cadence spec

`planning/cadence.md` — one page. Sections:

- **Stage.** The team's current stage (5-15, 15-50,
  or 50-150). Named.
- **Weekly rhythm.** The load-bearing meetings, per
  team (chapter 07 lists them at 15-50):
  - **Weekly planning / kanban replenish** —
    Monday, 30-60 minutes, owned by the EM (or
    tech lead at 5-15).
  - **Weekly cadence-metrics reading** — end of
    weekly planning, 5-15 minutes. The four DORA
    numbers (from [exercise 05](exercise-05-dora-four-key-measurement-plan.md))
    and open post-mortem action items.
  - **Weekly retro** — Friday (or the team's
    last working day), 30-45 minutes. Blameless
    ethos (cite
    [www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems)).
  - **Weekly team-lead / EM sync** — 30 minutes.
    Cross-functional alignment.
  - Name the total meeting load per engineer per
    week. Chapter 07's rule of thumb: under 5
    hours. If your rhythm exceeds it, flag the
    trade-off explicitly.
- **Three-loop planning cadence.**
  - **Sprint / iteration** — weekly or
    two-weekly, depending on the kanban-vs-sprint
    call.
  - **Roadmap review** — every 2-6 weeks, with
    product / design and the CTO / VP Eng.
  - **Quarterly planning** — one-to-two-day
    event, all engineering leads plus product /
    design plus CEO. Output: a written next-
    quarter roadmap per team with cross-team
    dependencies surfaced.
  - **Annual planning / budget cycle** — pointer
    to
    [exercise 03 artifact 4](exercise-03-fifteen-to-fifty-first-em-and-platform-team.md)
    for the 15-50 initial budget and to
    [`mod-108`](../../mod-108-cto-ceo-and-board-communication/README.md)
    for the CFO conversation shape.
- **Kanban-vs-sprint call.** Which one your team is
  running and why. Cite either
  [leankanban.com/kanban-books](http://leankanban.com/kanban-books/)
  (Anderson) or the current
  [scrumguides.org](https://scrumguides.org/) or
  both. Chapter 07's rule of thumb: kanban when
  bursty / small / heterogeneous, sprint when
  predictable / cross-functional / larger. If your
  org runs *both* — some teams kanban, some sprint
  — name the per-team choice and the reason.
- **The DORA-cadence tie.** One paragraph on where
  the DORA numbers show up in the weekly rhythm
  (the weekly cadence-metrics reading), and the
  rule for how a moved number becomes a
  conversation (see [exercise 05](exercise-05-dora-four-key-measurement-plan.md)).
- **What is NOT a standing meeting.** 3-4 bullets.
  Guard against meeting sprawl — cross-team
  syncs that could be async, status meetings that
  duplicate the standup, etc.

### Artifact 2 — On-call rotation

`on-call/README.md` — one page. Sections:

- **Stage.** The team's current stage. If 5-15,
  reference the [exercise 02](exercise-02-five-to-fifteen-transition-playbook.md)
  version. If 15-50 or 50-150, this file *extends*
  the 5-15 version.
- **Rotation shape.**
  - **Per-team rotation** at 15-50 (each team
    on-call for the services it owns). Named.
  - **Follow-the-sun** at 50-150 if the org has
    engineers in multiple time zones. Named,
    with the timezone bands.
- **Roster.** 4-6 engineers per rotation (or per
  team-per-region, at 50-150 follow-the-sun).
  Named or role-played.
- **Primary / secondary / manager escalation.**
  Ack windows (chapter 07 default: 15 minutes for
  the primary, then secondary, then the team's
  EM). The CTO / VP Eng is NOT in the primary
  escalation path.
- **Rotation cadence.** Weekly, Friday-to-Friday.
- **Handoff.** 15 minutes on Friday, using the
  `handoff-template.md`.
- **Comp.** Pointer to `on-call/comp.md`.

`on-call/page-path.md` — the operational path:

- **What pages.** Named alerts and criteria —
  customer-visible outage, specific dashboard
  threshold, SLO burn-rate breach (see
  [sre.google/workbook/alerting-on-slos](https://sre.google/workbook/alerting-on-slos/)).
- **What does NOT page.** Named non-actionable
  events — log warnings, non-critical dashboard
  changes.
- **Vendor.** PagerDuty
  ([pagerduty.com](https://www.pagerduty.com/)),
  Opsgenie
  ([atlassian.com/software/opsgenie](https://www.atlassian.com/software/opsgenie)),
  incident.io ([incident.io](https://incident.io/)),
  Grafana OnCall
  ([grafana.com/products/oncall](https://grafana.com/products/oncall/)),
  or FireHydrant
  ([firehydrant.com](https://firehydrant.com/)).
  Named.
- **The alert-curation loop.** Every alert that
  fires goes through a review at the weekly retro
  or the post-mortem. Non-actionable alerts get
  tuned or removed. Chapter 07's alert-storm
  anti-pattern is the failure mode this loop
  guards against.

`on-call/handoff-template.md` — the weekly handoff
document template (as in
[exercise 02](exercise-02-five-to-fifteen-transition-playbook.md)):

- **Open incidents** with current status and next
  action.
- **Ongoing issues** — non-page-worthy but worth-
  watching.
- **Follow-ups** — post-mortem action items whose
  owner is on the outgoing rotation.
- **Contacts** — customer or partner escalation
  points.

`on-call/comp.md` — one paragraph:

- **The stipend, extra PTO, or comp adjustment.**
  Name the number (or the range), tied to the
  comp band from
  [`mod-104` chapter 06](../../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md).
  Chapter 07's unpaid-rotation anti-pattern is
  the failure mode this comp doc guards against.
- **Who is exempt** (usually managers at some
  tiers) and why.

`on-call/runbook-convention.md` — one page:

- **The rule** — every service has a `runbooks/`
  directory (in the repo or in the service
  catalogue) with troubleshooting steps for
  common alerts.
- **The template** — for each alert: symptom,
  first-check, likely-causes, mitigation,
  escalation.
- **The link from page to runbook.** Every
  pageable alert has a runbook link in the alert
  payload (chapter 07 assumption; the SRE-book
  guidance at
  [sre.google/sre-book/practical-alerting](https://sre.google/sre-book/practical-alerting/)).
- **Where runbooks live.** In the service
  catalogue (Backstage at
  [backstage.io](https://backstage.io/) or the
  commercial equivalents from
  [exercise 06](exercise-06-platform-investment-sizing-per-stage.md))
  or in the service repo.

### Artifact 3 — Blameless post-mortem template

`on-call/post-mortem/template.md` — one page. The
six-section template from chapter 02 artifact 3 and
chapter 07:

- **What happened.** User-visible impact, with
  times.
- **Timeline.** Detection, first response,
  mitigation, resolution. Facts only.
- **Root cause(s).** Plural. Asserting exactly one
  cause is a warning sign — cite Sidney Dekker's
  *The Field Guide to Understanding 'Human
  Error'*
  ([sidneydekker.com](https://sidneydekker.com/books/))
  on why single-cause narratives are usually
  wrong.
- **What went well.** Named.
- **What went badly.** Named. **Attributed to the
  system, not the individual on call.** The
  template's language should push a reader in
  that direction — e.g., a placeholder such as
  *"the [system / process / tool] did [not] X"*
  rather than *"the on-call engineer did / did
  not Y"*. See John Allspaw — *Blameless
  PostMortems and a Just Culture* (Etsy, 2012) —
  [www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems).
- **Action items.** Owned. Dated. Landed in the
  backlog with the same priority weight as
  feature work (chapter 07 15-50 discipline).

Plus the *published-to-the-team* discipline note —
the post-mortem is posted to the eng org, not left
in a private folder — and a pointer to
[sre.google/sre-book/postmortem-culture](https://sre.google/sre-book/postmortem-culture/).

`on-call/post-mortem/archive/README.md` — a short
convention document:

- One file per incident, named
  `YYYY-MM-DD-short-slug.md`.
- The archive is public within the eng org.
- Every action item in every post-mortem is
  cross-linked into the tech-debt inventory
  ([`mod-105` chapter 06](../../mod-105-technical-debt-as-business-decision/06-debt-inventory-and-portfolio-decision-log.md))
  if it is a debt item, or into the team's
  regular backlog if it is a fix.

### Artifact 4 — Incident-response playbook

`on-call/incident-response.md` — one page. The
*"what happens when a page fires"* runbook. Three
sections:

- **Triage** — the primary's first ten minutes.
  Acknowledge the page. Assess the impact
  (customer-visible? scoped to one tenant / a
  region / the whole surface? data-loss risk?
  security implication?). Decide whether to
  declare an incident. The decision rule:
  named, and cite one of PagerDuty's public
  guidance
  ([response.pagerduty.com](https://response.pagerduty.com/))
  or the Google SRE book chapter on managing
  incidents
  ([sre.google/sre-book/managing-incidents](https://sre.google/sre-book/managing-incidents/)).
- **Response** — if an incident is declared:
  open the incident channel (per your vendor
  choice from `on-call/page-path.md`); page
  the **incident commander** at 50-150 (the
  incident-command-system pattern from the SRE
  book — incident commander, communications
  lead, operations lead); start the incident
  timeline; coordinate the response.
- **Resolution** — once service is restored:
  close the incident; publish the customer-
  facing status update if applicable; **schedule
  the post-mortem calendar hold *before*
  closing the incident**. Chapter 07's 15-50
  discipline is that the calendar hold exists
  by the time the primary declares the incident
  resolved.

Plus:

- **Severity levels.** Sev-1 / Sev-2 / Sev-3 (or
  your naming convention). Named criteria per
  level. Sev-1 is *"customer-visible outage of
  the core product"* or the equivalent.
- **The customer-communication rule.** When and
  how customers get notified. If you have a
  public status page (Statuspage
  [statuspage.io](https://www.statuspage.io/) or
  equivalent), the update rule. If you have
  paid customers with SLA contracts, the
  contact / escalation path.
- **The security-incident divergence.** Named. A
  security-triggered incident escalates
  differently — see
  [`mod-107`](../../mod-107-founder-scope-security-and-compliance/README.md)
  for the CTO-scope security-incident playbook.
  A one-sentence pointer is enough here.
- **The debt / DORA loop.** One paragraph on
  the closed loop: incident → post-mortem →
  debt item ([`mod-105` chapter 06](../../mod-105-technical-debt-as-business-decision/06-debt-inventory-and-portfolio-decision-log.md))
  → refactor budget ([`mod-105` chapter 04](../../mod-105-technical-debt-as-business-decision/04-refactor-budget-tied-to-roadmap.md))
  → DORA numbers ([exercise 05](exercise-05-dora-four-key-measurement-plan.md))
  → weekly cadence reading. Chapter 07's summary
  section describes this loop; the playbook is
  where it lands operationally.

## Starter guidance

- **Extend the 5-to-15 artifacts if they exist.**
  If your working repo has the [exercise 02](exercise-02-five-to-fifteen-transition-playbook.md)
  on-call rotation and post-mortem template, this
  exercise adds the 15-50 or 50-150 deltas —
  per-team rotation, incident-command system,
  runbook-per-service, SLI / SLO error-budget
  policy. Do not duplicate.
- **The kanban-vs-sprint call is per-team, not
  org-wide.** Chapter 07's failure mode is the
  CTO who mandates *"we all do two-week
  sprints"*. Two teams whose work shapes are
  legitimately different should choose
  differently. If your cadence spec says
  *"the whole org runs sprints"* without a
  team-by-team defence, revise.
- **The comp doc is where the honesty check
  lands.** *"On-call comp TBD"* is not comp; it
  is the absence of a rotation. The unpaid-
  rotation anti-pattern (chapter 07) is the
  failure mode. Set a number, tied to the
  comp band from
  [`mod-104` chapter 06](../../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md).
- **The blameless post-mortem template's
  discipline is in the language.** Read
  [www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems)
  and Sidney Dekker's *The Field Guide to
  Understanding 'Human Error'*
  ([sidneydekker.com](https://sidneydekker.com/books/))
  before authoring the template. The template
  should nudge a reader toward system-attribution
  even when the underlying incident had a human
  proximate cause. If a reader could infer
  *"whose fault is this"* from your template
  headings and placeholder text, revise.
- **The incident-response playbook's discipline
  is that the post-mortem calendar hold is
  created *during* the incident.** Not *"we
  will schedule the post-mortem after the
  incident closes"* — the hold exists on the
  calendar by the time the incident is
  resolved. If the hold does not exist, the
  post-mortem does not happen (chapter 07
  15-50 discipline).
- **The runbook-per-service discipline is the
  50-150 differentiator.** At 5-15 you can get
  away with tribal knowledge. At 50-150 you
  cannot — the primary who wakes up at 3am on
  a service they have never seen before needs
  a runbook. Name the rule (*"no page-worthy
  alert exists without a runbook link in the
  payload"*) and enforce it in the alert-
  curation loop.
- **The four artifacts read as a system.** The
  cadence spec references the on-call rotation
  (which team owns which services); the on-call
  rotation references the runbook convention;
  the incident-response playbook references the
  post-mortem template; the post-mortem
  template references the debt inventory. Read
  them together after authoring — a reader
  should be able to trace the loop from *"page
  fires"* to *"debt item lands in the
  portfolio"* without leaving your directory.
- **Bundle the Google SRE book / workbook
  chapters into one canonical reading list in
  `docs/on-call/README.md`.** The four artifacts
  touch five different SRE chapters —
  [*Being On-Call*](https://sre.google/sre-book/being-on-call/),
  [*Practical Alerting*](https://sre.google/sre-book/practical-alerting/),
  [*Alerting on SLOs*](https://sre.google/workbook/alerting-on-slos/),
  [*Managing Incidents*](https://sre.google/sre-book/managing-incidents/),
  and [*Postmortem Culture*](https://sre.google/sre-book/postmortem-culture/).
  List them once at the top of the rotation
  README as the operational substrate's
  canonical reading rather than scattering the
  citations across the four artifact files. The
  full
  [*Site Reliability Workbook* table of contents](https://sre.google/workbook/table-of-contents/)
  is the one place to orient from if your team
  decides to lift more than the listed
  chapters.
- **The incident-command system (ICS) pattern in
  the SRE book is borrowed from the fire-service
  ICS, not invented by Google.** Chapter 07
  notes this explicitly; the exercise's
  `incident-response.md` benefits from citing
  the upstream primary alongside
  [*Managing Incidents*](https://sre.google/sre-book/managing-incidents/)
  so the pattern is not read as a Google-
  specific invention. FEMA's National Incident
  Management System ([FEMA NIMS](https://www.fema.gov/emergency-managers/nims))
  is the current-day keeper of the ICS
  specification; the IS-100 training ("ICS-100 —
  Introduction to the Incident Command System")
  is the common entry-level reading.
  <!-- needs-research: the canonical primary
  source the SRE book is adapting from. The SRE
  book's *Managing Incidents* chapter cites the
  fire-service ICS without pinning a specific
  FEMA / NIMS revision; confirm the specific
  primary URL (FEMA NIMS program, IS-100
  training, or an older US Forest Service /
  ICS-SG original) before writing it into the
  playbook. -->
- **The 15-minute primary-ack default is a
  chapter 07 convention, not a sourced
  universal.** Artifact 2 pins the primary ack
  window at 15 minutes, with the secondary and
  then the EM as subsequent steps. Neither the
  SRE book nor the public vendor playbooks
  mandate a specific number — the window is
  calibrated against the service's SLO burn
  rate and the team's after-hours tolerance.
  Name your number in `on-call/README.md` and
  tie it to the SLO burn-rate math from
  [*Alerting on SLOs*](https://sre.google/workbook/alerting-on-slos/)
  rather than citing it as a universal.
  <!-- needs-research: a sourced primary
  reference for the 15-minute primary-ack
  default. The chapter cites 15 minutes as a
  rule of thumb; the common sources (the SRE
  book's *Being On-Call* chapter, PagerDuty's
  [response.pagerduty.com](https://response.pagerduty.com/)
  playbook) do not pin a specific number. -->
- **Position the three post-mortem references by
  depth so the template-authoring step does not
  scatter searches.** The exercise cites three
  canonical references for the blameless
  template — Allspaw's Etsy post
  ([www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems)),
  the Google SRE book chapter on post-mortem
  culture
  ([sre.google/sre-book/postmortem-culture](https://sre.google/sre-book/postmortem-culture/)),
  and Sidney Dekker's *The Field Guide to
  Understanding 'Human Error'*
  ([sidneydekker.com/books](https://sidneydekker.com/books/)).
  These are not interchangeable: Allspaw is the
  short-read that establishes the just-culture
  framing; the SRE-book chapter is the
  operational discipline (template, action-item
  tracking, publication discipline); Dekker is
  the book-length deep read on why single-cause
  narratives mislead. Read in that order so the
  template-authoring step does not copy the
  template without the framing that makes the
  template work.
- **Link `dora.dev/research` as the external
  anchor for the weekly cadence-metrics
  reading.** Artifact 1 ties the four DORA
  numbers to the weekly rhythm. The external
  anchor for that discipline — the one the
  reader of your cadence spec will want to see
  — is the DORA research program at
  [dora.dev/research](https://dora.dev/research/),
  the home of the annual *Accelerate State of
  DevOps* report and the elite / high / medium /
  low performance cutoffs. Cite it next to the
  pointer to
  [exercise 05](exercise-05-dora-four-key-measurement-plan.md)
  in `planning/cadence.md` so the external
  primary is one click away from the cadence
  spec.

## Acceptance criteria

Your drill output is complete when:

- The `docs/planning/cadence.md` and
  `docs/on-call/` files exist in the shape above.
- The cadence spec names the total per-engineer
  meeting load per week (with the chapter 07
  rule of thumb), the three-loop planning
  cadence, the kanban-vs-sprint call with a
  cited reference, and the DORA-cadence tie.
- The on-call rotation names the rotation shape
  for your stage (per-team at 15-50, follow-
  the-sun with time-zone bands at 50-150), a
  named roster of 4-6 engineers, primary /
  secondary / manager escalation with ack
  windows, a named vendor, and a real comp
  number (not a placeholder).
- The runbook convention names the rule that
  every page-worthy alert has a runbook link,
  the runbook template, and where runbooks
  live.
- The blameless post-mortem template's
  *what-went-badly* section attributes to the
  system, not the individual. If a reader
  could infer whose fault the incident is
  from the template, revise.
- The incident-response playbook names
  severity levels with criteria, the
  triage / response / resolution flow, the
  incident-commander role at 50-150, the
  customer-communication rule, the security-
  incident divergence pointer to
  [`mod-107`](../../mod-107-founder-scope-security-and-compliance/README.md),
  and the debt / DORA loop.
- The post-mortem calendar-hold-before-close
  discipline is stated in both the incident-
  response playbook and the post-mortem
  template's process notes.
- The four artifacts cross-reference each
  other where they naturally should. A reader
  can trace the loop from page → response →
  post-mortem → debt item → refactor budget →
  DORA reading without leaving your directory
  sub-tree.
- The four artifacts can be handed to a new
  hire on their first day and they can execute
  a rotation cycle plus a simulated post-
  mortem without a follow-up round of
  clarifications.

## What this feeds into

- **The lab** — the four artifacts land in the
  `docs/scaling/` runbook as the operational
  substrate the other stage-transition slices
  execute against.
- **`mod-107`** — the on-call rotation, the
  incident-response playbook, and the
  blameless-post-mortem practice are the
  operational substrate the SOC 2 Type I
  readiness checks
  ([`mod-107`](../../mod-107-founder-scope-security-and-compliance/README.md))
  rely on.
- **`mod-108`** — the DORA numbers, the
  delivery-cadence spec, and the incident-
  response practice land in the board pre-read
  and the technical-DD data room
  ([`mod-108`](../../mod-108-cto-ceo-and-board-communication/README.md)).
- **`mod-105`** — every post-mortem's action
  items land in the tech-debt inventory
  ([`mod-105` chapter 06](../../mod-105-technical-debt-as-business-decision/06-debt-inventory-and-portfolio-decision-log.md));
  the refactor budget
  ([`mod-105` chapter 04](../../mod-105-technical-debt-as-business-decision/04-refactor-budget-tied-to-roadmap.md))
  funds the remediation; the DORA numbers
  ([exercise 05](exercise-05-dora-four-key-measurement-plan.md))
  are the aggregate signal.

The delivery-cadence and on-call exercise is where
the CTO writes down how the team executes and how
it responds when things break. If any of the four
artifacts feels like *"we will figure this out the
first time it happens"*, the exercise has not yet
forced the discipline; go back and finish it. The
on-call rotation without a written runbook, the
incident without a scheduled post-mortem, and the
post-mortem without a debt-item link are the three
places the loop most-often breaks — and the
artifact's job is to keep the loop closed.
