# Exercise 02 — Five-to-Fifteen Transition Playbook

**Module:** `mod-106-scaling-org-and-stack`
**Planned time:** ~3 hours
**Chapter this builds on:** [`02-five-to-fifteen-first-structure.md`](../02-five-to-fifteen-first-structure.md),
supported by [`mod-104` chapter 05 on tech-lead
promote-vs-hire](../../mod-104-first-engineering-hires-and-team-topology/05-first-em-tech-lead-vp-eng-and-promote-vs-hire.md)
and [`mod-102` chapter 02 on ADRs](../../mod-102-architecture-under-uncertainty/README.md).

## Problem statement

Author the **six-artifact 5-to-15 transition
playbook** as a single `docs/eng-handbook/` sub-tree in
the working repo (or the reference startup you used in
exercise 01). The six artifacts:

1. **Tech-lead role charter** (one page).
2. **On-call rotation v1** (one page + a page-path
   document + a handoff-doc template).
3. **Blameless post-mortem template** (one page,
   plus an empty archive directory).
4. **RFC process document** (one page + an RFC
   template + an example first RFC).
5. **Product-engineering planning cadence document**
   (one page).
6. **Engineering handbook v0 outline** (one page —
   the table-of-contents, not the full handbook).

The playbook is what you hand to the *first tech
lead* when they take on the role. They should be able
to run the 5-to-15 transition from the playbook without
the CTO having to re-explain any of it. The exercise's
discipline is the *artifact quality* — a real team
should be able to adopt the playbook Monday morning
without needing three follow-up Slack threads to
disambiguate the ambiguous bits.

## Requirements

All six artifacts live under `docs/eng-handbook/` (or
equivalent) in the working repo. Directory shape:

```
docs/eng-handbook/
  README.md                 # v0 outline (artifact 6)
  tech-lead-charter.md      # artifact 1
  on-call/
    README.md               # rotation v1 (artifact 2)
    page-path.md
    handoff-template.md
  post-mortem/
    template.md             # artifact 3
    archive/
      README.md             # empty for now, the archive lives here
  rfc/
    README.md               # process doc (artifact 4)
    template.md
    0001-example.md         # first RFC (see below)
  planning-cadence.md       # artifact 5
```

### Artifact 1 — Tech-lead role charter

One page. Sections:

- **Scope.** Which slice / subsystem does the tech
  lead own? Named, with the current-team roster.
- **Responsibilities.** 5-8 bullet points. Cover:
  design review for the slice, RFC end-to-end,
  on-call escalation for the slice, mentorship of
  ICs on the slice, technical roadmap for the slice.
- **What the tech lead is NOT.** 3-5 bullet points.
  Cover: 1:1s (still the CTO or EM), hiring loops
  (still shared), performance reviews (still shared).
- **Escalation.** Where does the tech lead escalate
  cross-slice questions? To whom, on what cadence?
- **Time allocation.** What percentage of the tech
  lead's time is expected to be spent on the tech-
  lead responsibilities vs. IC work? Fournier's
  *The Manager's Path*
  ([oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/))
  argues 20-50% for the tech-lead role; name your
  target and defend it.

### Artifact 2 — On-call rotation v1

Three files.

`on-call/README.md` — the rotation:

- **Roster.** 4-6 engineers on a weekly rotation.
- **Primary / secondary / escalation.** Ack windows,
  named escalation targets.
- **Comp.** The stipend / PTO / comp adjustment. Name
  the number (or the range, if it is comp-band
  dependent).
- **On-call handoff cadence.** Friday afternoons, 15
  minutes.

`on-call/page-path.md` — the operational path:

- **What pages.** Named alerts and named criteria
  (customer-visible outage, specific dashboard
  threshold).
- **What does NOT page.** Named non-actionable
  events (log warnings, non-critical dashboard
  changes).
- **Vendor.** PagerDuty / Opsgenie / incident.io /
  Grafana OnCall / other. Cite the chosen vendor.

`on-call/handoff-template.md` — the weekly handoff
document template:

- **Open incidents.** With current status and next
  action.
- **Ongoing issues.** Non-page-worthy but
  worth-watching.
- **Follow-ups.** Post-mortem action items whose
  owner is on the outgoing rotation.
- **Contacts.** Any customer or partner escalation
  points the incoming primary needs.

### Artifact 3 — Blameless post-mortem template

One file at `post-mortem/template.md`:

- The six-section template from chapter 02 artifact
  3 (What happened / Timeline / Root causes / What
  went well / What went badly / Action items).
- A note on the *published-to-the-team* discipline.
- A pointer to
  [sre.google/sre-book/postmortem-culture](https://sre.google/sre-book/postmortem-culture/)
  and
  [www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems).

Plus an empty `post-mortem/archive/README.md` that
explains the archive convention (one file per
incident, named `YYYY-MM-DD-short-slug.md`).

### Artifact 4 — RFC process document

`rfc/README.md`:

- **What an RFC is** and when to write one. Rule of
  thumb: *"a change that affects someone who is not
  in the room"*.
- **Who approves.** Named — the tech lead of the
  affected slice, with the CTO as final approver on
  cross-slice.
- **How review happens.** In the same tool as pull
  requests (usually GitHub / GitLab PR review).
- **RFC states.** Draft / Under review / Accepted /
  Rejected / Withdrawn. Pointer to
  [github.com/rust-lang/rfcs](https://github.com/rust-lang/rfcs)
  and
  [rfd.shared.oxide.computer](https://rfd.shared.oxide.computer/)
  as references.

`rfc/template.md`:

- **Summary** (one paragraph).
- **Motivation.**
- **Proposal.**
- **Alternatives.** At least two, with rejection
  reasons.
- **Open questions.**
- **Decision** (filled in when accepted / rejected /
  withdrawn).

`rfc/0001-example.md`:

- A **first RFC** on a real (or plausibly-real)
  change your team is considering. Not a
  hypothetical *"consider making a change"*; a
  specific decision the team could make this
  quarter. Suggested topics: adopting a specific
  observability vendor; standardising a specific
  code-review policy; introducing feature flags;
  splitting a monorepo package.
- Fully filled out — every section including a
  Decision.

### Artifact 5 — Planning-cadence document

`planning-cadence.md`:

- **Weekly rhythm.** Which meetings run every week,
  by whom, with what outcome.
- **The 2-to-6-week roadmap review.** Who attends
  (engineering + product + CEO if applicable), what
  the outcome is.
- **Quarterly review.** Length, attendees, output.
- **Kanban-vs-sprint call.** Which one your team is
  running and why. Cite either
  [leankanban.com/kanban-books](http://leankanban.com/kanban-books/)
  or
  [scrumguides.org](https://scrumguides.org/) or
  both.
- **CEO / CTO 1:1.** Cadence, agenda, output. (This
  is a hand-off to
  [`mod-108`](../../mod-108-cto-ceo-and-board-communication/README.md);
  a one-sentence pointer is sufficient.)

### Artifact 6 — Engineering handbook v0 outline

`README.md`:

- **What the handbook is.** One paragraph.
- **Table of contents** — the list of sections that
  the handbook will contain in v1. At v0 many
  sections are stubs; the ToC is the outline.
- **Ownership and update cadence.** Who owns each
  section, when it is reviewed. Rule of thumb: each
  section reviewed monthly by its named owner (10
  minutes).
- **Pointer to industry examples** —
  [about.gitlab.com/handbook/engineering](https://about.gitlab.com/handbook/engineering/)
  and
  [basecamp.com/gettingreal](https://basecamp.com/gettingreal)
  — with the note that GitLab's is far past the
  size a 5-15 team should be reading as a template.

## Starter guidance

- **Do not import a template wholesale.** GitLab's
  handbook is thousands of pages. The 5-15 handbook
  is closer in size to *Getting Real*
  ([basecamp.com/gettingreal](https://basecamp.com/gettingreal)).
  Read the references, then write your own — do not
  copy-paste.
- **The first RFC is the load-bearing artifact.** A
  process document without an example is a
  compliance artifact. Writing an actual first RFC
  forces you to notice which parts of the process
  are ambiguous.
- **The tech-lead charter should name the person, if
  possible.** *"The tech lead's role is..."* is
  weaker than *"Alice is the tech lead of the
  billing slice; her scope is..."*. If you cannot
  yet name the person, name what the person should
  look like (skills, seniority, tenure, comp band).
- **The on-call comp must be a real number, not a
  placeholder.** *"Comp TBD"* is not on-call comp;
  it is the absence of a rotation. Set the number
  against your comp band from
  [`mod-104` chapter 06](../../mod-104-first-engineering-hires-and-team-topology/06-org-chart-career-ladder-and-comp-band.md).
- **The blameless post-mortem template's discipline
  is in the *what-went-badly* section**. Read Etsy's
  writeup at
  [www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems)
  before authoring it. The section should be
  attributed to the *system*, not the individual;
  the template's language should push a reader in
  that direction.
- **Read the six artifacts together at the end.**
  They should be consistent: the tech-lead's
  responsibilities should include RFC end-to-end and
  on-call escalation; the on-call escalation path
  should reference the tech lead; the planning
  cadence should reference the RFC process for
  cross-slice work. If the six do not cross-
  reference, they are six documents rather than one
  playbook.

## Acceptance criteria

Your drill output is complete when:

- The `docs/eng-handbook/` directory contains all
  the files in the shape above.
- Each artifact is one page or the equivalent (a
  reader should get through it in 5 minutes).
- The first RFC is fully filled out including a
  Decision section — a hypothetical open question is
  not enough.
- The on-call rotation names a comp number, a
  vendor, and 4-6 named or roleplayed engineers.
- The blameless post-mortem template's language
  attributes what-went-badly to the system, not the
  individual. If a reader could infer *"whose fault
  is this"* from the template, revise.
- The six artifacts cross-reference each other
  where they naturally should (tech-lead charter →
  on-call, RFC, planning cadence; on-call README →
  post-mortem template).
- The handbook v0 outline names an owner for every
  section. Unowned sections rot.
- The full playbook can be handed to a new hire on
  their first day and they can read it in under 45
  minutes and act on it.

## What this feeds into

- **Exercise 03** — the 15-50 playbook builds on
  this. The first EM's role charter is the natural
  next artifact, above the tech-lead charter.
- **Exercise 05** — the DORA measurement plan is
  read in the weekly planning-cadence meeting from
  artifact 5.
- **Exercise 07** — the on-call rotation v1 from
  artifact 2 is the base the 15-50 rotation
  evolves from; the blameless post-mortem template
  from artifact 3 is reused in exercise 07's
  incident-response playbook.
- **The lab** — the six artifacts, plus the four
  ADRs from exercise 01, are the substrate for the
  `docs/scaling/` runbook.

The 5-to-15 handbook is the artifact that survives
the founder's memory. The exercise is not complete
until the handbook is short enough to read but complete
enough to run the team from.
