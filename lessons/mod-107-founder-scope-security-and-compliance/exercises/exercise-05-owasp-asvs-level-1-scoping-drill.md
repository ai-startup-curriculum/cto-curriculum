# Exercise 05 — OWASP ASVS Level 1 Scoping Drill

**Module:** `mod-107-founder-scope-security-and-compliance`
**Planned time:** ~2 hours
**Chapter this builds on:** [`06-owasp-asvs-as-appsec-catalog.md`](../06-owasp-asvs-as-appsec-catalog.md),
supported by [`07-slsa-and-build-provenance.md`](../07-slsa-and-build-provenance.md)
for the SCA / secrets / SBOM tooling stack the L1
verification methods lean on.

## Problem statement

Score your current application against the **OWASP
Application Security Verification Standard Level 1**
requirements and produce the **L1 gap register** the
CTO owns at founder scope. Then draft the **L2 gap
register** that becomes the enterprise-ready roadmap
the first security hire drives to closure.

The point of the drill is not to *fix every gap*
(that is sprint work over the next quarter). The
point is to force yourself to walk the L1 catalog
requirement by requirement, mark each Pass / Fail /
N/A with concrete evidence, and produce the
register you can hand to a design partner's
security team and to the first security hire.

Use the current stable ASVS release available at
the time you run the drill — verify at
[github.com/OWASP/ASVS/releases](https://github.com/OWASP/ASVS/releases).
The chapter is written against v4.x; if v5.x is
current, use v5.x's chapter numbering and
requirement IDs.

## Requirements

Author the artifacts under
`docs/security/` (or the equivalent in your working
repo).

### Artifact 1 — Scope memo (`asvs-scope.md`)

A one-page memo naming:

- The **ASVS version** you scored against (with a
  citation to the release page).
- The **application(s) in scope** — one or more
  services, with a one-sentence description of the
  trust boundary each service sits behind.
- The **level target** — L1 as the founder-scope
  baseline, L2 as the enterprise-ready target.
  Confirm L3 is out of scope with the *"if a
  customer demands L3, that is a hiring signal,
  not a founder-scope work item"* framing from
  chapter 06.
- The **verification-method map** — for each L1
  chapter, which tool or method will attest each
  Pass (SAST tool, SCA tool, secrets scanner,
  container scanner, DAST tool, manual review,
  penetration test).
- **Out-of-scope categories** — any V-chapter
  that is entirely N/A for the application (e.g.,
  V12 Files and Resources if the application
  accepts no uploads); each with a one-line
  justification.

### Artifact 2 — L1 gap register (`asvs-l1-gap-register.md` or `.xlsx`)

A row-per-requirement table covering every ASVS L1
requirement in scope. Columns per chapter 06:

- **ID** — the ASVS requirement identifier (e.g.,
  `V2.1.1`).
- **Level** — 1 (or 2 if authored in the L2
  register below).
- **Chapter** — the ASVS chapter name.
- **Requirement** — the requirement text (verbatim
  from ASVS).
- **Status** — Pass / Fail / N/A / In Progress.
- **Evidence or justification** — for Pass, a
  citation (log query, code file / line, control
  reference); for Fail, a description of the gap
  and the risk in one sentence; for N/A, the
  one-line justification; for In Progress, the
  current state and the plan.
- **Verification method** — self-attestation /
  code review / SAST / DAST / SCA / secrets
  scanner / container scan / unit test / manual
  walkthrough / penetration test.
- **Owner** — the engineer (or the CTO)
  accountable.
- **Target close date** — for Fail / In Progress.

For the drill target, cover **every applicable L1
requirement** in the ASVS release you scored
against. If the release has ~130 L1 requirements,
your register should have ~130 rows (minus the
N/A rows you justified in the scope memo). The
discipline is the walk, not the length.

### Artifact 3 — L2 gap register (`asvs-l2-gap-register.md` or `.xlsx`)

The same format as Artifact 2, but scoped to the
**delta** between L1-Pass and L2 — i.e., the L2
requirements that are *not* already L1
requirements. This is the enterprise-ready roadmap.

For each L2 requirement:

- If it is currently Pass in the codebase, mark
  it Pass with evidence. Some L2 requirements will
  already be satisfied because the team happens
  to have done the right thing.
- If it is a Gap, describe the gap and estimate
  the engineering scope (single sprint / multiple
  sprints / quarter).
- If it is N/A for the application, mark it N/A
  with a one-line justification (SAML if no SAML,
  file-upload requirements if no upload, etc.).

The L2 register is the artifact you hand to the
first security hire and the artifact you cite when
an enterprise customer's security team asks *"do
you meet ASVS L2?"*.

### Artifact 4 — Verification-tooling manifest (`security-tooling.md`)

A one-page manifest naming, per verification method:

- **The tool** (CodeQL / Semgrep / Trivy /
  osv-scanner / Dependabot / Snyk / Gitleaks /
  TruffleHog / ZAP / commercial DAST / penetration-
  test vendor).
- **Where it runs** (pre-commit hook, CI pipeline
  step, scheduled workflow, external service).
- **What it blocks** (which severity level fails
  a PR; which findings ticket-out instead).
- **Where the findings live** (GitHub Security
  tab, tool's own dashboard, ticket system).
- **The triage cadence** (who reviews findings on
  what interval; what the SLA is per severity).
- **The gap-close plan** if a category is not yet
  tooled (e.g., no DAST yet, planned for
  Q[N]).

### Artifact 5 — `SECURITY.md` and `security.txt` (`SECURITY.md` at repo root; `public/.well-known/security.txt` or platform equivalent)

The coordinated-disclosure surface from chapter 06:

- **`SECURITY.md`** at the root of the primary
  source repository. Contents per
  [docs.github.com — Adding a security policy](https://docs.github.com/en/code-security/getting-started/adding-a-security-policy-to-your-repository):
  security contact (e.g., `security@yourcompany.com`),
  preferred language, acknowledged-within-N-days
  window, in-scope / out-of-scope categories,
  reward / recognition policy (or explicit
  statement that no reward is offered — this is
  fine at founder scope).
- **`/.well-known/security.txt`** at the root of
  the production website, formatted per RFC 9116
  ([securitytxt.org](https://securitytxt.org/)).
  Include `Contact`, `Expires`, `Preferred-
  Languages`, and `Canonical` fields.

### Cover memo (`README.md` in `docs/security/`)

A one-page cover memo linking to the four artifacts
above plus the `SECURITY.md` and `security.txt`,
naming the ASVS version scored, the L1 Pass /
Fail / N/A tallies, the top-three L1 Fails by risk,
and the plan for the next quarter.

## Starter guidance

- **Start with the scope memo.** Naming what is
  in scope and what is out of scope before
  scoring saves half the walk. If the application
  accepts no uploads, V12 Files and Resources is
  entirely N/A and does not need row-by-row
  scoring — mark it out in the scope memo and
  skip it in the register.
- **Score in one focused block.** ASVS L1 for a
  founder-scope codebase is 2–3 focused days.
  Splitting the scoring across multiple weeks is
  where the register loses coherence — you
  forget the context of decisions made in
  earlier sittings.
- **Score honestly.** A register that reports 95%
  Pass on day one is either dishonest or the
  scope is too narrow. Chapter 06 predicts 60-80%
  Pass on first score; that is the healthy
  range. Fails are the point of the drill.
- **Every Pass needs evidence.** *"We do input
  validation"* is not evidence. *"Every request
  handler in `src/api/handlers.py` uses
  `validate_request()` which enforces the JSON
  schema at `src/schemas/`; verified via unit
  test `tests/test_validation.py::test_all_endpoints_validated`"*
  is evidence. If a Pass has no evidence, it is
  In Progress at best.
- **Every N/A needs a justification.** *"N/A"*
  by itself invites the reviewer to assume you
  did not read the requirement. *"N/A — the
  application accepts no file uploads; verified
  by absence of any multipart/form-data
  endpoint"* invites the reviewer to trust the
  next N/A too.
- **The V2 / V3 / V4 chapters usually produce
  the most Fails at founder scope.** Password
  policy without breach-list check (V2),
  session-timeout not enforced server-side (V3),
  authorisation checked on some routes but not
  others (V4). Budget your walk time toward
  those chapters.
- **The V6 / V7 chapters usually produce the
  most surprises.** Deprecated algorithms in
  places nobody remembers writing (V6), stack
  traces returned to the user in a specific
  error path (V7). Grep is your friend for
  these categories.
- **Use the OWASP ASVS spreadsheet template.**
  The project publishes CSV and XLSX
  representations of every release at
  [github.com/OWASP/ASVS](https://github.com/OWASP/ASVS)
  under the release assets. Load that into
  Google Sheets / Excel and score inline;
  export or link from the register.
- **The L2 gap register is aspirational, not
  urgent.** Do not turn the L1 → L2 gap into
  sprint commitments in the same quarter as the
  L1-Fail close-out. L2 is what the first
  security hire drives once L1 is Pass.
- **The `SECURITY.md` is 10 minutes of work
  and worth days.** External researchers who
  find a bug will look for `SECURITY.md`
  first; if there is none they may disclose
  publicly rather than to you. This is the
  founder-scope substitute for a bug-bounty
  programme.

## Acceptance criteria

Your drill output is complete when:

- The scope memo names the ASVS version, the
  applications in scope, the L1 baseline / L2
  target / L3 out-of-scope framing, the
  verification-method map, and the out-of-scope
  categories with justifications.
- The L1 gap register scores every applicable L1
  requirement Pass / Fail / N/A / In Progress
  with evidence per Pass, gap description per
  Fail, justification per N/A, plan per In
  Progress.
- The L2 gap register covers the delta between
  L1 and L2 with the same format, scoped as the
  enterprise-ready roadmap.
- The verification-tooling manifest names one
  tool per method (SAST / SCA / secrets /
  container / DAST) with runtime location,
  blocking level, findings destination, and
  triage cadence.
- `SECURITY.md` exists at the repo root; a
  `security.txt` exists at
  `/.well-known/security.txt` in the production
  site (or the platform equivalent).
- The cover memo names the ASVS version, the L1
  tally, the top-three Fails, and the next-quarter
  plan.
- A technical reviewer who does not know your
  application can read the L1 register in 15
  minutes and name the top-three gaps and the
  plan to close each.
- Every Pass has evidence; every N/A has a
  justification; every Fail has an owner and a
  target close date.

## What this feeds into

- **Exercise 01 (posture memo) — Section 3**
  takes the *"OWASP ASVS at Level 1 with a gap
  register for the [N] items we have not yet
  closed"* clause from this register.
- **Exercise 02 (SOC 2 readiness) — CC7 and
  CC8** — several ASVS controls (input
  validation, secure configuration, logging)
  are evidence artifacts for the corresponding
  SOC 2 criteria.
- **Exercise 06 (SLSA baseline)** — the CI
  hardening checklist overlaps with several
  ASVS L1 verification methods (SAST, SCA,
  secrets scanning). Cross-reference between
  the two registers.
- **The module lab** consolidates the ASVS
  register with the other exercise outputs
  into a single `docs/compliance/` sub-tree.
- **Capstone
  [`project-102`](../../../projects/project-102-soc-2-type-i-readiness-and-founder-scope-compliance-package)** —
  the ASVS L1 register is the AppSec
  deliverable of the project.

The drill's discipline is the *walk*. A CTO who
can point at every L1 requirement and say Pass /
Fail / N/A with evidence has closed a category of
procurement risk that no amount of *"we take
security seriously"* language ever closes.
