# The C4 Model at Stakeholder-Appropriate Depth

> Simon Brown's positioning of the C4 model
> ([c4model.com](https://c4model.com/)): a set of hierarchical
> abstractions — System Context, Container, Component, Code —
> that software teams use to think and communicate about the
> architecture of a software system at the level of zoom the
> audience actually needs.

## Motivation

Every startup ends up with two kinds of architecture diagrams,
neither of which is very useful:

- The **investor-deck box-and-arrow diagram** — a colourful
  hand-drawn picture that shows "our AI platform" as a big
  central box connected to "customers" and "data". No
  engineer can implement from it; no due-diligence reviewer
  can evaluate it.
- The **whiteboard photo the CTO refuses to throw away** — an
  unlabelled snarl of arrows between database icons and cloud
  logos, meaningful only to the two engineers who were in the
  room when it was drawn. New hires bounce off it; when the
  original authors leave, the diagram becomes archaeology.

Simon Brown's C4 model
([c4model.com](https://c4model.com/)) exists so that neither
diagram has to be the artifact the CTO puts in front of a
stakeholder. C4 defines four levels of increasing zoom — System
Context, Container, Component, Code — and the load-bearing
rule is that **you use the level of zoom appropriate to the
audience**, not the level of zoom that shows off how much you
know about the system.

For the pre-seed / seed CTO, C4 does three jobs:

- Gives you a **shared diagramming vocabulary** so the
  team's diagrams are readable by anyone who has seen the
  model before (which, increasingly, is any experienced
  engineer or technical due-diligence reviewer).
- Forces you to **draw the right diagram for the right
  audience** — an investor sees the System Context diagram;
  a new engineer sees the Container and Component diagrams;
  nobody sees a Level-4 Code diagram because tools generate
  them from the code.
- **Pairs cleanly with ADRs.** The C4 diagrams show the
  *current* structure; the ADRs explain *why* the structure
  is that shape and what the alternatives were. Chapter 02
  discussed the ADR side; this chapter discusses the diagram
  side.

## The four levels

The C4 model is a *hierarchical* set of abstractions. Each
level zooms one step further into the previous level. Simon
Brown's canonical description
([c4model.com/introduction](https://c4model.com/introduction))
is worth reading in full; the summary below is enough to run
the paired exercise.

### Level 1: System Context

A single **System Context** diagram shows the software system
you own as a black box, sitting in an environment of **users**
and **other systems**.

- **What's on it:** exactly one box for *your* system, plus
  boxes for every category of user who interacts with it, plus
  boxes for every external system it depends on or is
  consumed by.
- **What's *not* on it:** anything inside your system. No
  microservices, no databases, no queues, no cloud provider.
- **Audience:** anyone who is not going to write code against
  the system this quarter — investors, board members, first
  design partners, non-technical co-founders, external
  advisors, technical due-diligence reviewers doing the first
  pass. This is the "one diagram to explain what we do"
  diagram.
- **How many:** one per software system. A pre-seed / seed
  startup usually owns exactly one software system, so it
  owns exactly one System Context diagram.

### Level 2: Container

A **Container** diagram zooms into the single box from the
System Context diagram and shows the deployable / runnable
units inside it — web applications, mobile apps, server-side
services, databases, file stores, message queues.

- **What's on it:** every runnable / deployable unit inside
  the system, plus the technology choice and the primary
  communication protocol between each pair. A container is a
  thing you would run — a Django app, a Postgres database, a
  React SPA, a background-worker process, a Redis instance.
- **Important:** "container" here is a Brown-C4 term of art
  and does **not** mean "Docker container". A Postgres RDS
  instance is a container in C4 terms; whether it is
  containerised in the Docker sense is a Level 3 concern.
- **Audience:** every engineer on the team; a new hire on
  day one; a technical advisor; a technical due-diligence
  reviewer on a deeper pass. This is the "understand the
  moving parts" diagram.
- **How many:** typically one per system. If you have
  multiple systems (rare at pre-seed), one per system.

### Level 3: Component

A **Component** diagram zooms into a single container from
the Container diagram and shows the major logical building
blocks inside it — the components a developer would recognise
in the code.

- **What's on it:** the major logical components inside one
  container. In a modular-monolith Django app (see chapter
  01), a Component diagram would show `identity`, `billing`,
  `catalog`, `worker`, and the interfaces between them.
- **Audience:** engineers working on that specific container.
  A frontend engineer does not read the backend Component
  diagram; a backend engineer reads only the containers they
  work in.
- **How many:** one per container that is complex enough to
  need it — usually the monolith container itself, sometimes
  a rich single-page-app container, rarely anything else at
  pre-seed / seed.

### Level 4: Code

A **Code** diagram (UML class diagram, ER diagram, or the
equivalent) zooms into a single component and shows how it
is implemented at the class / interface / table level.

- **Audience:** whoever is writing the component. Nobody
  else.
- **How many:** almost never hand-drawn. If you want one,
  generate it from the code with an IDE or a tool
  (Structurizr, PlantUML from source, or the IDE's built-in
  class-diagram generator). A stale Level-4 diagram is
  worse than none, and hand-drawn Level-4 diagrams go
  stale within a week.

For most pre-seed / seed startups, **you author the C4 Levels
1-3 and skip Level 4 entirely**. Level 4 is where the C4
discipline pays off precisely because it is not required —
the argument is that if you have a coherent Level 1-3 set,
Level 4 is just "read the code".

## The audience-first rule

The most important thing to internalise from the C4 model is
that **the level you draw is chosen by the audience, not by
the author**.

| Audience | Level(s) they consume |
|---|---|
| Investor / board member / press / prospective customer | System Context (Level 1) |
| Non-technical co-founder | System Context (Level 1) |
| Technical advisor / due-diligence first pass | System Context + Container (Levels 1-2) |
| New engineering hire on day one | Container (Level 2) + Component for the parts they'll touch (Level 3) |
| Engineer implementing a change | Component (Level 3), and the code |
| Technical due-diligence deep pass | All of Levels 1-3, plus the ADRs from chapter 02 |

The failure mode this rule guards against: the CTO who
shows the board a Level-3 Component diagram of the auth
system and wonders why the board's eyes glaze over. The
board wanted the Level-1 System Context diagram plus one
sentence per external system dependency. The Level-3
Component diagram is for the engineer being onboarded, not
the board.

## What a C4 diagram *actually* looks like

The C4 site is deliberately notation-agnostic, but there is
a canonical visual style — a legend, a colour convention,
box-and-line with the label on the line showing the protocol
and the direction. The **notation cheat sheet** at
[c4model.com/diagrams/notation](https://c4model.com/diagrams/notation)
is the reference; Brown's *Visualising Software Architecture*
book expands on it.

The important rules:

- **Every diagram has a title, a scope, and a legend.** No
  exceptions. A diagram without a legend is a diagram whose
  audience is guessing.
- **Every element has a name, a type, and (optionally) a
  one-line description.** "Postgres" is not enough; "Postgres
  (RDBMS) — stores customer, billing, and catalog data" is.
- **Every line has a label and a direction.** "Reads/writes
  via HTTPS/JSON" or "Sends invoices via SES SMTP". A line
  without a label is a line whose meaning is guessing.
- **Elements not in the diagram's scope are shown greyed out
  or excluded.** A Container diagram does not show external
  users; a System Context diagram does not show internal
  containers.

## Tooling that helps but is not required

As with ADRs, C4 is a discipline; the tool is secondary. The
tools worth naming:

- **Structurizr** — [structurizr.com](https://structurizr.com/) —
  Simon Brown's own tooling. Text-DSL that renders to all four
  levels; free tier is enough for most pre-seed / seed
  startups. The "diagrams as code" model plays well with the
  in-repo ADR discipline.
- **PlantUML with the C4 macros** —
  [github.com/plantuml-stdlib/C4-PlantUML](https://github.com/plantuml-stdlib/C4-PlantUML) —
  free, open source, renders inside `.md` previews in many
  IDEs. The C4-PlantUML library implements the canonical
  notation.
- **Mermaid** — [mermaid.js.org](https://mermaid.js.org/) —
  built into GitHub Markdown rendering. Mermaid's C4 support
  is younger than PlantUML's but the rendering-in-GitHub-PRs
  ergonomics matter more than notation completeness at this
  stage.
- **Excalidraw / Miro / whiteboard photo** — fine for the
  first-pass sketch during a spike (see chapter 06). *Not*
  the format the final in-repo diagram lives in — a
  hand-drawn PNG has no diff and no legend enforcement.

Pick one and use it consistently. Do not run three notations
in parallel; the point of C4 is a shared vocabulary, which
degrades when there are three of them.

## Where the diagrams live

The convention that pairs cleanly with the ADR discipline is
`docs/architecture/` in the same repo:

```
docs/
  adr/
    0001-use-postgres-for-primary-datastore.md
    ...
    README.md               # ADR index
  architecture/
    01-system-context.md    # Level 1, with embedded PlantUML or link to Structurizr workspace
    02-container.md         # Level 2
    03-component-monolith.md  # Level 3, one per non-trivial container
    README.md               # architecture-doc index
```

The Level 1 System Context diagram is the one Sunday-night
diagram every engineer, advisor, and design partner should
be able to find without asking; it belongs at the top of the
repo `README.md` in most cases.

## How C4 diagrams and ADRs reinforce each other

C4 diagrams and ADRs are two views of the same architecture:

- **The C4 diagram shows *what* the current architecture
  looks like.** It is a snapshot.
- **The ADR explains *why* the architecture has that shape
  and what the alternatives were.** It is a history.

Concretely, the Container diagram (Level 2) that shows one
monolith container with a Postgres container next to it
should carry a footnote pointing at ADR-0001 (Postgres) and
ADR-0003 (modular monolith first). The reader who wants to
know *why* the diagram shows one database and one monolith
follows the ADR link; the reader who wants to know *what*
the current state is reads the diagram.

When the ADR is superseded, the diagram is updated in the
same PR. When the diagram is updated, the PR references the
ADR that authorises the change (or opens a new one). The
discipline that keeps these in sync is the same discipline
that keeps the ADRs from becoming a dead index.

## Common failure modes

- **Level-3 diagrams for a Level-1 audience.** The CTO
  presenting the Component diagram to the board. The fix
  is to check the audience before opening the tool.
- **The single "architecture diagram" that tries to be all
  four levels at once.** Boxes inside boxes inside boxes,
  arrows crossing arrows. Split it into a proper Level 1,
  Level 2, and Level 3 set.
- **Undocumented notation.** No legend, no colours defined,
  no protocol on the lines. Reader guesses. Reader guesses
  wrong.
- **Static export that goes stale.** A screenshot of a
  Miro board committed as a PNG that no one can edit
  without the original creator's Miro account. Prefer
  diagram-as-code so the diff shows up in PRs.
- **Level 4 hand-drawn diagrams.** Almost always stale by
  the second month. Skip them or generate them from source.

## Summary

- The C4 model has four levels — **System Context /
  Container / Component / Code** — from most zoomed-out to
  most zoomed-in.
- **Draw the level your audience consumes**, not the level
  that shows off how much you know. Investors read
  System Context; new engineers read Container + Component;
  Code diagrams are generated, not authored.
- Every diagram carries a title, a scope, and a legend;
  every element has a name and a type; every line has a
  label and a direction.
- C4 diagrams show *what* the architecture is; ADRs
  (chapter 02) explain *why*. Each diagram cites the ADRs
  that authorise the shape; each ADR is a candidate to be
  superseded when the diagram changes.
- Skip Level 4 as a hand-drawn artifact at pre-seed / seed.
  If you need it, generate it from the code.

The chapter's paired exercise —
[`exercise-03-c4-diagram-set-for-one-startup.md`](exercises/exercise-03-c4-diagram-set-for-one-startup.md)
— walks the authoring of a System Context + Container +
Component diagram set for one startup at the depth each
stakeholder audience actually consumes.
