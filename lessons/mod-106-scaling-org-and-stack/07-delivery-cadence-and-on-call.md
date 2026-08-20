# Delivery Cadence, On-Call, and Incident Response

> "The delivery cadence is the metronome the org
> executes to; the on-call rotation is the org's
> immune system; the incident-response playbook is
> the muscle memory that keeps the immune system
> from panicking. A team that inherits all three as
> written artifacts can run without the CTO in the
> room. A team that runs on tribal knowledge cannot."

## Motivation

The prior chapters have covered the *shape* of the org
at each stage transition (chapters 01-04), the DORA
measurement (chapter 05), and the platform-investment
sizing (chapter 06). This chapter is the operational
substrate — the concrete rituals, rotations, and
playbooks that the team executes week after week — so
that the shape and the metrics translate into
predictable delivery and reliable service.

Three artifacts do the work at this level:

1. The **delivery-cadence spec** — the weekly rhythm,
   the planning cadence, the kanban-vs-sprint call.
2. The **on-call rotation design** — the page path,
   the escalation, the comp, the handoff, the
   evolution from 5-15 to 50-150.
3. The **incident-response playbook and blameless
   post-mortem template** — the muscle memory that
   turns an incident into a bounded event with a
   learning outcome.

The chapter's discipline: **each of the three artifacts
is a written document in the working repo**. Nobody
has to remember them; the artifact is the memory. When
a new hire joins, they read the three documents on
their first day and are then a functioning member of
the team without any tribal on-boarding.

## Artifact 1 — The delivery-cadence spec

The delivery cadence at 5-15 engineers has already
been introduced (chapter 02 artifact 5). The 15-50 and
50-150 evolutions add complexity that is worth naming
explicitly.

### The weekly rhythm

The load-bearing meetings at 15-50, per team:

- **Weekly planning / kanban replenish.** 30-60
  minutes on Monday. The team reviews the last
  week's completion, groom the next week's work,
  and re-confirm the top-of-list priorities. Owned
  by the EM (chapter 03 artifact 1).
- **Weekly cadence-metrics reading.** 5-15 minutes,
  usually at the end of the weekly planning. The
  four DORA numbers (chapter 05) and any open
  post-mortem action items. The point is not
  discussion; it is *visibility*. Discussion happens
  when a number moves.
- **Weekly retro.** 30-45 minutes on Friday (or the
  team's last working day). Not a status meeting;
  a *"what worked, what didn't, what to change"*
  meeting. The Etsy blameless-postmortems ethos
  ([www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems))
  extends here: the retro is blameless; the point
  is system change, not individual attribution.
- **Weekly team-lead / EM sync.** 30 minutes. The
  tech lead(s), the EM, and any product /
  design partner. Cross-functional alignment for
  the week.

The 5-15 team collapses several of these into fewer
meetings; the 50-150 team may split them further. The
principle: **each meeting has a distinct outcome, and
the total meeting load per engineer stays under 5
hours per week**. Over that, the team's flow is being
eroded (see the SPACE / DevEx frames in chapter 05).

### The planning cadence at team and org levels

The 5-15 three-loop cadence (weekly, every-2-to-6-weeks,
quarterly) extends at 15-50 and 50-150 to:

- **Sprint / iteration** at the team level (weekly or
  two-weekly, depending on the kanban-vs-sprint call).
- **Roadmap review** at the team level (every 2-6
  weeks, with product / design and the CTO / VP Eng
  attending).
- **Quarterly planning** at the org level (a
  one-to-two-day planning event, all engineering
  team leads plus product / design plus CEO). The
  outcome is a written next-quarter roadmap per team
  with cross-team dependencies surfaced (chapter 04
  artifact 4).
- **Annual planning / budget cycle** at the CTO / VP
  Eng level (chapter 03 artifact 4).

### Kanban vs. sprint — the call

At 5-15 engineers most teams do kanban (continuous
flow, WIP limits, no fixed iteration). At 15-50 some
teams shift to sprints (usually two-weekly Scrum-
adjacent). At 50-150 the org is usually a mix — some
teams kanban, some sprint — driven by the team's
work-shape rather than an org-wide standard.

The two references worth having open:

- **David Anderson — *Kanban: Successful Evolutionary
  Change for Your Technology Business*** —
  [leankanban.com/kanban-books](http://leankanban.com/kanban-books/).
  The load-bearing reference on the kanban discipline
  (WIP limits, pull-based flow, class of service).
- **The 2020 Scrum Guide** —
  [scrumguides.org](https://scrumguides.org/) —
  the current Scrum reference (16 pages, deliberately
  short). Free.

The rule of thumb:

- **Kanban when** the work is bursty (a lot of
  reactive customer work, unpredictable
  prioritization), the team is small (under 8), or
  the work items are heterogeneous in size.
- **Sprint when** the work is predictable, the team
  benefits from a synchronization ceremony (a
  cross-functional team with product / design /
  engineering all needing to align on a release), or
  the team is large enough (8+) that the WIP limits
  alone are not producing coordination.

The failure mode: forcing an org-wide standard. Two
teams whose work shapes are legitimately different
should not both be doing the same cadence just because
consistency is aesthetically pleasing. The 15-50 CTO
who mandates *"we all do two-week sprints"* usually
finds two teams thrashing and moves back to per-team
choice within a quarter.

### The DORA-cadence tie

The delivery cadence is the ritual that surfaces the
DORA numbers (chapter 05). Concretely, the weekly
cadence-metrics reading is the point at which the
team notices that Lead Time has doubled or Change
Failure Rate has climbed. Without the ritual, the
numbers are dashboards nobody looks at.

## Artifact 2 — The on-call rotation design

The on-call rotation at 5-15 engineers has already been
introduced (chapter 02 artifact 2). The 15-50 and
50-150 evolutions:

### The 15-50 rotation

Usually:

- **Per-team rotation.** Each team has its own on-call
  rotation for the services it owns. A single org-wide
  rotation stops scaling once there are more than 3-4
  teams; a per-team rotation aligns responsibility
  with ownership.
- **Primary / secondary / manager escalation.** The
  primary is paged first; the secondary is paged if
  the primary does not ack within 15 minutes; the
  team's EM is paged if the secondary does not ack.
  The CTO / VP Eng is *not* in the primary escalation
  path.
- **Weekly rotation, with the handoff document.**
  Same as at 5-15, extended.
- **Explicit on-call comp.** Formalised: a stipend,
  extra PTO, or a comp adjustment. See
  [`mod-104` chapter 06](../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md)
  for the comp-band shape.

### The 50-150 rotation

Adds:

- **Follow-the-sun rotation** if the org has
  engineers in multiple time zones. Reduces the
  after-hours page load per engineer, which is the
  single strongest predictor of on-call burnout.
- **Incident commander / on-call commander role**
  for larger incidents. See the incident-response
  playbook below.
- **Runbook-per-service discipline.** Every service
  has a `runbooks/` directory in the repo (or the
  service catalogue) with the specific
  troubleshooting steps for common alerts.
- **SLI / SLO / error-budget policy.** The on-call
  page volume is bounded by the error-budget policy
  from the Google SRE workbook
  ([sre.google/workbook/table-of-contents](https://sre.google/workbook/table-of-contents/)).
  Concretely: if the service is meeting its SLO, the
  team ships features; if the service is burning its
  error budget, the team stops shipping features and
  fixes the reliability issue.

### On-call anti-patterns

Named explicitly:

- **The hero rotation.** One senior engineer takes
  most of the pages; the rest of the team never
  develops the operational muscle. When the hero
  leaves (chapter 03 artifact 5), the team is
  helpless. Remedy: rotate deliberately, including
  the CTO / VP Eng on early rotations to build the
  rotation-as-a-norm.
- **The unpaid rotation.** Operational responsibility
  is a tax on the conscientious. See chapter 02.
- **The rotation with no runbook.** The primary
  wakes up at 3am, does not know what to do, pages
  the secondary. See the incident-response playbook
  below.
- **The alert-storm rotation.** The pager fires
  every hour on non-actionable alerts. Team
  develops alert fatigue and starts ignoring pages.
  Remedy: rigorous alert curation, driven by the
  post-mortem action items and the SRE book's
  *Practical Alerting from Time-Series Data*
  ([sre.google/sre-book/practical-alerting](https://sre.google/sre-book/practical-alerting/)).

### Vendor / tool decisions

The common vendors for the paging path:

- **PagerDuty** —
  [pagerduty.com](https://www.pagerduty.com/) —
  the incumbent, most widely used at 15-50 and
  above.
- **Opsgenie** —
  [atlassian.com/software/opsgenie](https://www.atlassian.com/software/opsgenie)
  — the Atlassian-suite alternative.
- **incident.io** —
  [incident.io](https://incident.io/) — combines
  paging with incident-management workflow (Slack
  integration, incident channels, status updates).
- **Grafana OnCall** —
  [grafana.com/products/oncall](https://grafana.com/products/oncall/)
  — open-source-adjacent, often paired with a
  Grafana observability stack.
- **FireHydrant** —
  [firehydrant.com](https://firehydrant.com/) —
  incident-management platform.

Which vendor is a minor decision at each stage. The
important discipline is that the page path is written
down and everyone on the rotation knows it.

## Artifact 3 — Incident-response playbook and blameless post-mortem template

The incident-response playbook is the *"what happens
when a page fires"* document. It has three sections:

- **Triage.** The primary's first ten minutes.
  Acknowledge the page, assess the impact, decide
  whether to declare an incident.
- **Response.** If an incident is declared: open the
  incident channel, page the incident commander (at
  50-150), start the incident timeline, coordinate
  the response.
- **Resolution.** Once service is restored: close the
  incident, publish a customer-facing update if
  applicable, schedule the post-mortem within 48
  hours.

The load-bearing reference on the mechanics is the
Google SRE book chapter on **managing incidents** —
[sre.google/sre-book/managing-incidents](https://sre.google/sre-book/managing-incidents/).
The chapter is short (a few pages) and describes the
*incident command system* pattern (borrowed from the
fire-service ICS) — incident commander, communications
lead, operations lead — that becomes load-bearing at
50-150.

Two other references worth having open:

- **PagerDuty's incident-response documentation** —
  [response.pagerduty.com](https://response.pagerduty.com/) —
  publicly-published, one of the most-copied
  playbooks in the industry.
- **Google's *Site Reliability Workbook* chapter on
  managing incidents** —
  [sre.google/workbook/managing-incidents](https://sre.google/workbook/incident-response/).

### The blameless post-mortem template

Repeats chapter 02 artifact 3 for reference:

- **What happened.** User-visible impact, with times.
- **Timeline.** Detection, first response, mitigation,
  resolution. Facts.
- **Root cause(s).** Plural. Asserting exactly one
  cause is a warning sign.
- **What went well.** Named.
- **What went badly.** Named. Attributed to the
  *system*, not the individual on call.
- **Action items.** Owned. Dated. Landed in the
  backlog with the same priority weight as feature
  work.

Load-bearing references, repeated for the operational
context:

- Google SRE book chapter on **post-mortem culture** —
  [sre.google/sre-book/postmortem-culture](https://sre.google/sre-book/postmortem-culture/).
- John Allspaw — *Blameless PostMortems and a Just
  Culture* (Etsy, 2012) —
  [www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems).
- Sidney Dekker — *The Field Guide to Understanding
  'Human Error'* —
  [sidneydekker.com](https://sidneydekker.com/books/).

The 15-50 discipline: **the post-mortem is scheduled
before the incident is closed**. Not "we should do
one"; the calendar hold exists by the time the primary
declares the incident resolved. If the calendar hold
does not exist, the post-mortem does not happen.

The 50-150 discipline: **the post-mortem action items
have the same tracking as feature work**. A separate
tracker for post-mortem actions produces a separate
priority queue that the team deprioritises the moment
feature pressure rises. Merge them.

## Closing the loop — from incident to debt to DORA

The three-artifact system closes a loop that the
[`mod-105`](../mod-105-technical-debt-as-business-decision/README.md)
debt-portfolio work and the DORA measurement
(chapter 05) both feed into:

- **An incident** happens. The blameless post-mortem
  identifies a set of action items. Some of these
  are cheap fixes; others are debt items (chapter
  05).
- **The debt items** land in the tech-debt inventory
  from
  [`mod-105` chapter 06](../mod-105-technical-debt-as-business-decision/06-debt-inventory-and-portfolio-decision-log.md).
  Their cost-to-carry is sized against the on-call
  and MTTR taxes they impose.
- **The DORA numbers** — specifically Change Failure
  Rate and MTTR — are the aggregate signal that the
  debt portfolio's on-call carry cost is or is not
  being paid down.
- **The refactor budget** (from
  [`mod-105` chapter 04](../mod-105-technical-debt-as-business-decision/04-refactor-budget-tied-to-roadmap.md))
  funds the highest-priority repayment work.
- **The delivery cadence** (this chapter) is the
  ritual that keeps the loop closed. The weekly
  cadence-metrics reading is the check that the
  loop is running.

Without the delivery cadence and the on-call rotation,
the debt-portfolio work becomes theoretical. Without
the debt portfolio, the incident-response work
becomes reactive. Without the DORA measurement,
neither can be defended in front of the CFO or the
board. The three modules are a system, not
independent.

## Summary

- **Delivery cadence** — the weekly rhythm (planning,
  cadence-metrics reading, retro, team-lead sync),
  the three-loop planning cadence (sprint / roadmap /
  quarterly), and the kanban-vs-sprint call. Rule of
  thumb: kanban for bursty work / small teams;
  sprint for predictable work / cross-functional
  synchronization. Anti-pattern: forcing an org-wide
  standard.
- **On-call rotation** — per-team at 15-50, follow-
  the-sun at 50-150, with primary / secondary /
  manager escalation. Explicit comp. Runbook per
  service. SLI / SLO / error-budget policy at 50-150.
  Load-bearing references: Google SRE book chapter
  on *Being On-Call*
  ([sre.google/sre-book/being-on-call](https://sre.google/sre-book/being-on-call/))
  and *Practical Alerting*
  ([sre.google/sre-book/practical-alerting](https://sre.google/sre-book/practical-alerting/)).
  Anti-patterns: hero rotation, unpaid rotation,
  no-runbook rotation, alert-storm rotation.
- **Incident-response playbook** — triage,
  response, resolution. Incident command system
  ([sre.google/sre-book/managing-incidents](https://sre.google/sre-book/managing-incidents/))
  at 50-150. PagerDuty's public playbook at
  [response.pagerduty.com](https://response.pagerduty.com/)
  is a load-bearing reference to adapt from.
- **Blameless post-mortem** — one-page template
  (what happened / timeline / root causes / what
  went well / what went badly / action items).
  Post-mortem calendar hold scheduled before the
  incident is closed. Action items tracked in the
  same backlog as feature work.
- **The closed loop** — incident → post-mortem →
  debt item ([`mod-105` chapter 06](../mod-105-technical-debt-as-business-decision/06-debt-inventory-and-portfolio-decision-log.md))
  → refactor budget ([`mod-105` chapter 04](../mod-105-technical-debt-as-business-decision/04-refactor-budget-tied-to-roadmap.md))
  → DORA numbers (chapter 05) → weekly cadence
  reading. The three modules are a system.

The chapter's paired exercise —
[`exercise-07-delivery-cadence-and-on-call-design.md`](exercises/exercise-07-delivery-cadence-and-on-call-design.md)
— asks you to author a delivery-cadence spec, an
on-call rotation v1, a blameless post-mortem
template, and an incident-response playbook as a
single `docs/on-call/` sub-tree in the working repo.

This is the last chapter of the module. The
[`README.md`](README.md) lists the exercises, the lab,
and the pointers to the adjacent modules
([`mod-107`](../mod-107-founder-scope-security-and-compliance/README.md)
and
[`mod-108`](../mod-108-cto-ceo-and-board-communication/README.md))
that build on this substrate.
