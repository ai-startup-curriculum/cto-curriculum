# Resources — mod-105-technical-debt-as-business-decision

Primary references for the topics covered in this module.
Every entry is linked to a publisher, an author-maintained
URL, or an official standards body. See
[`JOB_REQUIREMENTS.md`](../../JOB_REQUIREMENTS.md) for the
full authoritative-reference list that grounds the whole
curriculum.

## The debt metaphor and the Fowler quadrants (chapter 01)

- **Ward Cunningham** — *The WyCash Portfolio Management
  System* (OOPSLA '92 experience report — the original
  debt metaphor) —
  [c2.com/doc/oopsla92.html](http://c2.com/doc/oopsla92.html).
  One-page; read in full.
- **Ward Cunningham** — *Debt Metaphor* (2009 video
  clarification of the original intent) —
  [youtube.com/watch?v=pqeJFYwnkjE](https://www.youtube.com/watch?v=pqeJFYwnkjE).
  Cunningham himself distinguishing the *deliberate
  learning-and-refactor loan* from the modern default
  usage.
- **Martin Fowler** — *TechnicalDebtQuadrant* (2009
  bliki entry — the 2×2 that separates loans from bad
  debts) —
  [martinfowler.com/bliki/TechnicalDebtQuadrant.html](https://martinfowler.com/bliki/TechnicalDebtQuadrant.html).
- **Martin Fowler** — *TechnicalDebt* (bliki entry —
  the metaphor overview) —
  [martinfowler.com/bliki/TechnicalDebt.html](https://martinfowler.com/bliki/TechnicalDebt.html).
- **Steve McConnell** — *Managing Technical Debt* (2007
  post; unintentional vs. intentional framing) —
  [stevemcconnell.com/articles/technical-debt](https://stevemcconnell.com/articles/technical-debt/).
  Predates and overlaps Fowler's quadrants; useful when
  a stakeholder reaches for the McConnell vocabulary.

## Quality-attribute debt and ISO/IEC 25010 (chapter 02)

- **ISO/IEC 25010:2023 — SQuaRE Software Quality
  Model** —
  [iso.org/standard/78176](https://www.iso.org/standard/78176.html).
  The 2023 revision behind the ISO paywall for the full
  text; the abstract and scope are free.
- **ISO 25000 portal** —
  [iso25000.com — ISO/IEC 25010](https://iso25000.com/index.php/en/iso-25000-standards/iso-25010).
  A browsable reference to the ISO/IEC 25010
  characteristics and sub-characteristics, maintained by
  the SQuaRE community.
- **Sandi Metz** — *The Wrong Abstraction* (2016) —
  [sandimetz.com/blog/2016/1/20/the-wrong-abstraction](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction).
  The canonical short essay on why duplication is
  cheaper than the wrong abstraction — foundational for
  the *structural debt* family.
- **Eric Evans** — *Domain-Driven Design*
  ([domainlanguage.com/ddd](https://www.domainlanguage.com/ddd/)).
  The classical reference on aggregate boundaries and
  bounded contexts — the vocabulary structural-debt
  items are usually described in.
- **Ford, Parsons, Kua** — *Building Evolutionary
  Architectures* —
  [oreilly.com](https://www.oreilly.com/library/view/building-evolutionary-architectures/9781491986356/).
  Fitness-function-driven architecture that reasons
  about the adjacent-decision compounder from chapter 03.

## Cost-to-carry, DORA, and engineering productivity (chapter 03)

- **DORA — DevOps Research and Assessment** —
  [dora.dev](https://dora.dev/). The four-key
  measurements (Deployment Frequency, Lead Time for
  Changes, Change Failure Rate, MTTR) used in the
  lead-time tax source. See also *State of DevOps
  Report* annual publications.
- **Forsgren, Humble, Kim** — *Accelerate: The Science
  of Lean Software and DevOps* —
  [itrevolution.com — Accelerate](https://itrevolution.com/product/accelerate/).
  The book-length reference for DORA.
- **Nicole Forsgren, Margaret-Anne Storey, Chandra
  Maddila, Thomas Zimmermann, Brian Houck, Jenna
  Butler** — *The SPACE of Developer Productivity*
  (2021, ACM Queue) —
  [queue.acm.org/detail.cfm?id=3454124](https://queue.acm.org/detail.cfm?id=3454124).
  Broader productivity vocabulary for the morale /
  attrition source that DORA alone does not cover.
- **Winters, Manshreck, Wright (eds.)** — *Software
  Engineering at Google* (chapter: *"Software
  Engineering is Programming Integrated Over Time"*) —
  [abseil.io/resources/swe-book](https://abseil.io/resources/swe-book).
  Free online. The canonical treatment of the
  compounding of decisions over time.

## Refactor budget and engineering-time allocation (chapter 04)

- **Will Larson** — *An Elegant Puzzle: Systems of
  Engineering Management* —
  [lethain.com/elegant-puzzle](https://lethain.com/elegant-puzzle/).
  Systems for allocating engineering time across
  categories; the "explicit allocation" discipline the
  refactor budget uses.
- **Michael Feathers** — *Working Effectively with
  Legacy Code* —
  [informit.com — WELC](https://www.informit.com/store/working-effectively-with-legacy-code-9780131177055).
  Empirical reality of the fraction of feature-work
  velocity at which legacy refactoring proceeds.
- **Winters, Manshreck, Wright (eds.)** — *Software
  Engineering at Google* — engineering-productivity /
  sustainable-software-engineering chapters —
  [abseil.io/resources/swe-book](https://abseil.io/resources/swe-book).

## Deprecate / Rewrite / Leave — Chesterton, Fowler, Newman, Spolsky (chapter 05)

- **G. K. Chesterton** — *The Thing* (1929) — the
  Chesterton's Fence discipline. Public-domain full
  text at
  [gutenberg.ca — Chesterton, *The Thing*](https://gutenberg.ca/ebooks/chestertongk-thething/chestertongk-thething-00-h.html).
- **Martin Fowler** — *StranglerFigApplication* —
  [martinfowler.com/bliki/StranglerFigApplication.html](https://martinfowler.com/bliki/StranglerFigApplication.html).
  The canonical incremental-migration pattern for the
  rewrite response.
- **Martin Fowler** — *MonolithFirst* —
  [martinfowler.com/bliki/MonolithFirst.html](https://martinfowler.com/bliki/MonolithFirst.html).
  The bracketing pattern: start with a monolith,
  extract via strangler when the seam is real.
- **Sam Newman** — *Monolith to Microservices* —
  [samnewman.io/books/monolith-to-microservices](https://samnewman.io/books/monolith-to-microservices/).
  The book-length treatment of the strangler-fig
  pattern applied to the service-extraction case.
- **Sam Newman** — *Building Microservices, 2nd
  edition* —
  [samnewman.io/books/building_microservices_2nd_edition](https://samnewman.io/books/building_microservices_2nd_edition/).
  The reference for when NOT to adopt microservices —
  useful for the deprecate-vs-rewrite framing.
- **Joel Spolsky** — *Things You Should Never Do,
  Part I* (2000) —
  [joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/).
  20 years old, three pages, every paragraph still
  applies. Required reading before any rewrite memo.
- **Marty Cagan** — *Inspired* and *Empowered* —
  [svpg.com/books](https://www.svpg.com/books/). The
  product-decision framing for the sunset-schedule
  side of a deprecation.

## Debt inventory and portfolio decision log (chapter 06)

- **Michael Nygard** — *Documenting Architecture
  Decisions* (the ADR pattern) —
  [cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions).
  The four-section ADR template the decision-log
  entries reuse.
- **Nat Pryce** — `adr-tools` —
  [github.com/npryce/adr-tools](https://github.com/npryce/adr-tools).
  Reference CLI for the Nygard template; also fine for
  the portfolio decision log.
- **MADR — Markdown Architectural Decision Records** —
  [adr.github.io](https://adr.github.io/). A slightly
  more structured variant of Nygard's template.
- **Andreessen Horowitz** — *Technical Due Diligence
  Checklist* —
  [a16z.com/tech-diligence-checklist](https://a16z.com/tech-diligence-checklist/).
  The public-facing tech-DD reference; the debt-
  inventory + decision-log is one of the artifacts a
  Series-B DD reviewer asks for by name.

## Higher-level architectural depth (deferred up, chapters 05 and 06)

- **`ai-infra-senior-architect`** (level 45) —
  [../../../ai-infra-senior-architect-learning](../../../ai-infra-senior-architect-learning) —
  deep multi-region / multi-tenant / high-scale
  refactor and system-extraction mechanics beyond the
  pre-Series-A CTO's scope.
- **`ai-infra-principal-architect`** (level 55) —
  [../../../ai-infra-principal-architect-learning](../../../ai-infra-principal-architect-learning) —
  highest-altitude architectural depth; distributed-
  consensus / multi-region / multi-tenancy-model
  rewrites at scale.
- **`ai-infra-principal-engineer`** (level 50) —
  [../../../ai-infra-principal-engineer-learning](../../../ai-infra-principal-engineer-learning) —
  principal-scope engineering-craft depth on the
  StranglerFig migration mechanics themselves.
- **AWS SaaS Lens (Well-Architected)** —
  [docs.aws.amazon.com/wellarchitected/latest/saas-lens](https://docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html) —
  the multi-tenant isolation vocabulary (silo / pool /
  bridge) referenced in the chapter 05 boundary
  section.

## Adjacent-module references

- **`mod-101-cto-role-and-ownership-map`** — the CTO
  ladder and the shared reading vocabulary the debt
  conversation runs on top of.
- **`mod-102-architecture-under-uncertainty`** —
  chapter 01 (MonolithFirst / StranglerFig / the
  evolutionary posture the debt metaphor lives inside),
  chapter 02 (ADRs — the Nygard template the decision
  log reuses), chapter 04 (ISO/IEC 25010 — the
  quality-attribute-debt family's vocabulary), chapter
  05 (modular-monolith vs. services — the target shape
  many structural-debt rewrites aim at).
- **`mod-103-build-vs-buy-and-platform-economics`** —
  build-vs-buy decisions are one source of downstream
  debt (a "build" that failed to earn its keep becomes
  the deprecation candidate; a "buy" that has become
  a vendor-lock issue becomes a structural debt item).
- **`mod-104-first-engineering-hires-and-team-topology`** —
  chapter 01 (the hiring plan the refactor budget
  interacts with), chapter 03 (the founding-engineer
  profile that guards against the Inadvertent-Reckless
  quadrant), chapter 04 (the topology whose ownership
  vacuums are structural debt).
- **`mod-106-scaling-org-and-stack`** — DORA four-key
  metrics as the org-level symptom aggregate cost-to-
  carry manifests as; the stage-transition playbooks
  the debt portfolio is an input to.
- **`mod-107-founder-scope-security-and-compliance`** —
  security debt as a quality-attribute-debt subclass
  (chapter 02) whose business owner is often the CEO
  in the compliance-lead capacity.
- **`mod-108-cto-ceo-and-board-communication`** —
  chapter 04 (board pre-read) is where the one-page
  portfolio summary from this module lands.

---

Full citations with `use` notes for the whole curriculum
are in [`.aicg/job-requirements.json`](../../.aicg/job-requirements.json)
under `authoritative_references`.
