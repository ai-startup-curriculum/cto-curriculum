# The 5→15 Transition — First Tech Lead, On-Call, RFCs, Handbook

> "The point at which the small-team-invisibility of the
> missing process gives out." The 5→15 transition is
> when the team is no longer small enough for *"whoever
> is closest to the problem fixes it"* to work, and the
> CTO has to write down — for the first time — how the
> team makes decisions, how it responds to incidents,
> and how it onboards someone who wasn't there when the
> team formed.

## Motivation

At five engineers the room is small enough that the
missing structure is invisible. At fifteen engineers it
is loud. Concretely, three things break simultaneously
around engineer #8 to #10:

- **The CTO stops being the reviewer of every PR.** The
  volume outstrips one person, and the reviews the CTO
  does get to are slower and shallower than they used
  to be.
- **The first customer incident happens at a time when
  the CTO is not looking at their phone.** Nobody has a
  written escalation path. The customer waits four
  hours for a response that would have been fifteen
  minutes if there were a rotation.
- **A new hire asks a question that has been answered
  in Slack six times over the last year, and nobody can
  find the answer.** The tribal knowledge that runs the
  five-person team does not survive the five-to-fifteen
  transition.

Each of these is a symptom of the same underlying gap:
the team is still operating on the process shape of
5 engineers with 10-15 people in the room. The 5→15
transition is the work of installing the *smallest set
of written mechanisms* that lets the team run without
the CTO being the substrate for every decision.

Six artifacts do the work at this stage, and this
chapter walks them in the order they usually appear:
tech-lead role, on-call rotation, blameless post-mortem
practice, RFC process, planning cadence, and engineering
handbook.

## Artifact 1 — The first tech lead

The first tech lead is the CTO's first *technical*
delegation. The mechanics of the promote-vs-hire
decision are covered in
[`mod-104` chapter 05](../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md);
this chapter's contribution is what changes about the
*org shape* when the tech lead is in place.

Three concrete deltas:

- **The tech lead owns the reviews for their slice.**
  The CTO is no longer the reviewer of last resort for
  that slice. Design decisions that used to go to the
  CTO now go to the tech lead; the CTO reviews the
  tech lead's designs, not every design.
- **The tech lead runs the first RFC for their slice
  end-to-end.** Not the CTO with the tech lead
  observing. See artifact 4 below.
- **The tech lead is the on-call escalation for their
  slice.** Not the CTO. If the on-call primary can't
  handle the incident, the tech lead is paged next.
  See artifact 2.

The tech lead is *not* a manager at this stage. They
do not do 1:1s, hiring loops, or performance reviews.
Fournier's *The Manager's Path*
([oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/))
distinguishes the technical-lead role from the
engineering-manager role explicitly, and the 5→15
version of the role is the *"lead engineer of a slice"*
variant — the responsibility is the technical direction
of a subsystem, not the humans who work on it.

The role charter should be a one-page written document
in the engineering handbook (artifact 6). See the
exercise for the concrete template.

## Artifact 2 — The first on-call rotation

The trigger for the first on-call rotation is not
headcount. It is the **first customer incident that
happened at a time when the CTO was not looking at their
phone**. If you can name that incident and it was more
than a month ago, you are late.

The 5-15 on-call rotation is small — usually 4-6 engineers
on a weekly rotation, with the tech lead(s) as
secondary. Google's *Site Reliability Engineering* book
([sre.google/sre-book](https://sre.google/sre-book/table-of-contents/))
is the canonical reference for the operational shape;
the *"being on-call"* chapter
([sre.google/sre-book/being-on-call](https://sre.google/sre-book/being-on-call/))
is the load-bearing read.

Five design decisions the first rotation has to make:

- **Page path.** How does an alert (or a customer email)
  become a page on someone's phone? PagerDuty
  ([pagerduty.com](https://www.pagerduty.com/)),
  Opsgenie
  ([atlassian.com/software/opsgenie](https://www.atlassian.com/software/opsgenie)),
  incident.io
  ([incident.io](https://incident.io/)), Grafana OnCall
  ([grafana.com/products/oncall](https://grafana.com/products/oncall/))
  are the common vendors. Which vendor is a minor
  decision; the important discipline is that *someone*
  is on the phone.
- **Escalation.** Primary → secondary → CTO, with an
  ack window (typically 15 minutes) at each level.
- **What actually pages.** At 5-15 engineers the paging
  criteria are usually *"the app is down for a
  customer"* and *"a specific alert on the health
  dashboard"*. Not "every log warning". See the SRE
  book chapter on *toil* for the framing that keeps the
  page volume tolerable.
- **Comp.** The rotation is *paid* work — an explicit
  on-call stipend, extra PTO, or a comp adjustment. If
  the rotation is unpaid at 5-15 engineers the team
  learns that operational responsibility is a tax on
  the engineers who happen to be conscientious, and
  the good ones quietly rotate out. Reference the
  compensation discussion in
  [`mod-104` chapter 06](../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md).
- **Handoff.** The end-of-week rotation handoff is a
  short written summary — open incidents, ongoing
  issues, follow-ups. Fifteen minutes on Friday. The
  handoff document lives in the engineering handbook.

Two anti-patterns to name:

- **The CTO-is-always-on-call rotation.** The CTO takes
  every page, the rotation exists on paper. The team
  learns the CTO does not trust them and never develops
  the operational muscle. The remedy: the CTO
  explicitly rotates *off* the primary for stretches at
  a time, even if the ack response would be slower.
- **The rotation-without-runbook.** The primary is
  paged and does not know what to do. The remedy is the
  incident-response playbook (chapter 07) and the
  runbook-per-alert discipline (Rundeck / a `runbooks/`
  directory in the repo).

## Artifact 3 — The first blameless post-mortem

The first post-mortem is usually written after the first
incident that took more than 30 minutes to resolve or
affected more than one customer. The word *blameless*
is doing all the work: the point of the post-mortem is
to change the system that produced the incident, not to
find the human to blame for it.

The canonical references:

- **The Google SRE book chapter on post-mortem culture**
  — [sre.google/sre-book/postmortem-culture](https://sre.google/sre-book/postmortem-culture/).
  Free online. The three-page distillation of the
  practice as run inside Google.
- **John Allspaw's *Blameless PostMortems and a Just
  Culture*** (Etsy, 2012) —
  [www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems).
  The essay that established the "just culture" framing
  in industry practice.
- **Sidney Dekker — *The Field Guide to Understanding
  'Human Error'*** —
  [sidneydekker.com](https://sidneydekker.com/books/). The
  academic ancestor of the just-culture framing;
  substrate reading for anyone who has to argue against
  a *"we need to hold someone accountable"* pushback in
  the incident review.

The 5-15 template is short — usually one page:

- **What happened.** The user-visible impact, with times.
- **Timeline.** Detection, first response, mitigation,
  resolution. Facts, not narrative.
- **Root cause(s).** Plural. Almost no incident has
  exactly one cause; asserting one is a warning sign the
  review is looking for a person to blame.
- **What went well.** The response, the alert, the
  recovery. Named.
- **What went badly.** Named. Attributed to the *system*
  (missing test coverage, unclear alert, ambiguous
  runbook), not to the individual who was on call.
- **Action items.** Owned. Dated. Landed in the
  engineering backlog with the same priority weight as
  feature work.

The 5-15 discipline that matters: the post-mortem is
*published to the whole team*, not filed away. The
first two or three post-mortems set the culture — if the
first one names an individual as the cause, the tenth
one will name a scapegoat. Etsy's essay above is the
clearest treatment of why.

## Artifact 4 — The first RFC process

At five engineers, decisions happen in Slack and get
made in a video call the same day. At fifteen engineers
that model produces decisions made by whoever happened
to be online at the time, with no record and no
opportunity for the engineer who was on parental leave
to object.

The RFC (Request for Comments) is the written mechanism
for changing a shared decision. Two canonical open-
source examples that shape the shape of the practice:

- **The Rust RFC process** —
  [github.com/rust-lang/rfcs](https://github.com/rust-lang/rfcs).
  Template, discussion, decision, all in a repo. Read
  the `README.md` for the shape.
- **The Python PEP process** —
  [peps.python.org](https://peps.python.org/). Older,
  longer, more formal — worth reading for the vocabulary
  around status transitions (Draft / Accepted /
  Rejected / Withdrawn).

Two other frames worth having open:

- **Michael Nygard — Documenting Architecture
  Decisions** (the ADR pattern, covered in
  [`mod-102` chapter 02](../mod-102-architecture-under-uncertainty/README.md))
  — [cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions).
  ADRs are the *decision-record* half; RFCs are the
  *proposal-and-discussion* half. Both live in the
  same repo.
- **Oxide Computer's RFD (Request for Discussion)
  process** —
  [rfd.shared.oxide.computer](https://rfd.shared.oxide.computer/)
  and the writeup at
  [oxide.computer/blog/rfd-1-requests-for-discussion](https://oxide.computer/blog/rfd-1-requests-for-discussion).
  An industry example of a startup running the process
  from day one.

The 5-15 RFC template is short (one to three pages):

- **Summary.** One paragraph.
- **Motivation.** Why the change matters. The
  hidden-cost-if-we-do-nothing side.
- **Proposal.** What the change is, concretely.
- **Alternatives.** Two or three, with why they were
  not chosen. Absence of alternatives is a warning
  sign the RFC is a decision looking for a rubber
  stamp.
- **Open questions.** Explicit list of things the
  author does not know.
- **Decision.** Filled in when the RFC is accepted /
  rejected / withdrawn.

The 5-15 discipline: RFCs live in the same repo as the
code they describe (`docs/rfcs/` is a common convention);
they are reviewed in the same tool as pull requests;
and the *"who approves"* rule is written down (usually
the tech lead of the affected slice, with the CTO as
final approver on cross-slice changes).

The failure mode: RFCs required for *every* change.
5-15 engineers cannot support an RFC on the shape of a
minor library function; requiring one produces a
consultative bottleneck that kills velocity. The rule
of thumb: RFC required for *"a change that affects
someone who is not in the room"*.

## Artifact 5 — The first product-engineering planning cadence

At five engineers, planning is a Monday morning stand-up
plus the CTO and the CEO trading messages. At fifteen
engineers that produces two failure modes: (a) engineering
delivers what the CTO thought the CEO meant, which is
never quite what the CEO said; (b) engineering work
that isn't in the CTO's field of view drifts out of the
CEO's roadmap and back into it too late to plan around.

The 5-15 planning cadence is a written rhythm with three
loops:

- **Weekly** — the sprint / iteration / kanban replenish
  meeting. 30-60 minutes, engineering team plus product
  (if a PM is on board yet) plus the CTO. Reviews the
  last week's completion, plans the next.
- **Every 2-6 weeks** — the roadmap review with the
  CEO and any founding customers or design partners.
  Aligns the engineering backlog against the go-to-
  market plan for the next quarter.
- **Quarterly** — the "big picture" review that resets
  the priorities against the actual business trajectory
  since the last quarter.

Two shape decisions to make explicitly at 5-15:

- **Kanban vs. sprints.** Sprints (typically two-week
  Scrum-adjacent) work when the team's throughput is
  predictable and there is a benefit to a
  synchronization ceremony. Kanban (continuous flow,
  WIP limits, no fixed iteration) works when demand is
  bursty and prioritisation shifts frequently — which
  is often the 5-15 startup shape. See the *Kanban:
  Successful Evolutionary Change for Your Technology
  Business* book by David Anderson at
  [leankanban.com/kanban-books](http://leankanban.com/kanban-books/)
  for the framing.
- **The CEO / CTO 1:1.** Weekly, at least 45 minutes,
  written agenda. The [`mod-108`](../mod-108-cto-ceo-and-board-communication/README.md)
  module handles the shape of this meeting; the 5-15
  requirement is that it exists on the calendar.

The failure mode: the planning cadence becomes a
governance layer. If the weekly meeting runs 90 minutes,
if there are three separate roadmap reviews across
product management and engineering leadership, if the
quarterly review runs a full day — the cadence has
outgrown 5-15 and is doing 50-150 work in a room with
15 people. Ruthlessly cut back.

## Artifact 6 — The first engineering handbook

The engineering handbook is *the artifact that survives
the founder's memory*. Concretely, it is a `docs/`
directory (or a Notion / Confluence space) that captures
the six sub-artifacts of this chapter, plus the four
decisions from chapter 01, plus a small set of
onboarding materials:

- The four ADRs from chapter 01 (repo, branching, CI,
  dev env).
- The tech-lead role charter (artifact 1).
- The on-call rotation and page-path documents
  (artifact 2).
- The blameless post-mortem template + the archive of
  past post-mortems (artifact 3).
- The RFC process document (artifact 4).
- The planning-cadence document (artifact 5).
- An onboarding checklist — the ordered list of tasks
  a new hire completes in their first week (accounts,
  local dev env running, first PR merged, first on-call
  shadow shift, first RFC read, first post-mortem read).

Two industry references worth having open:

- **GitLab's public engineering handbook** —
  [about.gitlab.com/handbook/engineering](https://about.gitlab.com/handbook/engineering/).
  Sprawls (GitLab is far past 5-15); useful as a
  reference to see the shape, not to copy wholesale.
- **Basecamp / 37signals's *Getting Real*** —
  [basecamp.com/gettingreal](https://basecamp.com/gettingreal).
  Older, opinionated, short. Useful counter-frame to the
  GitLab-scale handbook: the smallest thing that works.

The 5-15 handbook is closer to *Getting Real* than to
GitLab's — it is a short document, updated by the team,
that captures the *"how do we do things"* that a new
hire needs to know. It is not a compliance artifact
(that is the 15-50 conversation in chapter 03 and the
[`mod-107`](../mod-107-founder-scope-security-and-compliance/README.md)
module).

The failure mode: the handbook exists but is out of
date. The remedy is a lightweight *"handbook review"*
in the weekly cadence — the tech lead of a slice reads
the section relevant to their slice once a month and
updates it. Ten minutes. If nobody is willing to spend
ten minutes on it, the handbook is not doing enough
work and should be pruned until it is.

## Where DORA lives at 5-15

Chapter 05 gives the full treatment; the 5-15 point:

- **Deployment Frequency** — should be daily or better
  by the end of the 5-15 transition, if trunk-based
  development is honestly practised. If it isn't, the
  first RFC to file is *"why is deploy frequency lower
  than we thought?"*
- **Lead Time for Changes** — usually degrades during
  the 5-15 transition because code review becomes a
  queue and the CTO is no longer the reviewer. The
  tech-lead delegation (artifact 1) is what recovers
  it.
- **Change Failure Rate** — usually rises during the
  5-15 transition because new engineers ship changes
  in subsystems they don't yet own. The RFC process
  (artifact 4) and the on-call rotation (artifact 2)
  are the mechanisms that recover it.
- **MTTR** — usually improves during the 5-15
  transition because there is now an on-call rotation
  and post-mortem practice. If it doesn't improve, the
  on-call rotation is a rotation on paper only.

The 5-15 posture: read the four DORA numbers in the
weekly cadence, and treat the direction of change as a
diagnostic on which artifact is or isn't landing.

## Summary

- 5-15 is the phase in which the small-team-invisibility
  of the missing process gives out. Six artifacts do
  the work.
- **Tech lead** — the CTO's first *technical*
  delegation. Owns the reviews, the RFC end-to-end,
  the on-call escalation for a slice. Not a manager.
  Promote-vs-hire is
  [`mod-104` chapter 05](../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md).
- **On-call rotation** — the trigger is the first
  incident the CTO missed. Five decisions to make:
  page path, escalation, what pages, comp, handoff.
  Anti-pattern: the CTO-is-always-primary rotation
  that exists on paper.
- **Blameless post-mortem** — one-page template.
  Published to the team. The Google SRE book
  ([sre.google/sre-book/postmortem-culture](https://sre.google/sre-book/postmortem-culture/))
  and Allspaw's *Blameless PostMortems*
  ([www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems))
  are the two load-bearing references.
- **RFC process** — the written mechanism for
  changing a shared decision. Rust RFCs
  ([github.com/rust-lang/rfcs](https://github.com/rust-lang/rfcs))
  and Oxide's RFDs
  ([rfd.shared.oxide.computer](https://rfd.shared.oxide.computer/))
  are useful references. The rule of thumb: RFC
  required for *"a change that affects someone who
  is not in the room"*.
- **Planning cadence** — weekly / every-2-to-6-weeks /
  quarterly. Kanban vs. sprint decision to be made
  explicitly. The failure mode is the cadence
  becoming a governance layer.
- **Engineering handbook** — the artifact that
  survives the founder's memory. Six sub-artifacts.
  Closer in size to *Getting Real* than to GitLab's
  handbook.
- DORA numbers at 5-15 are a *diagnostic* on which
  artifact is or isn't landing. Chapter 05 gives the
  full treatment.

The chapter's paired exercise —
[`exercise-02-five-to-fifteen-transition-playbook.md`](exercises/exercise-02-five-to-fifteen-transition-playbook.md)
— asks you to author the six artifacts as a single
`docs/eng-handbook/` sub-tree, ready to hand to the
first tech lead as the substrate they will maintain.

Chapter 03 walks the 15→50 transition — the first
engineering manager, the first platform team (only if
the earn-its-keep tests pass), the career ladder v1,
the first budget cycle, and the first voluntary
departure.
