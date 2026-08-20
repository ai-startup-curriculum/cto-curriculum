# Exercise 01 — Zero-to-Five First Process Drill

**Module:** `mod-106-scaling-org-and-stack`
**Planned time:** ~2 hours
**Chapter this builds on:** [`01-zero-to-five-first-process.md`](../01-zero-to-five-first-process.md),
supported by [`mod-102` chapter 02 on the ADR
discipline](../../mod-102-architecture-under-uncertainty/README.md).

## Problem statement

Author the **four foundational decisions** for a 0-5
engineer team — repo layout, branching model, CI
pipeline, and dev-environment convention — as a set of
short **ADRs** (Architecture Decision Records) in the
working repo. Do this for either your own pre-seed
startup or a reference startup you can describe in a
paragraph (product, team size, tech stack, primary
customer).

The point of the drill is not to *decide* what shape the
process should be — the chapter has given you the
defaults. The point is to force yourself to *write down
the decision*, along with the reason it will still make
sense at 15 engineers, in the artifact format the team
will use for every subsequent architecture decision.
The four ADRs are the *first* four ADRs of the working
repo, and their existence is the moment the
architecture-decision discipline starts.

## Requirements

Author four ADR files at `docs/adr/` (or the equivalent
convention in your working repo). The ADR template
follows Michael Nygard's four-section shape
([cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions))
extended with a short "reversibility" section for this
drill.

### File naming

- `0001-repo-layout.md`
- `0002-branching-model.md`
- `0003-ci-pipeline.md`
- `0004-dev-environment.md`

### ADR sections (per file)

- **Status** — Accepted (this is a from-scratch
  decision, not a change from a prior one).
- **Context** — 3-5 sentences on the team size, the
  product shape, the tech stack, and the constraints
  that shape the decision. Concrete: *"5 engineers,
  Typescript / Node full-stack, one production
  customer, weekly deploys, no compliance
  requirements yet."*
- **Decision** — the specific choice, in a
  paragraph. Concrete: *"Single monorepo, one
  `services/` directory containing per-service
  subdirectories, one root `package.json` with a
  workspace manifest, one shared linter and
  formatter config at the root."*
- **Consequences** — 4-8 bullet points on what the
  decision buys and what it costs. Cover both the
  *now* consequences and the *at-15-engineers*
  consequences.
- **Reversibility** — 2-4 sentences on how expensive
  the decision would be to reverse at 5 engineers,
  10 engineers, and 20 engineers. Use *"engineer-
  weeks"* as the unit. If your answer is *"trivial
  at every stage"*, either the decision is wrong-
  fitted for this drill or the reversibility
  analysis is not yet honest.
- **Alternatives considered** — 2-3 alternatives,
  each with one sentence on why it was not chosen.
  Absence of alternatives is a warning sign.
- **References** — the primary sources cited (e.g.,
  [trunkbaseddevelopment.com](https://trunkbaseddevelopment.com/),
  [12factor.net](https://12factor.net/),
  [docs.github.com/actions](https://docs.github.com/en/actions)).

### The four decisions and their scope

- **ADR 0001 — Repo layout.** Monorepo, multi-repo,
  or grouped-repos. If grouped, name the groups
  explicitly.
- **ADR 0002 — Branching model.** Trunk-based,
  GitFlow, or release-train. Name the deploy trigger
  (merge-to-`main`, tag-and-release, scheduled
  release).
- **ADR 0003 — CI pipeline.** The vendor (GitHub
  Actions / GitLab CI / CircleCI / Buildkite /
  other), the trigger (every push, every PR), the
  jobs (lint, build, unit test, integration test,
  smoke deploy), the target CI wall-clock time (name
  the number).
- **ADR 0004 — Dev-environment.** The bring-up path
  (docker compose / Nix-adjacent / cloud dev
  environment), the config-management approach
  (Twelve-Factor
  [12factor.net](https://12factor.net/) or a named
  alternative), the target new-hire time-to-first-PR
  (name the number).

### An accompanying `docs/adr/README.md`

Short (under 200 words):

- What ADRs are, one paragraph.
- The Nygard template, one paragraph, with a link
  to
  [cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions).
- How to write a new ADR — file naming, review
  process (at 0-5, "the CTO and one senior engineer
  review"), where they live in the repo.
- A pointer to `adr-tools`
  ([github.com/npryce/adr-tools](https://github.com/npryce/adr-tools))
  if you plan to use it.

## Starter guidance

- **Start with the chapter's defaults, then justify
  them.** Monorepo / trunk-based /
  GitHub-Actions-or-equivalent / docker-compose plus
  Twelve-Factor is the default. If your context
  legitimately calls for a different choice (a
  regulated deploy, a mobile-only product, a language
  ecosystem with poor monorepo tooling), the ADR
  should say so explicitly. Do not accept the
  defaults without asking whether they fit your
  context; do not reject the defaults for aesthetic
  reasons.
- **Cite the primary source, not a blog aggregation.**
  Trunk-based development is
  [trunkbaseddevelopment.com](https://trunkbaseddevelopment.com/);
  the *"GitFlow is discouraged for continuously-
  deployed SaaS"* note is on the original 2010 post
  at
  [nvie.com/posts/a-successful-git-branching-model](https://nvie.com/posts/a-successful-git-branching-model/);
  Twelve-Factor is
  [12factor.net](https://12factor.net/); the DORA
  program is at [dora.dev](https://dora.dev/). Cite
  the primary source per ADR.
- **The reversibility analysis is the hardest section
  to write honestly.** Sit for a few minutes with
  each ADR and ask *"if we tried to reverse this at
  20 engineers, what would break, and how long would
  it take?"* — do not answer *"we would just do it,
  it would be fine"*. The reversibility unit
  (engineer-weeks) is the point.
- **The at-15-engineers consequences are the
  load-bearing ones.** The 0-5 defaults are easy to
  defend at 0-5; the drill is checking that they
  will *still* be defensible at 15. If a decision's
  15-engineer consequences look bad, either the
  decision is wrong or the 5-15 transition needs a
  specific mitigation you should name in the ADR.
- **The alternatives-considered section catches the
  reversibility problem before it lands.** If the
  alternatives are all *"the alternative would be
  worse right now"*, none of them are *"the
  alternative would be better at 15 engineers"* —
  and the drill's *reversibility* section is the
  place to name that mismatch.
- **Read the four ADRs together, not each in
  isolation.** The four decisions interact: the CI
  pipeline decision assumes the repo-layout
  decision; the dev-environment decision assumes
  the CI-pipeline decision. If the four ADRs
  contradict each other (a monorepo with a
  per-service CI vendor and a per-service dev
  environment) you have four internally-consistent
  decisions that combine badly, and the four should
  be revised as a set.

## Acceptance criteria

Your drill output is complete when:

- All four ADR files exist at `docs/adr/` (or your
  repo's equivalent), each following the
  eight-section template above.
- The `docs/adr/README.md` exists and describes the
  process.
- Every ADR cites at least one primary reference in
  the References section.
- The reversibility section of each ADR names a
  concrete engineer-week cost at 5, 10, and 20
  engineers.
- The four ADRs are internally consistent — the
  monorepo-vs-multi-repo decision matches the CI
  scope; the branching model matches the deploy
  trigger; the dev-environment matches the CI
  environment.
- Reading the four ADRs takes no more than 10
  minutes for a technical reviewer who does not
  know your codebase, and they can articulate the
  four decisions back to you without asking a
  follow-up.
- Every ADR names at least two alternatives that
  were considered and rejected.

## What this feeds into

- **Exercise 02** — the six-artifact 5→15 playbook
  extends this ADR set with the tech-lead role
  charter, the on-call rotation, the RFC process,
  the planning cadence, the blameless post-mortem
  template, and the engineering-handbook v0.
- **Exercise 05** — the DORA measurement plan
  measures against the CI pipeline defined in
  ADR 0003 and the dev-environment defined in ADR
  0004.
- **Exercise 06** — the platform-investment sizing
  at 0-5 is the *absence* of the platform team,
  which these four ADRs justify.
- **The lab** (`lab-01-publish-a-stage-transition-runbook`)
  starts from this ADR set as the first entry in
  the runbook.

The drill's discipline is *authoring the four
decisions in the format the team will use forever*,
not choosing exotic alternatives. If you find yourself
justifying multi-repo at 3 engineers or a release-train
at 5, sit with the chapter's defaults again — the
drill is looking for defensible defaults, not novelty.
