# Resources — mod-102-architecture-under-uncertainty

Primary references for the topics covered in this module.
Every entry is linked to a publisher, an author-maintained
URL, or an official standards body. See
[`JOB_REQUIREMENTS.md`](../../JOB_REQUIREMENTS.md) for the
full authoritative-reference list that grounds the whole
curriculum.

## Architecture Decision Records (chapter 02)

- **Michael Nygard** — *Documenting Architecture Decisions*
  ([cognitect.com/blog/2011/11/15/documenting-architecture-decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)) —
  the original ADR essay; the four-section template every
  ADR tool has since inherited.
- **Nat Pryce** — `adr-tools`
  ([github.com/npryce/adr-tools](https://github.com/npryce/adr-tools)) —
  the reference CLI for the Nygard template. `adr new
  "title"` creates a numbered, dated, filled-in ADR.
- **MADR — Markdown Architectural Decision Records** —
  [adr.github.io](https://adr.github.io/) — a slightly more
  structured variant of Nygard's template, with active
  community and IDE plugins.
- **Thomas Vaillant** — `log4brains`
  ([github.com/thomvaill/log4brains](https://github.com/thomvaill/log4brains)) —
  static-site generator for browsing an ADR log; useful
  once the ADR set outgrows a single index README.
- **ThoughtWorks Technology Radar — 'Lightweight
  Architecture Decision Records'** —
  [thoughtworks.com/radar/techniques/lightweight-architecture-decision-records](https://www.thoughtworks.com/en-us/radar/techniques/lightweight-architecture-decision-records) —
  the entry that moved ADRs into "Adopt" and popularised
  the pattern beyond the original Nygard essay.

## MonolithFirst / Strangler-Fig / Evolutionary Architecture (chapter 01)

- **Martin Fowler** — *MonolithFirst* —
  [martinfowler.com/bliki/MonolithFirst.html](https://martinfowler.com/bliki/MonolithFirst.html) —
  the canonical argument for starting with a monolith.
- **Martin Fowler** — *StranglerFigApplication* —
  [martinfowler.com/bliki/StranglerFigApplication.html](https://martinfowler.com/bliki/StranglerFigApplication.html) —
  the pattern for incremental extraction from a monolith
  when the extraction is finally worth doing.
- **Neal Ford, Rebecca Parsons, Patrick Kua et al.** —
  *Building Evolutionary Architectures* —
  [oreilly.com](https://www.oreilly.com/library/view/building-evolutionary-architectures/9781491986356/) —
  the book-length reference for fitness functions and
  evolvability. Check the O'Reilly catalog for the current
  edition; the reference above is the original 2017 edition.
- **ThoughtWorks — 'Evolutionary architecture'** —
  [thoughtworks.com/insights/blog/microservices/evolutionary-architecture](https://www.thoughtworks.com/en-us/insights/blog/microservices/evolutionary-architecture) —
  short-form primer on the fitness-function vocabulary from
  Ford, Parsons, Kua.

## C4 Model (chapter 03)

- **Simon Brown** — C4 Model for visualising software
  architecture — [c4model.com](https://c4model.com/) —
  the canonical model site. The
  [introduction](https://c4model.com/introduction) and
  [notation cheat sheet](https://c4model.com/diagrams/notation)
  pages are the two most useful starting points.
- **Structurizr** — [structurizr.com](https://structurizr.com/) —
  Simon Brown's own diagrams-as-code tooling. Free tier
  covers most pre-seed / seed startups.
- **C4-PlantUML** —
  [github.com/plantuml-stdlib/C4-PlantUML](https://github.com/plantuml-stdlib/C4-PlantUML) —
  PlantUML macros implementing the canonical C4 notation;
  works with any PlantUML renderer.
- **Mermaid — C4 syntax** —
  [mermaid.js.org/syntax/c4.html](https://mermaid.js.org/syntax/c4.html) —
  Mermaid's C4 support, which renders inline in GitHub
  Markdown.

## ISO/IEC 25010 quality attributes (chapter 04)

- **ISO/IEC 25010:2023 — SQuaRE Software Quality Model** —
  [iso.org/standard/78176](https://www.iso.org/standard/78176.html) —
  the 2023 revision of the standard. Behind an ISO paywall
  for the full text; the abstract and scope are free.
- **ISO 25000 portal** —
  [iso25000.com — ISO/IEC 25010](https://iso25000.com/index.php/en/iso-25000-standards/iso-25010) —
  a browsable reference to the ISO/IEC 25010
  characteristics and sub-characteristics, maintained by
  the SQuaRE community. Useful when the ISO PDF is not
  available.
- **Software Engineering Institute (SEI) — Attribute-Driven
  Design and ATAM** —
  [insights.sei.cmu.edu — ATAM collection](https://insights.sei.cmu.edu/library/architecture-tradeoff-analysis-method-collection/) —
  adjacent trade-off-analysis vocabulary; ATAM is worth
  knowing exists even at seed stage.
- **AWS Well-Architected Framework** —
  [aws.amazon.com/architecture/well-architected](https://aws.amazon.com/architecture/well-architected/) —
  a widely-adopted vendor take on quality attributes
  (their "pillars") with concrete AWS-flavoured checklists.
- **Google — Site Reliability Engineering** —
  [sre.google/books](https://sre.google/books/) — the SRE
  book and workbook for the reliability sub-characteristic
  vocabulary (SLIs / SLOs / error budgets).

## Monolith → services and CAP theorem (chapter 05)

- **Sam Newman** — *Building Microservices, 2nd edition* —
  [samnewman.io/books/building_microservices_2nd_edition](https://samnewman.io/books/building_microservices_2nd_edition/) —
  the canonical reference on when (and when not) to
  extract services from a monolith.
- **Sam Newman** — *Monolith to Microservices* —
  [samnewman.io/books/monolith-to-microservices](https://samnewman.io/books/monolith-to-microservices/) —
  companion volume specifically on the extraction pattern.
- **Eric Brewer** — *Towards Robust Distributed Systems*
  (PODC 2000 keynote — the original CAP conjecture) —
  [sites.cs.ucsb.edu — Brewer PODC 2000](https://sites.cs.ucsb.edu/~rich/class/cs293b-cloud/papers/Brewer_podc_keynote_2000.pdf).
- **Seth Gilbert and Nancy Lynch** — *Brewer's Conjecture
  and the Feasibility of Consistent, Available,
  Partition-Tolerant Web Services* (SIGACT 2002 — the
  proof) —
  [groups.csail.mit.edu — Gilbert & Lynch 2002](https://groups.csail.mit.edu/tds/papers/Gilbert/Brewer2.pdf).
- **Eric Brewer** — *CAP Twelve Years Later: How the
  Rules Have Changed* (IEEE Computer, June 2012) —
  [sites.cs.ucsb.edu — Brewer 2012](https://sites.cs.ucsb.edu/~rich/class/cs293b-cloud/papers/Brewer_computer_2012.pdf) —
  the retrospective that clarifies the common
  misinterpretations.
- **Daniel Abadi** — *Consistency Tradeoffs in Modern
  Distributed Database System Design* (IEEE Computer,
  February 2012 — the PACELC refinement) —
  [cs.umd.edu — Abadi PACELC](https://www.cs.umd.edu/~abadi/papers/abadi-pacelc.pdf).
- **Werner Vogels** — *Eventually Consistent* (2008) —
  [allthingsdistributed.com/2008/12/eventually_consistent.html](https://www.allthingsdistributed.com/2008/12/eventually_consistent.html) —
  the shortest useful reference on the
  eventual-consistency vocabulary.
- **Martin Kleppmann** — *Designing Data-Intensive
  Applications* —
  [dataintensive.net](https://dataintensive.net/) — the
  book-length reference on persistence choices, from
  storage engines to replication to consistency models.

## Spikes and time-boxed experiments (chapter 06)

- **Extreme Programming — Spike Solutions** —
  [extremeprogramming.org/rules/spike.html](http://www.extremeprogramming.org/rules/spike.html) —
  the original definition; still the shortest useful
  reference.
- **Kent Beck** — *Extreme Programming Explained, 2nd
  edition* —
  [informit.com — XP Explained](https://www.informit.com/store/extreme-programming-explained-embrace-change-9780321278654) —
  the book-length source for the spike vocabulary in the
  XP tradition.
- **Scaled Agile Framework — Spikes** —
  [scaledagileframework.com — Spikes](https://scaledagileframework.com/spikes/) —
  the modern reformulation of the pattern inside SAFe;
  useful if your organisation already uses that vocabulary.

## Team Topologies (referenced in chapters 01 and 05)

- **Matthew Skelton and Manuel Pais** — *Team Topologies* —
  [teamtopologies.com/book](https://teamtopologies.com/book) —
  the reference for team-topology patterns; used in
  chapter 05 to name the "team-topology divergence"
  extraction trigger.

## Higher-level architectural depth (deferred up, chapters 05 and 06)

- **`ai-infra-senior-architect`** (level 45) —
  [../../../ai-infra-senior-architect-learning](../../../ai-infra-senior-architect-learning) —
  deep multi-region / multi-tenant / high-scale
  architecture beyond the pre-seed / seed CTO's scope.
- **`ai-infra-principal-architect`** (level 55) —
  [../../../ai-infra-principal-architect-learning](../../../ai-infra-principal-architect-learning) —
  highest-altitude architectural depth; distributed
  consensus and full multi-cloud / multi-region posture.
- **AWS SaaS Lens (Well-Architected)** —
  [docs.aws.amazon.com/wellarchitected/latest/saas-lens](https://docs.aws.amazon.com/wellarchitected/latest/saas-lens/saas-lens.html) —
  the multi-tenant-isolation vocabulary (silo / pool /
  bridge) the seed-stage CTO recognises and defers up on.
- **Google Cloud Architecture Center** —
  [cloud.google.com/architecture](https://cloud.google.com/architecture) —
  reference architectures and pattern library for
  cloud-native systems.
- **Microsoft Azure Architecture Center — patterns** —
  [learn.microsoft.com/azure/architecture/patterns](https://learn.microsoft.com/en-us/azure/architecture/patterns/) —
  vendor-neutral catalogue of cloud-native architectural
  patterns.

## Adjacent-module references

- **`mod-101-cto-role-and-ownership-map`** — the CTO
  ladder, the shared reading vocabulary (Majors,
  Horowitz, Fournier, Larson). Chapter 05 of that module
  is required reading before chapter 06 of this one.
- **`mod-103-build-vs-buy-and-platform-economics`** — the
  build-vs-buy side of every ADR authored in exercise 02
  of this module. Mod-103's vendor-selection scorecard
  builds on the Bucket-B ADR from that exercise.
- **`mod-105-technical-debt-as-business-decision`** — the
  deprecate-vs-rewrite decision on load-bearing legacy
  code uses the same StranglerFig pattern chapter 01 of
  this module introduces.
- **`mod-108-cto-ceo-and-board-communication`** — the
  technical-narrative and technical-due-diligence
  material builds on the ADR index and C4 diagram set
  authored in this module's exercises.

---

Full citations with `use` notes for the whole curriculum are
in [`.aicg/job-requirements.json`](../../.aicg/job-requirements.json)
under `authoritative_references`.
