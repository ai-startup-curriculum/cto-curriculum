# ISO/IEC 25010 Quality-Attribute Trade-offs

> ISO/IEC 25010:2023 defines the product-quality model used
> when the term "software quality" appears in a specification
> or an ADR — a small set of *characteristics* and their
> *sub-characteristics* that describe the non-functional
> properties of a software product.
> ([ISO/IEC 25010:2023 — SQuaRE Software Quality Model](https://www.iso.org/standard/78176.html))

## Motivation

Every load-bearing architectural decision is a trade-off
between non-functional properties — "we chose managed
Postgres over a self-hosted distributed store because
maintainability and operability matter more to us at this
stage than raw write throughput." That sentence is only
defensible if the reader and the author share a vocabulary
for "maintainability" and "operability" that is more
disciplined than gut feel.

The CTO who reasons about non-functional properties by
default — "we need it to be fast and reliable and secure"
— ends up with an ADR that says nothing, because *fast*
and *reliable* and *secure* are competing properties whose
trade-off has not been named. The ADR is only useful when
the trade-off is explicit: which properties the design
optimises for, which properties it deliberately trades
away, and why *that* trade is the right one for the stage.

**ISO/IEC 25010** is the international-standard vocabulary
for that conversation. It is not the only vocabulary — the
SEI Attribute-Driven Design method
([sei.cmu.edu — ADD](https://insights.sei.cmu.edu/documents/1611/2006_005_001_14636.pdf))
uses a similar taxonomy, and Nick Rozanski and Eoin
Woods's *Software Systems Architecture* uses a slightly
different one — but ISO/IEC 25010 has the useful property
of being the vocabulary due-diligence reviewers, RFP
authors, and enterprise buyers already recognise. Adopting
it is cheaper than negotiating a bespoke vocabulary every
time the CTO writes an ADR.

## The eight characteristics of ISO/IEC 25010:2023

The 2023 revision of ISO/IEC 25010 defines eight
top-level product-quality characteristics
([iso.org/standard/78176](https://www.iso.org/standard/78176.html)).
Each has sub-characteristics; the top-level names are the
ones that appear in most ADRs. The list below names each
characteristic and gives one seed-stage example of the
trade-off it usually forces.

- **Functional Suitability** — does the software do what
  the user asked for? Sub-characteristics include
  *functional completeness*, *functional correctness*,
  *functional appropriateness*. Trade-off at seed: shipping
  the 80%-complete feature next week vs. the 100% feature
  next quarter.
- **Performance Efficiency** — does it meet its
  time-behaviour, resource-utilisation, and capacity
  targets? Trade-off at seed: sub-second p95 API latency
  for the free tier vs. one server per tenant for the
  first three enterprise design partners.
- **Compatibility** — does it co-exist and inter-operate?
  Sub-characteristics: *co-existence*, *interoperability*.
  Trade-off at seed: which webhooks / API standards the
  product speaks to fit the buyer's existing stack.
- **Interaction Capability** (formerly *Usability* — the
  2023 revision renamed and expanded this characteristic)
  — how well the product supports the user's interaction
  with it. Trade-off at seed: the internal-admin console
  the CTO built in an afternoon vs. the polished
  self-service onboarding the first enterprise buyer
  expects.
- **Reliability** — does it maintain its performance under
  stated conditions, over stated time? Sub-characteristics
  include *maturity*, *availability*, *fault tolerance*,
  *recoverability*. Trade-off at seed: 99.5% single-region
  uptime vs. multi-region active-active (which almost
  always defers up to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning) —
  see chapter 06).
- **Security** — does it protect information and data?
  Sub-characteristics include *confidentiality*,
  *integrity*, *non-repudiation*, *accountability*,
  *authenticity*. Trade-off at seed: SOC 2 Type I on the
  90-day path vs. the ISO/IEC 27001 posture the first
  regulated buyer will ask for. See mod-107 for the
  founder-scope security playbook.
- **Maintainability** — how easy is it to modify safely?
  Sub-characteristics include *modularity*, *reusability*,
  *analysability*, *modifiability*, *testability*. This
  is the ISO/IEC 25010 name for the chapter-01 *cheap to
  change* invariant, and it is usually the top-ranked
  characteristic at seed.
- **Portability** — how easily can the software be moved
  from one environment to another? Sub-characteristics
  include *adaptability*, *installability*,
  *replaceability*. Trade-off at seed: build against a
  cloud-agnostic subset vs. take the productivity win of
  the cloud's managed services and accept some lock-in.
  See mod-103 on the build-vs-buy side of this.

A ninth characteristic — **Flexibility** — was added in
the 2023 revision to cover *adaptability*, *scalability*,
*installability*, and *replaceability*, with some overlap
against portability; see the ISO/IEC 25010:2023 page for
the exact revision-2023 taxonomy. The vocabulary above is
enough for the pre-seed / seed CTO; a more granular
sub-characteristic map is available at
[iso25000.com](https://iso25000.com/index.php/en/iso-25000-standards/iso-25010)
for reference.

## Ranking, not maximising

The trap ISO/IEC 25010 exists to prevent is treating every
characteristic as equally important. You cannot maximise
all eight at once at seed stage; each pair of them has a
trade-off that the design has to resolve in one direction
or the other.

- **Performance Efficiency vs. Maintainability** — a
  hand-tuned SQL query with three levels of indexing runs
  faster than the ORM equivalent and is harder to change
  when the schema evolves.
- **Reliability vs. Maintainability** — a multi-region
  active-active deploy is more reliable than a
  single-region deploy and is much harder to change.
- **Security vs. Interaction Capability** — mandatory MFA
  on every action is more secure than session-scoped auth
  and is a worse user experience.
- **Portability vs. Performance Efficiency** — a
  cloud-agnostic subset of managed services is more
  portable than the cloud's proprietary managed services
  and is slower and more expensive to run.
- **Functional Suitability vs. Reliability** — shipping the
  feature next week meets the customer commitment and
  introduces reliability risk that a more careful two-week
  ship would have caught.

The CTO's job in the ADR (chapter 02) is to *name the
trade* the design makes and defend it against the stage.
"We rank Maintainability > Performance Efficiency at this
stage; when we hit N RPS we will re-open ADR-000X" is a
defensible position. "It's fast and maintainable" is not,
because it means the trade has not been resolved.

## Ranking template — pre-seed / seed default

For most pre-seed / seed startups, the ranking is roughly:

1. **Maintainability** — cheap to change is the load-bearing
   invariant (chapter 01).
2. **Functional Suitability** — the feature is what makes
   the customer keep calling.
3. **Security** — the founder-scope baseline (mod-107) is
   non-negotiable; enterprise buyers will not sign without
   at least the SOC 2 Type I posture.
4. **Reliability** — reliable enough that customers do not
   fire you and design partners do not lose confidence,
   but not four-nines and not multi-region.
5. **Interaction Capability** — polished enough that the
   first buyer takes the product seriously, but not
   pixel-perfect.
6. **Performance Efficiency** — meets the p95 latency the
   product needs, no more. Do not premature-optimise.
7. **Compatibility** — inter-op only where the buyer's
   stack forces it.
8. **Portability** — take the lock-in in exchange for the
   managed-service productivity gain. Revisit only when a
   specific customer requirement or a specific vendor risk
   forces re-examination.

This ranking is not universal. A B2B startup selling into
banks will rank Security higher and Functional Suitability
lower. A consumer-mobile startup will rank Interaction
Capability higher. A startup selling on-premise / air-gapped
deployments will rank Portability much higher. What matters
is that the ranking is **explicit, written down, and
defended against the current stage** — not implicit.

## Documenting the trade-off in the ADR

Every ADR's *Consequences* section (chapter 02) is where
the ISO/IEC 25010 characteristics get named. A well-formed
Consequences section looks like:

```
## Consequences

**Positive**
- Maintainability: the modular monolith keeps the domain
  seams intact, so a pricing-model pivot is a one-module
  change.
- Reliability: managed Postgres with point-in-time recovery
  gives us recoverability without operating our own
  replication.

**Negative**
- Performance Efficiency: writes are bounded by a single
  primary. We estimate this ceiling as ~10× current
  traffic; when we approach it we open a supersession ADR.
- Portability: we are choosing AWS RDS specifically; a move
  off AWS would require re-provisioning and a cutover. We
  accept this in exchange for not operating our own
  Postgres.

**Deferred**
- Security: the auth path is deferred to ADR-0004 (Clerk).
- Compatibility: no external inter-op required in this
  release; revisit at Q3.
```

The `Deferred` bucket is a Nygard-style pointer to the
adjacent ADRs where the linked characteristic is resolved.
This is what turns the ADR index from a flat list into a
graph the reader can traverse.

## The two characteristics you are actively trading away

The most disciplined framing is the one used in the exercise
for this chapter. It asks the CTO to identify the **two**
characteristics they are actively trading away this quarter
— not "not maximising", but *deliberately spending down*.

This forces the conversation to be honest. It is easy to
say "we care about all eight characteristics"; it is much
harder to say "we are actively trading Portability and
Performance Efficiency down this quarter in exchange for
Maintainability and Functional Suitability, and here is
what would cause us to re-open the trade".

The two-you-trade-away framing has two useful properties:

- **It reveals the ADR's real shape.** When the whole team
  agrees on which two characteristics are being spent
  down, downstream disagreements about specific choices
  become much easier to resolve — they are usually a
  disagreement about the trade, not about the choice.
- **It surfaces stage-transition triggers.** The
  characteristic you are trading down this quarter is the
  one that will bite you when it matters — usually at the
  next stage transition. Writing it down makes the eventual
  re-opening cheaper because the "when" is already named.

## Where ISO/IEC 25010 stops and higher-level standards
begin

ISO/IEC 25010 is the product-quality model. Adjacent
standards in the SQuaRE family (ISO/IEC 25000-series) cover
data-quality (25012), quality-in-use (25010's usage-scope
sub-model), and measurement (25022 / 25023). At pre-seed /
seed you consume 25010 and defer the rest until (a) a
regulated buyer or (b) a formal-assurance need forces the
expansion.

Above ISO/IEC 25010, deep multi-region / multi-tenant /
high-scale reliability, performance, and security
engineering defers up to
[`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
(level 45) and
[`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning)
(level 55). This module's job is to make sure the trade-off
vocabulary is available so that the deferral is a
*deliberate* choice with a named trigger, not a "we'll deal
with it when it breaks" default.

## Common failure modes

- **The everything-matters ADR.** The Consequences section
  lists positive impact on eight characteristics and no
  negative impact on any. Fix: this means the ADR has not
  resolved the trade. Force yourself to name at least one
  characteristic the choice trades *down*.
- **The characteristic-name-only trade.** "We are trading
  reliability" — but reliability against what, and how much?
  Sub-characteristics matter here; "availability against
  maintainability" is a real trade, "reliability against
  performance" is often just imprecise thinking.
- **The permanent-trade fallacy.** The ranking is written
  down once and never revisited. It is fine to write
  "current-stage ranking" at the top of the ranking and
  re-open it at each stage transition — the
  wrong-rung-for-the-stage pathology from mod-101 applies
  here too.
- **The custom-vocabulary reinvention.** The team invents
  its own quality-attribute vocabulary rather than using
  ISO/IEC 25010, then has to re-explain it every time a
  new hire, a technical advisor, or a due-diligence
  reviewer joins the conversation. Fix: adopt the ISO
  vocabulary; the muscle it gives you is worth the
  half-day of vocabulary alignment.

## Summary

- ISO/IEC 25010 defines the vocabulary for the
  non-functional trade-offs every ADR is implicitly making.
  The 2023 revision has eight top-level characteristics:
  Functional Suitability, Performance Efficiency,
  Compatibility, Interaction Capability, Reliability,
  Security, Maintainability, Portability (plus Flexibility
  as a ninth in the 2023 revision).
- You do not maximise all of them; you **rank** them for
  the current stage and defend the ranking.
- Every ADR's Consequences section names which
  characteristics the choice improves and which it trades
  down — the honest ADR always trades at least one
  characteristic down.
- The most disciplined framing is: **which two
  characteristics are you actively trading away this
  quarter, and what would trigger you to re-open the
  trade?**
- Deep multi-region / multi-tenant / high-scale non-
  functional engineering defers up to
  [`ai-infra-senior-architect`](../../../ai-infra-senior-architect-learning)
  and
  [`ai-infra-principal-architect`](../../../ai-infra-principal-architect-learning).

The chapter's paired exercise —
[`exercise-04-iso-25010-quality-attribute-trade-off-map.md`](exercises/exercise-04-iso-25010-quality-attribute-trade-off-map.md)
— walks the ranking of the ISO/IEC 25010 characteristics
for your (or a real reference) startup and identifies the
two you are actively trading away.
