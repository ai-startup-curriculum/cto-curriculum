# Exercise 03 — C4 Diagram Set for One Startup

**Module:** `mod-102-architecture-under-uncertainty`
**Planned time:** ~3 hours
**Chapter this builds on:** [`03-c4-model-at-stakeholder-appropriate-depth.md`](../03-c4-model-at-stakeholder-appropriate-depth.md)

## Problem statement

Author a **coherent C4 diagram set** — one **System Context**
diagram, one **Container** diagram, and one **Component**
diagram — for a single real startup: yours, or a real
reference startup whose product and moving parts you
understand well enough to draw honestly.

The point of the drill is not to produce three diagrams. It
is to build the muscle of choosing **the level of zoom the
audience actually consumes** — and to end the exercise with
an artifact set the CTO can hand to (a) an investor / board
member, (b) a new engineering hire on day one, and (c) an
engineer implementing a change inside one of the
containers, without any of them having to squint.

## Requirements

Produce **three diagrams**, in a diagram-as-code format
committed to a real (or scratch) repo, plus a short
**diagram legend** that documents your notation choices.

### 1. The System Context diagram (Level 1)

- Exactly **one box** for your software system.
- Boxes for every **category of user** who interacts with it
  (buyer, admin, internal ops, third-party integrator, etc.
  — not individual users).
- Boxes for every **external system** it depends on or is
  consumed by (auth vendor, payments, foundation-model API,
  email, analytics-warehouse, buyer's ERP, etc.).
- **Nothing inside** the your-system box. No microservices,
  no databases, no queues.
- Every line labelled with the primary interaction ("Sends
  invoices via SMTP", "Reads user profile via HTTPS/JSON").
- Legend visible on the diagram itself.

### 2. The Container diagram (Level 2)

- Every **runnable / deployable unit** inside your system —
  web app, mobile app, backend service(s), databases, file
  stores, message queues, background workers.
- The **technology choice** for each container (e.g.
  "Django 5, Python 3.13", "Postgres 16 on RDS",
  "Next.js 14 on Vercel"). Remember: "container" here is
  Brown-C4 language, not Docker.
- The **primary communication protocol** on every line
  between containers ("HTTPS/JSON", "SQL over TLS",
  "Redis RESP", "SQS message").
- External systems from the System Context diagram shown
  as greyed-out edge boxes for context.
- Legend visible on the diagram itself.

### 3. The Component diagram (Level 3)

Zoom into the **single most complex container** from the
Container diagram — usually the backend monolith or the
richest single-page app — and draw its major logical
components.

- Modules / packages the codebase actually has (or would
  have if you built to your exercise-01 call): e.g.
  `identity/`, `billing/`, `catalog/`, `worker/` for a
  modular-monolith Django app.
- Cross-module interfaces (the service classes, domain
  events, or async queues that mediate calls between
  modules).
- External systems that this specific container talks to,
  greyed out on the edge.
- Legend visible on the diagram itself.

You do **not** need to author a Level-4 Code diagram. If
you want one, generate it from the code — see chapter 03.

### The diagram legend

A short (~half-page) document — `docs/architecture/README.md`
is a good home — that names:

- The **notation** you are using (Structurizr DSL,
  C4-PlantUML, Mermaid `c4Context`, hand-drawn Excalidraw
  exported to SVG, etc.).
- The **colour convention** for user boxes, your-system
  box, container boxes, and external-system boxes.
- The **line convention** for synchronous vs. asynchronous,
  read vs. write, and internal vs. external interactions.
- The **references** each diagram points at — specifically,
  which ADRs from exercise 02 authorise the shape of the
  Container diagram.

### Then — the meta-question

After the three diagrams and the legend, write a short
(200-400 word) answer to the following:

- Pick two of the three audience roles from chapter 03 —
  investor, technical advisor, new engineering hire,
  engineer implementing a change. For each, name which
  diagram they would look at first, one specific question
  the diagram would let them answer, and one specific
  question the diagram would **not** let them answer (so
  that you know when to send them to the next level).
- What did drawing the Container diagram surface about
  your architecture that you had not written down
  anywhere before? If nothing, either your existing
  architecture documentation is already excellent (rare),
  or the diagram is drawn at too high a level to be
  useful (much more common).

## Starter guidance

- Choose the diagramming format before you start. Do not
  spend the exercise's calendar comparing tools. Any of
  Structurizr ([structurizr.com](https://structurizr.com/)),
  C4-PlantUML
  ([github.com/plantuml-stdlib/C4-PlantUML](https://github.com/plantuml-stdlib/C4-PlantUML)),
  or Mermaid's `c4Context`
  ([mermaid.js.org — C4 diagrams](https://mermaid.js.org/syntax/c4.html))
  is fine.
- The System Context diagram is the diagram *most* likely
  to be reviewed by someone who has never opened your repo.
  Write the box labels like you were labelling for
  someone who has never used your product.
- If your Container diagram has more than about 10 boxes at
  seed stage, it is almost certainly wrong — you are
  either drawing implementation detail that belongs at
  Level 3, or you actually have a premature-microservices
  problem the diagram just made visible. Either fix the
  diagram or open an ADR on the extraction.
- Give the Component diagram a *specific* container to zoom
  into. "The backend" is not specific if you have two
  backend containers.
- Reference at least one ADR from exercise 02 in the
  legend, so that a reader following the "why is it this
  shape?" question is pointed at the answer.
- Keep every diagram inside one screen. If a diagram does
  not fit on one screen, it is trying to show more than
  its level allows; split it or move detail down a level.

## Acceptance criteria

Your diagram set is complete when a reader can:

- Open the System Context diagram and answer "what does
  this company do, who uses it, and what does it depend
  on?" in under a minute, without asking a follow-up.
- Open the Container diagram and identify every runnable
  process, every persistence store, every message-bus
  substrate, and the technology choice for each.
- Open the Component diagram and see the module boundaries
  the codebase actually respects (per exercise 01) — with
  fitness-function-worthy cross-module interfaces called
  out.
- Read the legend and reproduce your notation on a
  neighbouring diagram without asking.
- Trace at least one shape decision (the number of
  containers, the choice of persistence store, the
  monolith-vs-services call) back to the ADR from
  exercise 02 that authorises it.

The output of this exercise, together with exercise 02 and
exercise 04, forms the *architecture package* the paired
[lab-01](../README.md#lab) is scaffolded from once the lab
prompt is authored.
