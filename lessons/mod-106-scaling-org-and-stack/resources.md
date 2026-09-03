# Resources — mod-106-scaling-org-and-stack

Primary references for the topics covered in this
module. Every entry is linked to a publisher, an
author-maintained URL, or an official standards body
/ vendor documentation page. See
[`JOB_REQUIREMENTS.md`](../../JOB_REQUIREMENTS.md)
for the full authoritative-reference list that
grounds the whole curriculum.

## Cross-module load-bearing references

The four references that recur across most chapters
of this module:

- **Nicole Forsgren, Jez Humble, Gene Kim —
  *Accelerate: The Science of Lean Software and
  DevOps*** —
  [itrevolution.com/product/accelerate](https://itrevolution.com/product/accelerate/) —
  the book-length treatment of the DORA four keys
  and the *speed-and-stability-together* research
  finding.
- **DORA — DevOps Research and Assessment** —
  [dora.dev](https://dora.dev/) — home of the annual
  *State of DevOps Report* at
  [dora.dev/research](https://dora.dev/research/)
  and the DORA quickcheck at
  [dora.dev/quickcheck](https://dora.dev/quickcheck/).
- **Camille Fournier — *The Manager's Path*** —
  [oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/) —
  the tech-lead → EM → director → VP → CTO
  progression, load-bearing in chapters 02, 03, and
  04.
- **Will Larson — *An Elegant Puzzle*** —
  [lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/) —
  systems-shape thinking for engineering
  organisations at 50-150. Also *Staff Engineer* at
  [staffeng.com/book](https://staffeng.com/book) for
  the IC-tier counterpart.

## The 0→5 transition (chapter 01)

### Repo layout

- **Software Engineering at Google — free chapters on
  version control and branch management** —
  [abseil.io/resources/swe-book](https://abseil.io/resources/swe-book) —
  the canonical treatment of the monorepo shape at
  scale (chapter 16 on version control, chapter 17
  on Code Search).

### Branching model

- **Trunk-Based Development** —
  [trunkbaseddevelopment.com](https://trunkbaseddevelopment.com/) —
  the reference documentation for the trunk-based
  discipline.
- **Vincent Driessen — *A successful Git branching
  model* (the original GitFlow post, 2010)** —
  [nvie.com/posts/a-successful-git-branching-model](https://nvie.com/posts/a-successful-git-branching-model/) —
  historically important; note the author's own
  2020 update at the top of the post cautioning
  against GitFlow for continuously-deployed
  software.

### CI pipeline

- **GitHub Actions documentation** —
  [docs.github.com/actions](https://docs.github.com/en/actions).
- **GitLab CI/CD documentation** —
  [docs.gitlab.com/ee/ci](https://docs.gitlab.com/ee/ci/).
- **CircleCI** —
  [circleci.com](https://circleci.com/).
- **Buildkite** —
  [buildkite.com](https://buildkite.com/).

### Dev environment

- **The Twelve-Factor App** —
  [12factor.net](https://12factor.net/) — the
  canonical configuration-management convention
  the 0-5 dev environment is authored against.
- **Docker Compose** —
  [docs.docker.com/compose](https://docs.docker.com/compose/) —
  the default multi-service local-development shape.
- **Nix** — [nixos.org](https://nixos.org/) — the
  reproducible-environments reference.
- **Devbox** — [jetify.com/devbox](https://www.jetify.com/devbox) —
  Nix-adjacent, simpler onboarding.
- **mise** — [mise.jdx.dev](https://mise.jdx.dev/) —
  version-manager successor to asdf.
- **asdf** — [asdf-vm.com](https://asdf-vm.com/) —
  the long-established multi-runtime version manager.
- **GitHub Codespaces** —
  [github.com/features/codespaces](https://github.com/features/codespaces) —
  hosted cloud dev environments.
- **Gitpod** — [gitpod.io](https://www.gitpod.io/) —
  hosted cloud dev environments.

## The 5→15 transition (chapter 02)

### Tech-lead role

- **Camille Fournier — *The Manager's Path* — tech-
  lead chapters** —
  [oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/).

### On-call

- **Google SRE book — *Being On-Call*** —
  [sre.google/sre-book/being-on-call](https://sre.google/sre-book/being-on-call/) —
  free online. The load-bearing reference on the
  on-call discipline.
- **Google SRE book — full table of contents** —
  [sre.google/sre-book/table-of-contents](https://sre.google/sre-book/table-of-contents/).
- **PagerDuty** —
  [pagerduty.com](https://www.pagerduty.com/).
- **Opsgenie (Atlassian)** —
  [atlassian.com/software/opsgenie](https://www.atlassian.com/software/opsgenie).
- **incident.io** —
  [incident.io](https://incident.io/).
- **Grafana OnCall** —
  [grafana.com/products/oncall](https://grafana.com/products/oncall/).
- **FireHydrant** —
  [firehydrant.com](https://firehydrant.com/).

### Blameless post-mortems

- **Google SRE book — *Post-mortem Culture: Learning
  from Failure*** —
  [sre.google/sre-book/postmortem-culture](https://sre.google/sre-book/postmortem-culture/) —
  free online.
- **John Allspaw — *Blameless PostMortems and a Just
  Culture* (Etsy Code as Craft, 2012)** —
  [www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems) —
  the canonical industry reference on blameless
  post-mortems.
- **Sidney Dekker — *The Field Guide to Understanding
  'Human Error'*** —
  [sidneydekker.com](https://sidneydekker.com/books/) —
  the safety-science substrate on why single-cause
  narratives are usually wrong.

### RFC process

- **Michael Nygard — *Documenting Architecture
  Decisions*** —
  [cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) —
  the ADR template every RFC / architecture decision
  resolves into.
- **Rust RFCs — the reference implementation** —
  [github.com/rust-lang/rfcs](https://github.com/rust-lang/rfcs).
- **Python PEPs** —
  [peps.python.org](https://peps.python.org/) — the
  language-ecosystem RFC precedent.
- **Oxide Computer — Requests for Discussion (RFDs)** —
  [rfd.shared.oxide.computer](https://rfd.shared.oxide.computer/) —
  a modern, publicly-visible RFC process; see the
  bootstrap RFD at
  [oxide.computer/blog/rfd-1-requests-for-discussion](https://oxide.computer/blog/rfd-1-requests-for-discussion).

### Engineering handbook

- **GitLab Engineering Handbook** —
  [about.gitlab.com/handbook/engineering](https://about.gitlab.com/handbook/engineering/) —
  the public reference at large scale; note that
  it is far past the size a 5-15 team should read
  as a template.
- **Basecamp — *Getting Real*** —
  [basecamp.com/gettingreal](https://basecamp.com/gettingreal) —
  the reference for the small-team handbook shape.

### Planning cadence

- **David Anderson — *Kanban: Successful Evolutionary
  Change for Your Technology Business*** —
  [leankanban.com/kanban-books](http://leankanban.com/kanban-books/) —
  the load-bearing kanban reference.
- **The 2020 Scrum Guide** —
  [scrumguides.org](https://scrumguides.org/) —
  the current Scrum reference (16 pages, free).

## The 15→50 transition (chapter 03)

### First engineering manager

- **Camille Fournier — *The Manager's Path* — first-
  EM chapters** —
  [oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/).
- **Julie Zhuo — *The Making of a Manager*** —
  [juliezhuo.com/book](https://www.juliezhuo.com/book) —
  the design-industry perspective on first-time
  management, applicable across disciplines.

### Team Topologies and platform teams

- **Matthew Skelton and Manuel Pais — *Team
  Topologies*** —
  [teamtopologies.com](https://teamtopologies.com/) —
  the four team types (stream-aligned, enabling,
  complicated-subsystem, platform) and the three
  interaction modes (collaboration, X-as-a-service,
  facilitating).
- **Platform Engineering community** —
  [platformengineering.org](https://platformengineering.org/) —
  the community of practice for internal-developer-
  platform work.

### Career ladders

- **progression.fyi** —
  [progression.fyi](https://www.progression.fyi/) —
  a curated library of public engineering career
  ladders. The recommended starting point for
  reading three or four before authoring your own.
- **Kickstarter Engineering Ladder** —
  [github.com/kickstarter/eng-ladder](https://github.com/kickstarter/eng-ladder) —
  a well-known small-org public example.
- **CircleCI Engineering Competency Matrix** —
  [github.com/circleci/engineering-competencies](https://github.com/circleci/engineering-competencies) —
  a mid-size-org public example.
- **Camille Fournier — *An Incomplete List of Skills
  Senior Engineers Need Beyond Coding*** —
  [skamille.medium.com](https://skamille.medium.com/an-incomplete-list-of-skills-senior-engineers-need-beyond-coding-8ed6a940b6a5) —
  a widely-cited essay on the senior-IC dimensions
  a ladder should capture.

### First budget

- **Bessemer Venture Partners — *State of the Cloud*** —
  [bvp.com/atlas/state-of-the-cloud](https://www.bvp.com/atlas/state-of-the-cloud) —
  R&D-as-percent-of-revenue benchmarks by stage,
  used in the annual-budget defence.
- **a16z — Tech Topics (essays library)** —
  [a16z.com/tech-topics](https://a16z.com/tech-topics/) —
  operator-authored essays on engineering
  organisational design; useful for the
  first-EM / first-platform-team context.

## The 50→150 transition (chapter 04)

### Executive infrastructure

- **Camille Fournier — *The Manager's Path* — CTO /
  VP-Eng chapters** —
  [oreilly.com](https://www.oreilly.com/library/view/the-managers-path/9781491973882/).
- **Will Larson — *An Elegant Puzzle*** —
  [lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/) —
  the executive-work chapter is the load-bearing
  read on the 50-150 CTO / VP shape.
- **Will Larson — *Staff Engineer*** —
  [staffeng.com/book](https://staffeng.com/book) —
  the IC-tier counterpart shape at 50-150.
- **Lara Hogan — writings on engineering leadership** —
  [larahogan.me](https://larahogan.me/) — the *"first
  90 days"* playbook shape.

### Governance and decision-making

- **Michael Nygard — *Documenting Architecture
  Decisions*** —
  [cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) —
  the decision-log substrate for the governance
  council.
- **Amazon — *Have Backbone; Disagree and Commit*
  (Leadership Principle)** —
  [aws.amazon.com/executive-insights/content/leadership-principles-have-backbone-disagree-and-commit](https://aws.amazon.com/executive-insights/content/leadership-principles-have-backbone-disagree-and-commit/) —
  the vocabulary for the residual after a council
  decision.
- **Amazon — the working-backwards / PR-FAQ
  mechanism** —
  [aws.amazon.com/blogs/publicsector/tag/working-backwards](https://aws.amazon.com/blogs/publicsector/tag/working-backwards/) —
  the related pattern from the product side.
- **Colin Bryar and Bill Carr — *Working
  Backwards*** —
  [workingbackwards.com](https://www.workingbackwards.com/) —
  the two-pizza team and single-threaded leader
  patterns.

### Budget re-forecasting under macro pressure

- **Sequoia Capital — *Adapting to Endure*
  (2022)** —
  [sequoiacap.com/article/adapting-to-endure](https://www.sequoiacap.com/article/adapting-to-endure/) —
  the industry-standard writeup on the mechanics of
  budget re-forecasting under macro pressure.
- **Bessemer Venture Partners — *State of the Cloud*** —
  [bvp.com/atlas/state-of-the-cloud](https://www.bvp.com/atlas/state-of-the-cloud) —
  benchmark reference for the CFO conversation.

### Cross-team dependency management

- **Backstage** —
  [backstage.io](https://backstage.io/) — the
  open-source reference implementation of a service
  catalogue, originally from Spotify.
- **Team Topologies** —
  [teamtopologies.com](https://teamtopologies.com/) —
  the vocabulary the cross-team dependency map is
  authored against.

## DORA four keys (chapter 05)

### The primary references

- **DORA — DevOps Research and Assessment** —
  [dora.dev](https://dora.dev/) — the DORA program's
  home page.
- **DORA — Annual *State of DevOps Report*** —
  [dora.dev/research](https://dora.dev/research/) —
  the annual survey with the current-year
  performance bands.
- **DORA — quickcheck diagnostic** —
  [dora.dev/quickcheck](https://dora.dev/quickcheck/).
- **Nicole Forsgren, Jez Humble, Gene Kim —
  *Accelerate*** —
  [itrevolution.com/product/accelerate](https://itrevolution.com/product/accelerate/) —
  the book-length treatment.

### The metric-as-target failure mode

- **Marilyn Strathern — *'Improving Ratings': Audit
  in the British University System* (1997)** —
  [oro.open.ac.uk/22183](https://oro.open.ac.uk/22183/) —
  the paper that formulates *"when a measure becomes
  a target, it ceases to be a good measure"*, often
  cited as Goodhart's Law after Charles Goodhart's
  1975 monetary-policy paper.

### Complementary developer-experience frames

- **Nicole Forsgren, Margaret-Anne Storey, Chandra
  Maddila, Thomas Zimmermann, Brian Houck, Jenna
  Butler — *The SPACE of Developer Productivity*
  (ACM Queue, 2021)** —
  [queue.acm.org/detail.cfm?id=3454124](https://queue.acm.org/detail.cfm?id=3454124) —
  five dimensions (Satisfaction, Performance,
  Activity, Communication, Efficiency & flow).
- **Abi Noda, Margaret-Anne Storey, Nicole
  Forsgren, Michaela Greiler — *DevEx: What
  Actually Drives Productivity* (ACM Queue,
  2023)** —
  [queue.acm.org/detail.cfm?id=3595878](https://queue.acm.org/detail.cfm?id=3595878) —
  three dimensions (Feedback loops, Cognitive load,
  Flow state).

### Tooling

- **GoogleCloudPlatform/fourkeys** —
  [github.com/GoogleCloudPlatform/fourkeys](https://github.com/GoogleCloudPlatform/fourkeys) —
  the open-source reference implementation of the
  four-key computation.
- **Grafana** — [grafana.com](https://grafana.com/) —
  the dashboarding substrate most 15-50 orgs use.
- **OpenTelemetry** —
  [opentelemetry.io](https://opentelemetry.io/) —
  the CNCF vendor-neutral instrumentation standard.

### The SLI / SLO substrate (the tightening of DORA
stability)

- **Google SRE book — *Service Level Objectives*** —
  [sre.google/sre-book/service-level-objectives](https://sre.google/sre-book/service-level-objectives/).
- **Google SRE workbook — table of contents** —
  [sre.google/workbook/table-of-contents](https://sre.google/workbook/table-of-contents/).
- **Google SRE workbook — *Alerting on SLOs*** —
  [sre.google/workbook/alerting-on-slos](https://sre.google/workbook/alerting-on-slos/).

## Platform investment (chapter 06)

### The discipline references

- **Jez Humble and David Farley — *Continuous
  Delivery*** —
  [continuousdelivery.com](https://continuousdelivery.com/) —
  the load-bearing reference for the fast-reliable-
  test-suite and continuous-deployment disciplines.
- **Michael Nygard — *Release It! Design and Deploy
  Production-Ready Software* (2nd edition)** —
  [pragprog.com/titles/mnee2/release-it-second-edition](https://pragprog.com/titles/mnee2/release-it-second-edition/) —
  the load-bearing reference for the deploy /
  operations discipline.
- **Google SRE book — *Practical Alerting from
  Time-Series Data*** —
  [sre.google/sre-book/practical-alerting](https://sre.google/sre-book/practical-alerting/) —
  the load-bearing reference for the observability /
  alerting discipline.

### Feature flags

- **LaunchDarkly** —
  [launchdarkly.com](https://launchdarkly.com/) —
  the incumbent commercial option.
- **Unleash** —
  [getunleash.io](https://www.getunleash.io/) —
  leading open-source / hybrid alternative.
- **Flagsmith** —
  [flagsmith.com](https://www.flagsmith.com/) —
  open-source / hybrid alternative.
- **PostHog feature flags** —
  [posthog.com](https://posthog.com/) — product-
  analytics-integrated option.

### Progressive rollout / GitOps

- **Argo Rollouts** —
  [argoproj.github.io/argo-rollouts](https://argoproj.github.io/argo-rollouts/).
- **Flagger** —
  [flagger.app](https://flagger.app/).
- **Argo CD** —
  [argo-cd.readthedocs.io](https://argo-cd.readthedocs.io/en/stable/).
- **Flux** — [fluxcd.io](https://fluxcd.io/).
- **Spinnaker** —
  [spinnaker.io](https://spinnaker.io/).

### Observability stack

- **OpenTelemetry** —
  [opentelemetry.io](https://opentelemetry.io/);
  documentation at
  [opentelemetry.io/docs](https://opentelemetry.io/docs/).
- **Honeycomb** —
  [honeycomb.io](https://www.honeycomb.io/) —
  high-cardinality event tracing.
- **Grafana Tempo** —
  [grafana.com/oss/tempo](https://grafana.com/oss/tempo/) —
  distributed-tracing backend.
- **Grafana Cloud** —
  [grafana.com/products/cloud](https://grafana.com/products/cloud/).

### Developer platform / internal developer portal

- **Backstage** — [backstage.io](https://backstage.io/) —
  the open-source reference implementation, from
  Spotify.
- **Platform Engineering community** —
  [platformengineering.org](https://platformengineering.org/).
- **Team Topologies** —
  [teamtopologies.com](https://teamtopologies.com/) —
  the platform-team interaction mode.

### Multi-tenancy at scale (deferred to
`ai-infra-senior-architect`)

- **AWS Well-Architected — SaaS Lens** —
  [docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html](https://docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html) —
  the silo / pool / bridge multi-tenancy
  vocabulary named in chapter 06's deferral list.

## Delivery cadence, on-call, incident response (chapter 07)

### Incident response

- **Google SRE book — *Managing Incidents*** —
  [sre.google/sre-book/managing-incidents](https://sre.google/sre-book/managing-incidents/) —
  the incident command system (ICS) pattern.
- **Google SRE workbook — *Incident Response*** —
  [sre.google/workbook/incident-response](https://sre.google/workbook/incident-response/) —
  applied companion.
- **PagerDuty — Incident Response documentation** —
  [response.pagerduty.com](https://response.pagerduty.com/) —
  publicly published; one of the most-adapted
  playbooks in the industry.

### Status pages / customer communication

- **Atlassian Statuspage** —
  [statuspage.io](https://www.statuspage.io/) —
  the incumbent hosted status page.

### Blameless post-mortem (repeated from chapter 02)

- **Google SRE book — *Post-mortem Culture*** —
  [sre.google/sre-book/postmortem-culture](https://sre.google/sre-book/postmortem-culture/).
- **John Allspaw — *Blameless PostMortems and a
  Just Culture* (Etsy, 2012)** —
  [www.etsy.com/codeascraft/blameless-postmortems](https://www.etsy.com/codeascraft/blameless-postmortems).
- **Sidney Dekker — *The Field Guide to
  Understanding 'Human Error'*** —
  [sidneydekker.com](https://sidneydekker.com/books/).

## Adjacent-module references

- **`mod-101-cto-role-and-ownership-map`** — the CTO
  ladder and the shared reading vocabulary (Majors,
  Horowitz, Fournier, Larson). This module's
  stage-transition treatment extends the ownership
  map across the four transitions.
- **`mod-102-architecture-under-uncertainty`** — the
  ADR discipline (chapter 02), the C4 diagramming
  vocabulary (chapter 03), the monolith-first and
  evolutionary-architecture posture (chapter 01) —
  the substrate every chapter of this module
  references.
- **`mod-103-build-vs-buy-and-platform-economics`** —
  the earn-its-keep test at the heart of chapter 03
  artifact 2 (the first platform team) and chapter
  06 (platform-investment sizing) is authored in
  this adjacent module.
- **`mod-104-first-engineering-hires-and-team-topology`** —
  the hiring plan, the promote-vs-hire checklist for
  tech-lead / EM / VP, the org-chart artifact, the
  career ladder / comp band. This module is the
  *staging overlay* on top of mod-104's hiring
  substrate.
- **`mod-105-technical-debt-as-business-decision`** —
  the debt portfolio, the cost-to-carry / depreciation
  frame, the refactor budget. The debt inventory is
  where post-mortem action items land; the refactor
  budget funds the remediation. The DORA numbers are
  the aggregate signal that the debt portfolio's
  carry cost is or is not being paid down.
- **`mod-107-founder-scope-security-and-compliance`** —
  the on-call rotation, the blameless post-mortem,
  and the incident-response playbook are the
  operational substrate the SOC 2 Type I readiness
  checks assume.
- **`mod-108-cto-ceo-and-board-communication`** —
  the DORA numbers, the delivery-cadence spec, the
  budget re-forecast under investor pressure, and
  the stage-transition runbook all land in the
  board pre-read and the technical-DD data room.

## Higher-level tracks this module explicitly defers up to

- **`ai-infra-senior-architect`** (level 45) —
  [../../../ai-infra-senior-architect-learning](../../../ai-infra-senior-architect-learning) —
  deep multi-region / multi-tenant / high-scale
  architecture beyond the 50-150 CTO's scope. Owns
  the multi-region deploy control plane, the
  multi-tenancy isolation model (silo / pool /
  bridge — AWS SaaS Lens at
  [docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html](https://docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html)),
  the distributed-consensus / storage-layer choices
  for a scale-critical subsystem.
- **`ai-infra-principal-architect`** (level 55) —
  [../../../ai-infra-principal-architect-learning](../../../ai-infra-principal-architect-learning) —
  highest-altitude architectural depth for
  cross-region / multi-cloud / compliance-critical
  posture (FedRAMP, HIPAA at scale, SOC 2 Type II —
  with `mod-107` as the CTO-scope adjacent module).
- **`ai-infra-mlops`** (level 25) —
  [../../../ai-infra-mlops-learning](../../../ai-infra-mlops-learning) —
  MLOps platform depth beyond the CTO's build-vs-buy
  scope.
- **`ai-infra-ml-platform`** (level 30) —
  [../../../ai-infra-ml-platform-learning](../../../ai-infra-ml-platform-learning) —
  ML platform depth (feature store, serving mesh)
  beyond the CTO's build-vs-buy scope.

## Communities and ongoing peer-learning surfaces

- **CTO Craft** —
  [ctocraft.com](https://www.ctocraft.com/) —
  community of practice for CTOs across stages;
  recurring stage-transition retrospectives.
- **First Round Review** —
  [review.firstround.com](https://review.firstround.com/) —
  operator-authored essays on engineering-leadership
  transitions.
- **Lenny's Newsletter — Engineering / CTO track** —
  [lennysnewsletter.com](https://www.lennysnewsletter.com/).
- **Platform Engineering community** —
  [platformengineering.org](https://platformengineering.org/) —
  for the 15-50 and 50-150 platform-team charter
  vocabulary.

---

Full citations with `use` notes for the whole
curriculum are in
[`.aicg/job-requirements.json`](../../.aicg/job-requirements.json)
under `authoritative_references`.
