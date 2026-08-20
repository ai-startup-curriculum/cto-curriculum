# First EM, First Tech Lead, First VP Engineering — and the Promote-vs-Hire Trade-off

> "Never promote someone to a management role as a
> reward. Promote them because the job needs to be done
> and they are the best person to do it." — the honest
> restatement of a line variously attributed but most
> often heard through Camille Fournier's *The Manager's
> Path* ([oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/)),
> the CTO chapter of which is the load-bearing reading
> for this chapter.

## Motivation

The three leadership hires this chapter is about — the
first **tech lead**, the first **engineering manager**,
the first **VP Engineering** — are the ones the
CTO makes at three different points in the org's life,
and each of them is the moment the CTO stops doing a
specific part of the CTO job themselves and hands it to
someone else. Each of those transitions is expensive to
get wrong.

Two failure modes dominate the field literature:

- **Hiring too late.** The CTO waits until the team is
  audibly complaining before making the leadership hire.
  By the time the search closes, the team has already
  worked around the missing lead for six months, cultural
  patterns have set that will resist the new hire, and
  the CTO is burned out from doing the role themselves.
- **Hiring too soon or too senior.** The CTO hires a VP
  Engineering at 12 engineers because a board member
  suggested it. The VP arrives, finds a team too small
  to need the layer of management they were hired for,
  either downgrades the role or leaves inside a year.

Between these two failure modes sits the more contested
question: **promote or hire**? Promote a founding
engineer into the first EM role, or hire an EM
externally? Promote a strong senior IC to the tech lead
role, or hire someone whose track record is
tech-leading? Every startup makes this decision in one
direction or the other, and every startup has one story
about the time it made it the wrong way.

This chapter names the honest triggers for each role,
walks the promote-vs-hire trade-off with an explicit
two-column checklist, and names the two failure modes
each direction of the decision defaults to.

Two references worth having open while reading this
chapter: Fournier's *The Manager's Path* (whole book,
CTO / VP-Eng chapters especially) and Larson's *An
Elegant Puzzle* ([lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/))
for the systems-of-engineering-management framing this
chapter's triggers draw on.

## The first tech lead

The first tech lead is usually the CTO's first
delegation of the *technical* half of the CTO job —
architecture decisions in a specific slice, code review,
mentorship of the engineers in that slice, and
representing the slice's technical direction to the
rest of the org.

### Trigger

The trigger for the first tech lead is *not* headcount
— it is the appearance of a **specific technical slice
that needs a lead**. Concretely, one of:

- The team has grown large enough (typically 6-10 ICs)
  that a single stream-aligned team can no longer hold
  all its subsystems in one person's head, and the CTO
  can no longer be the primary reviewer of every PR.
- Team topology (see [`chapter 04`](04-team-topologies-at-startup-scale.md))
  is transitioning from one stream-aligned team to two,
  and one of the two needs a technical lead who is not
  the CTO.
- A complicated-subsystem team is forming (an ML
  pipeline, a data platform) and its technical
  direction needs an owner who is deep enough in the
  domain to make the calls.

The trigger is *not* "an engineer has been here a long
time and it would be nice to give them a title". A tech
lead role handed out as a tenure reward becomes the
"why can this engineer make design decisions for a
subsystem they don't work in" complaint six months
later.

### Promote vs. hire — the honest checklist

The two-column checklist for the first tech lead
promote-vs-hire:

- **Promote when**: (a) the founding engineer with the
  deep domain context is already leading design
  decisions informally and the team already routes
  through them; (b) the CTO's coaching hours can absorb
  the ramp; (c) the person has said they want the role
  or has already asked how to grow toward it.
- **Hire externally when**: (a) no internal candidate
  has the specific technical depth the slice needs (a
  data-platform tech lead when the founding team is all
  application engineers); (b) an internal promotion
  would leave a hole in the IC ranks the team cannot
  absorb; (c) the internal candidate has said no, or
  the CTO is asking them because they are convenient
  rather than because they are the best fit.
- **Slow down and re-examine when**: the CTO is
  considering the promotion primarily as a *retention*
  move ("we'll lose them if we don't"). Retention as
  the driver produces mis-shaped roles — the promoted
  engineer stays for six months and then leaves anyway,
  and now the team has a vacant role at a title that
  will be awkward to fill downward.

### Default failure modes

- **Promoted-to-shut-them-up.** The tech lead was
  promoted to retain them; they turn out to be strong
  IC and weak lead; the team's technical direction
  drifts under a lead who cannot make the calls the
  role requires.
- **Hired-externally-into-a-social-vacuum.** The tech
  lead was hired externally, has strong background, but
  the team has spent nine months routing through the
  founding engineer for design calls. The new lead's
  first decisions are second-guessed by the team; the
  founding engineer becomes a shadow tech lead; the
  role does no work. Fix: brief the team explicitly on
  the role change (including the founding engineer's
  new role, if that founding engineer stays IC), and
  give the new lead a well-scoped first design
  decision to make so the team sees them lead.

## The first engineering manager

The first EM is the CTO's first delegation of the
*people* half of the CTO job — 1:1s, feedback,
performance management, hiring for the team, career
conversations, the difficult conversations. Note that
day-two management craft (1:1s, feedback,
performance-management, difficult conversations) is
owned by [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
(level 30) — the CTO's job here is to make the first EM
decision cleanly and then hand the day-two content to
that track.

### Trigger

The trigger for the first EM is a combination:

- **Team size.** 6-8 direct reports to the CTO is the
  point at which 1:1 hygiene, feedback cadence, and
  hiring load overwhelm the CTO's non-management
  capacity. Past that, either 1:1s slip (management debt
  in the Horowitz sense — see the *Hard Thing About
  Hard Things* chapter on management debt) or IC time
  vanishes entirely.
- **Calendar composition.** The CTO's calendar is
  >50% 1:1s and hiring, or the CTO is not doing the
  1:1s at the cadence the team expects. The pendulum
  (Charity Majors, *Engineering Management: The
  Pendulum Or The Ladder* —
  [charity.wtf/2019/01/04](https://charity.wtf/2019/01/04/engineering-management-the-pendulum-or-the-ladder/))
  has swung all the way to management and the CTO is
  losing the technical seat.
- **Complexity of interpersonal work.** A performance-
  management conversation is on the horizon, or a
  difficult inter-team conflict has emerged, and the
  CTO does not have the bandwidth to do it justice.

### Promote vs. hire — the honest checklist

The first EM decision is where the promote-vs-hire
tension is most acute in the field.

- **Promote when**: (a) a founding engineer has already
  been doing the interpersonal work informally
  (mentoring peers, mediating disputes, running
  planning) and *wants* the EM role, not because of
  title but because of the shape of the work; (b) the
  CTO has the coaching bandwidth to sit alongside the
  new EM for the first two quarters; (c) an external
  hire would take four months to build the trust the
  internal candidate already has; (d) the *team* would
  see the internal candidate as a legitimate manager
  rather than as "our peer who now has a title".
- **Hire externally when**: (a) no internal candidate
  wants the role (the honest failure mode of
  founding-engineer teams; management is not a
  universally-desired path); (b) the org needs EM craft
  the internal candidate has never seen (running a
  performance improvement plan, running a layoff, running
  a hiring loop at 3x the current pace); (c) the
  internal candidates who might want it are the wrong
  fit — strong ICs whose interpersonal signal is weak;
  (d) the team has grown enough that the first EM will
  need to hire two more engineers in the first six
  months, and the internal candidate has never run a
  loop.
- **Slow down and re-examine when**: the CTO is
  considering the promotion because they don't want to
  do a hiring loop themselves, or because they want to
  avoid the awkward conversation of *not* promoting the
  senior-most IC. Neither is a reason to promote; both
  are reasons to run the loop.

### Default failure modes

- **Promoted-to-management-without-choice.** The
  founding engineer is offered the EM role because they
  are senior-most, not because they want it. They
  accept because they don't want to disappoint the CTO.
  Six months in, they are miserable, the team's
  1:1-hygiene has slipped, and the CTO has a difficult
  conversation on their hands. Fix: make the pendulum
  vocabulary explicit (Majors —
  [charity.wtf/2019/01/04](https://charity.wtf/2019/01/04/engineering-management-the-pendulum-or-the-ladder/))
  when discussing the role, and make it socially safe
  to say no.
- **Hired-externally-into-a-broken-team.** The external
  EM arrives to find that the founding-engineer team
  has patterns (no 1:1s, no written feedback, no career
  conversations) that were tolerated because the CTO
  was doing them intermittently. The new EM has to
  simultaneously install the missing hygiene *and*
  build trust with a team that is culturally
  ambivalent about management. Fix: give the new EM a
  specific, bounded first project (three problems to
  solve in the first quarter) rather than "figure it
  out", and back their early calls in public.
- **The player-coach EM.** The first EM is hired but
  spends >50% of the week writing code. The team's
  management needs remain unmet. This is a fine mode at
  founding-team scale (there is no team to manage yet)
  but is a failure mode past ~4 direct reports. Fix:
  the EM's IC time is one deliberate slot (mirror of
  the CTO's own pendulum in [`mod-101` chapter
  01](../mod-101-cto-role-and-ownership-map/01-cto-ladder-pre-seed-to-series-b.md)),
  not a majority of the week.

## The first VP Engineering

The first VP Engineering (VP Eng, sometimes titled Head
of Engineering) is the CTO's first delegation of the
whole *engineering-org operating system* — hiring,
career ladder, planning cadence, delivery cadence,
performance calibration across teams, the annual
compensation review. It is a categorically different
hire from the first EM.

### Trigger

The trigger for the first VP Eng is a combination:

- **Multi-team scale.** 15-30 engineers organised into
  2-5 teams, typically at or just past the topology
  transition described in [`chapter 04`](04-team-topologies-at-startup-scale.md).
  Below this scale, a VP Eng is a layer of management
  with nothing to manage.
- **The CTO is at rung (c) or crossing to rung (d).**
  See [`mod-101` chapter 01](../mod-101-cto-role-and-ownership-map/01-cto-ladder-pre-seed-to-series-b.md).
  The player-coach CTO who wants to stay a player is
  the CTO who most needs a VP Eng to own the operating
  system.
- **The board or CEO has asked what happens if the CTO
  is hit by a bus.** The VP Eng is the answer, and the
  question typically first surfaces around Series-A
  close.

The VP Eng vs. CTO role split is the specific subject
of [`mod-101` chapter 02](../mod-101-cto-role-and-ownership-map/02-cto-vs-vp-eng-vs-chief-architect-vs-head-of-platform.md);
re-read that chapter before running this decision.
Fournier's *Manager's Path* CTO chapter is the load-
bearing reading; Ben Horowitz's chapter on hiring
executives ("Hiring Executives", in *The Hard Thing
About Hard Things* —
[harpercollins.com](https://www.harpercollins.com/products/the-hard-thing-about-hard-things-ben-horowitz))
is the second load-bearing reading, and it names the
executive-hiring failure modes this decision defaults
to if the CTO is not careful.

### Promote vs. hire — the honest checklist

The first VP Eng decision *usually* leans toward hire,
but the promote path exists and is worth naming
honestly.

- **Promote when**: (a) an internal EM has already been
  running the operating system informally — planning
  cadence, delivery cadence, cross-team calibration —
  and the promotion is a formalisation; (b) the CTO
  has been coaching the internal candidate on the VP
  Eng seat for at least two quarters; (c) the CEO and
  the board are comfortable with the promotion
  narrative; (d) the internal candidate has run at
  least one hiring wave and one performance calibration
  cycle already.
- **Hire externally when**: (a) the operating system
  the org needs is one the CTO has never installed
  themselves and no internal candidate has run before
  (a formal calibration process across five teams, a
  hiring machine that closes 15 offers a quarter, a
  performance-management practice that survives the
  first layoff); (b) the org's ambition — Series-B and
  a 50-engineer org inside 18 months — needs a VP Eng
  who has already been through that transition once;
  (c) an internal promotion would be perceived as
  political (the "founder's favourite got the role")
  in a way that undermines the promoted person's
  legitimacy.
- **Slow down and re-examine when**: the CTO is
  considering hiring a VP Eng because *they don't want
  to be a CTO anymore*. That is a legitimate personal
  answer, but it needs to be surfaced with the CEO and
  the board as a role-transition conversation, not
  quietly resolved by delegating the CTO seat to a VP
  Eng.

### The executive-hire failure modes to avoid

Horowitz's chapters on hiring executives (*The Hard
Thing About Hard Things*) are the standard reading on
the failure modes here. The three that recur:

- **Hiring for a pattern-match**, not for the role. The
  CTO hires a VP Eng who has "VP Eng at a Series-B
  company" on their resume, without asking whether the
  Series-B was a 40-engineer org or a 400-engineer
  org, and whether the VP Eng was the operator or a
  bystander.
- **Under-briefing the role**, so the new VP Eng
  arrives to find their scope was implicit and their
  authority is contested. Fix: write the role charter
  before the search closes (see [`mod-101` chapter
  02](../mod-101-cto-role-and-ownership-map/02-cto-vs-vp-eng-vs-chief-architect-vs-head-of-platform.md)
  for the specific hand-off between CTO and VP Eng).
- **Failing to survive the first ninety days.** The new
  VP Eng makes a controversial call in month one, the
  founder team second-guesses in public, the VP Eng's
  authority never re-establishes. Fix: the CTO and
  CEO back the VP Eng's early calls in public, and
  disagreement — where it exists — is resolved in
  private and communicated as a single voice.

## The honest promote-vs-hire drill (applied to any of the three)

A two-column drill the CTO runs *in writing* before
making the decision. For each row, the honest answer
goes in the column that matches.

```
Question                                            | Points toward PROMOTE | Points toward HIRE
----------------------------------------------------|-----------------------|-------------------
Is there an internal candidate who WANTS this role? | Yes (specific person) | No / uncertain
Has that candidate done this shape of work already? | Yes, informally, for 3+ months | No
Does the team already route through them for this?  | Yes                   | No
Can I coach them for the first two quarters?        | Yes (calendar clear)  | No
Would promoting leave a hole IC-side we can't fill? | No                    | Yes
Does the role need a skill nobody internal has?     | No                    | Yes
Would the promotion look political to the team?     | No                    | Yes
Am I promoting to retain them?                      | No                    | Yes (do NOT promote)
Am I hiring to avoid a hard conversation?           | Yes (do NOT hire)     | No
Do I have the calendar to run a serious search?     | -                     | Yes
```

**Rules for reading the drill.**

- Any *"Yes (do NOT promote)"* or *"Yes (do NOT hire)"*
  answer is a hard signal. Retention-promotion and
  conflict-avoidance-hiring are the two most common
  failure modes, and both are best flushed out by
  writing them down.
- The remaining rows are *directional signals*, not a
  vote. A promote decision with all-promote signals and
  one uncertain signal is a promote. A hire decision
  with 6 promote signals and 4 hire signals is a hire
  that will fail because the internal candidate exists
  and the team knows it.
- The drill goes in the decision memo (see chapter 06
  for the memo shape as an artifact). The CEO and — for
  the VP Eng — the board should see the drill.

## Failure modes across all three decisions

- **The "just add a manager" reflex.** The CTO is
  overloaded, adds a manager, moves on. The manager
  arrives to find their scope was implicit. Fix: write
  the role charter *first*, then hire; the charter is
  the artifact the whole decision depends on.
- **The peer-turned-manager trap.** The founding
  engineer is promoted to EM without an explicit
  conversation with the team about the role change.
  Two peers now have to be managed by their former
  peer, and the informal team dynamics resist the
  formal one. Fix: hold the explicit conversation with
  the team before the promotion is announced, and give
  the new EM cover to change some patterns immediately
  so the role is visible.
- **The over-hired executive.** The VP Eng arrives at
  a 12-engineer org because the board asked, has no
  operating system to run, and either leaves or
  downgrades to hands-on EM. Fix: wait for the trigger;
  under-managed at 12 is a solvable problem, over-
  managed at 12 is not.
- **The management-craft-vacuum.** The first EM
  arrives and does not have the day-two craft (1:1s,
  feedback, difficult conversations); the CTO does
  not have it either; the org runs unmanaged. Fix:
  cite the boundary — day-two management craft is
  owned by [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (level 30). The CTO onboarding a first EM should
  route them to that track's material, and consume it
  themselves alongside the EM for the first quarter.

## Summary

- The first tech lead's trigger is a **specific
  technical slice that needs a lead**, not headcount.
  Promote when the founding engineer already leads
  informally and wants the role; hire externally when
  the slice needs depth no internal candidate has.
- The first EM's trigger is **6-8 direct reports plus
  1:1 hygiene decay plus the CTO pendulum swinging all
  the way to management**. Promote when an internal
  candidate is already doing the interpersonal work and
  wants the role; hire externally when nobody internal
  wants it, or when the org needs EM craft nobody has.
- The first VP Eng's trigger is **15-30 engineers, 2-5
  teams, and the CTO at rung (c) crossing to rung
  (d)**. Usually leans toward hire; the honest promote
  path exists when an internal EM has been running the
  operating system informally.
- The **honest two-column promote-vs-hire drill** is a
  written artifact. Retention-promotion and conflict-
  avoidance-hiring are hard-signal failure modes that
  the drill exists to surface.
- Day-two management craft (1:1s, feedback,
  performance-management, difficult conversations) is
  owned by [`ai-infra-team-lead`](../../../ai-infra-team-lead-learning)
  (level 30) — this module's boundary. The
  compensation and people-ops depth is owned by
  [`startup-operations-governance-curriculum`](https://github.com/ai-startup-curriculum/startup-operations-governance-curriculum)
  (People pillar) — the other boundary. This chapter
  makes the leadership-hire *decision*; the linked
  tracks own the day-two content the CTO consumes.

The chapter's paired exercise —
[`exercise-05-promote-vs-hire-first-em-drill.md`](exercises/exercise-05-promote-vs-hire-first-em-drill.md)
— walks the drill for a specific first-EM decision, with
the written decision memo the CEO can read. Chapter 06
is where the org chart, career-ladder v0, and comp band
this decision triggers are formalised as artifacts.
