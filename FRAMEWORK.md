# The Governed Pull Request Framework
**Version:** v0.3
**Date:** 2026-08-06
**Author:** J. Wright · UX Minds, LLC
**Status:** Parent framework. Deployments in specific team or organizational contexts are governed derivatives (see §8) and must not modify this document directly.

**Reading path:** First-time contributors should read `QUICKSTART.md` (90 seconds) — it is sufficient to submit a correct PR. This document is for reviewers, adopters, and maintainers. Design rationale and term origins live in `LINEAGE.md` (optional context, never required reading).

---

## Changelog

- **v0.3 (2026-08-06)** — Nine amendments from Counter-Pass adversarial testing of v0.2. (1) §2.3 pre-cleared classes: class declarations now require a machine-checkable boundary predicate (A2), are treated as Time-sensitive claims with a mandatory expiry/review interval and a new-transitive-package mechanical exit trigger (A3), and §9 gains an explicit provenance limit (A4). (2) §10 Measurement: two new signals added — unattributed incident rate (funnel-boundary instrumentation) and emergency-path rate (A5); §10 now declares its topology-stability validity condition (A6). (3) New §10.1 Emergency Change Path: governed act-first bypass with mandatory retrospective Critical-tier PR (A7); §9 gains explicit perimeter limit (A8). (4) §6.1 AI-reviewer stance rewritten from categorical to configurational: K2 is a property of the review configuration, not the reviewer's substrate; diff-consuming tools fail it by construction; the §3/§6.1 incoherence dissolved (A9). (5) LINEAGE.md: Differentiator 1 reframed as compositional; precedent survey added (A1). No changes to K1–K4, the tag set, the two-switch architecture, or the tier definitions.

- **v0.2 (2026-08-06)** — Three additions from a comparative analysis against industry practice and ITIL change management: §10 Measurement (four outcome metrics as the partial detector for Known Limit #2; Change Control renumbered to §11), §6.1 AI-reviewer stance (AI tools extend the mechanized layer; they do not satisfy K2), §2.3 pre-cleared change classes (class-level Critical review at declaration; instances proceed on green automated gates). ITIL convergence citation added to `LINEAGE.md`, framed as independent reconvergence. Matching one-line pointers added to `QUICKSTART.md` and the PR template. No changes to K1–K4, the tag set, or the two-switch architecture.
- **v0.1.1 (2026-08-06)** — Legibility pass; no structural changes. Tier names replaced with plain language (Low-risk / Feature / Critical; T1–T3 codes retained). "Epistemic Summary" renamed "Verification Status." Operating Scale declaration moved from per-PR template to per-repository configuration (§3.0). Worked examples added to the template. `QUICKSTART.md` and `LINEAGE.md` introduced as companion files. Internal shorthand ("killer items," "Retro Rule," "membrane rule") retained in this document with plain-language definitions at first use; removed from contributor-facing files. Surfaced by an external-legibility review.
- **v0.1 (2026-08-06)** — Initial release.

---

## §0 — Purpose and Design Constraints

A pull request is three things at once: a change to a codebase, a request for judgment, and a permanent evidence artifact. Most PR processes serve the first, under-serve the second, and ignore the third.

This framework refines PR practice through three lenses — **Clarity** (the reviewer reads intent off the description, not out of the diff), **Consistency** (the bar does not move with deadline pressure, author, or reviewer), and **Credibility** (every claim in a PR is either verified, or honestly tagged as not yet verified) — and enforces them through two switches:

1. **Change Tier** — how far the change propagates; declared per PR (§2)
2. **Operating Scale** — who is reviewing and under what conditions; declared per repository (§3)

The framework's own design constraints, applied to itself:

- **Killer items only** — i.e., a checklist item earns its place only if skipping it causes silent, propagating failure AND it is the kind of thing that gets skipped under pressure. Everything else is either automated or omitted.
- **Tooling holds what tooling can check.** Any condition a linter, type system, commit hook, or CI job can verify is removed from the human checklist and mechanized (§6). A checkbox a machine could have checked is a checkbox that will eventually be checked falsely.
- **Governance where decisions propagate silently if wrong — not everywhere.** Uniform heavyweight process is itself a credibility failure: it trains ritual completion. Depth scales with blast radius.
- **Progressive disclosure.** The contributor-facing surface (`QUICKSTART.md`, the PR template) must remain self-sufficient in plain language. No amendment may make the template depend on this document or on `LINEAGE.md` to be understood. If it does, the amendment is rejected as reintroducing the legibility failure this version removed.

---

## §1 — The Four Universal Requirements (every tier, every scale)

These apply to every PR without exception. They are the entire mandatory human checklist for the smallest changes. (Design shorthand: the "killer items," K1–K4.)

**K1 — Tier declared honestly.** The PR states its Change Tier (§2). The reviewer's *first* check is whether the declaration matches the diff. A Low-risk label on a Critical-sized diff is the primary evasion vector for this entire framework and is treated as a blocking finding, not a formality.

**K2 — Reviewed outside the authoring context.** No PR is approved by the same session, person, or context that produced the code. What satisfies this depends on Operating Scale (§3). Review inside the authoring context is proofreading, not review.

**K3 — Automated gates green, not attested.** All mechanized checks (§6) pass. No human checkbox exists for anything a machine verifies. If a mechanized check is being bypassed, the bypass itself is declared in the PR body with a reason.

**K4 — No Unverified claim on a protected surface.** Changes touching a protected surface (§5) cannot merge carrying an Unverified tag (§4) on any claim about that surface. There is no epistemic escape hatch for the classes of change where being wrong is unrecoverable or invisible.

---

## §2 — Switch 1: Change Tier (declared per PR)

Tier is determined by **propagation, not line count**. Line count is a signal, not the definition: empirical code-review research shows defect detection collapses past roughly 200–400 changed lines, so a nominally low-tier PR at high line count should be treated as mis-tiered until justified.

*(Origin note: the propagation-based tiering adapts the author's Tiered Content Framework, which governs content by blast radius — catch the problem at the smallest unit and everything built from it inherits the fix. See `LINEAGE.md`. The TCF tier vocabulary itself does not appear in contributor-facing files.)*

| Tier | Name | Definition | Examples | Required PR content |
|---|---|---|---|---|
| **T1** | **Low-risk** | A change whose failure is local and visible. Single field, constant, isolated function, copy, test-only change. Reversible by a later visible refactor. | Rename, constant fix, single-function bug fix with existing test coverage | K1–K4 + one-line intent. Nothing else. (Instances of a pre-cleared class: see §2.3.) |
| **T2** | **Feature** | A feature slice or logic change whose failure could propagate within a bounded area. New hook/component, behavior change in one module. | New feature behind a flag, module-scoped refactor, bug fix requiring new tests | T1 requirements + full T2 block (§2.1) |
| **T3** | **Critical** | A change touching a protected surface (§5), a cross-module contract, a data convention, a dependency, deploy configuration, or anything whose failure would be silent or unrecoverable. | Protocol/schema change, sync or storage semantics, permission/exposure logic, dependency bump, deletion of undocumented code | T2 requirements + full T3 block (§2.2) |

**Tier disputes resolve upward.** If author and reviewer disagree on tier, the higher tier applies. No negotiation.

### §2.1 — The T2 (Feature) block

1. **Intent + acceptance criteria.** What this changes and why, stated before the diff must be read; acceptance criteria in *given / when / then* form, written before the code was generated, with each criterion mapped to where it is met.
2. **Verification Status.** Every substantive claim in the description carries a tag from §4.
3. **Not in this PR.** One line, two slots: `Not in this PR: [what] — [safe to defer because]`. This single field replaces separate out-of-scope, deferral, and scope-discipline declarations.
4. **Pre-mortem.** One answered question: *"It is two weeks from now and this PR caused an incident — what was it?"* The answer is written, not gestured at. This is the single generative adversarial item; it exists to catch the failure modes no fixed list enumerates.

### §2.2 — The T3 (Critical) block (adds to T2)

5. **Convention check.** Link to the governing convention document for any data convention, key format, protocol semantic, or state schema this touches. If the convention does not yet exist, the PR's second deliverable is the convention document — the code is not accepted until the convention is written (see §7).
6. **Decision record.** If this PR settles a previously undecided question that would *propagate silently if wrong*, a lightweight decision record (context / decision / alternatives / consequences) is linked. Local implementation choices reversible by a visible later refactor need no record. This is the materiality threshold: ceremony attaches to silent propagation only.
7. **Boundary questions.** If a protected surface (§5) is touched, the description answers: does this change what any party can *see, forge, replay, or deny*? "No change" is an acceptable answer; an unanswered question is not.
8. **Deletion justification.** Code may not be removed until the PR states why it existed. Undocumented code nobody can explain is a convention gap to be logged (§7), not a license to delete.
9. **Verification chain.** For any bug fix: root cause stated (not just symptom disappearance), with the hypothesis-first diagnostic trail summarized. "Fixed the bug" is not a credibility-bearing statement.

### §2.3 — Pre-cleared change classes (Low-risk tier extension)

A repository may declare **named pre-cleared classes of change**: categories of Low-risk change reviewed and approved *once, as a class*, whose individual instances then proceed without per-PR ceremony beyond K3 — green automated gates. The instance's intent line is the class name; K1 is satisfied by the class membership itself; K2 is satisfied by inheritance from the class-level review.

Canonical example: *dependency version bumps of non-protected libraries with green CI.* The class review establishes, once, which libraries are outside every protected surface (§5) and what the CI suite verifies about a bump; each subsequent bump within that boundary merges on green checks alone.

Four governance conditions:

1. **The class declaration is a Critical-tier change.** Declaring, widening, or modifying a pre-cleared class alters the repository's governance configuration — itself a protected surface (§5). The declaration therefore takes a full T3 review, including the boundary questions; individual instances inherit that pre-approval. Review rigor is spent once, at the class level, where it buys down the cost of every instance.
2. **No class may include a protected surface.** A change class touching any §5 surface is not eligible for pre-clearance at any breadth. K4 has no class-level exemption.
3. **An instance that exits the class definition exits the class.** A dependency bump that requires a code change to accommodate, crosses a major version where the class specified minor/patch, or touches anything beyond the declared boundary is not an instance — it tiers normally, per K1.
4. **The class declaration ships a machine-checkable boundary predicate.** The T3 class review's second deliverable (§7) is a CI-enforceable predicate that verifies instance membership mechanically: which files may be touched (lockfile and manifest only?), which libraries are in scope (declared set only?), which semver band is permitted, and whether any code changes are present. Instance-boundary verification is a mandatory §6 gate — it is not enforced by reviewer memory. A class declaration with no predicate is incomplete and does not confer pre-clearance.

**Class declarations are Time-sensitive claims.** A class approved against an ecosystem state carries a mandatory expiry and review interval, declared at the time of approval. Additionally: any lockfile change that introduces a *new* package (as distinct from a version update of an existing one) automatically exits the instance from the class and files a §7 convention-gap finding against the class definition — the class boundary must be revisited before the next instance proceeds. New-package detection is lockfile-diff-detectable and is part of the §6 predicate.

Class declarations live in `CONTRIBUTING.md` alongside the protected-surface list.

---

## §3 — Switch 2: Operating Scale (declared per repository)

### §3.0 — Where scale is declared

Operating Scale is a property of the repository, not of the PR. It is declared once — in `CONTRIBUTING.md` or the repository's governance config — and revisited when the contributor set changes. **It does not appear as a fillable field in the PR template.** The template ships with scale-gated sections marked; the repository's adoption step activates or removes them. Contributors never answer a question whose answer is fixed.

Scale gates *which review mechanisms are active* and *what satisfies K2*.

### S1 — Solo + AI assistant

- **K2 satisfied by:** a review pass in a *separate session/context* from the one that produced the code, conducted against the written spec and acceptance criteria — plus, for anything network-facing, verification with at least one party outside the local environment before the phase closes.
- **Honest limit, stated rather than hidden:** a fresh session is independent in context but not in kind. For Critical changes on protected surfaces, the compensating mechanism is *external verification* — checking the design claim against the upstream ecosystem, maintainer, or community of the dependency in question. At S1, the ecosystem is the second reviewer of record for boundary-layer claims.
- **Inactive at this scale:** reviewer-scope lines, block-right protections, fidelity-source field.

### S2 — Small trusted team (roughly 2–6 people, shared context)

- **K2 satisfied by:** a second human. The AI fresh-session review demotes to a **pre-review pass** the author runs before requesting human review — mechanical findings are cleared cheaply so scarce human attention goes to judgment.
- **Verification tags become transmission.** Tags are no longer self-discipline; they tell the reviewer which claims they are inheriting versus which they must independently check. A reviewer approving a PR is presumed to have accepted its *Confirmed* tags and independently evaluated everything else — unless their scope line says otherwise.
- **Block right is live.** Any team member may block any PR. At this scale it functions socially; it is named here so it survives the transition to S3.

### S3 — Organization (mixed seniority, rotating staffing, multiple disciplines, client or stakeholder deliverables)

Everything in S2, plus:

- **Reviewer-scope lines, mandatory on Feature-tier and above.** An approval states what it covers and what it does not: `Approved: [claim classes evaluated]. Not evaluated: [claim classes outside reviewer's domain].` An unscoped approval on a cross-domain change is the false-consensus failure mode — one reviewer's partial confidence laundered into total sign-off. Scoped approval is the review-side twin of the author-side verification tags.
- **Calibration awareness, lightweight.** Approvals are not uniform evidence: the same reviewer approving changes inside and outside their domain are different-strength signals. This framework does not mandate a scoring system; it mandates that scope lines make the difference *visible*, so that trust is conditioned by claim type rather than granted globally.
- **Fidelity source, mandatory where applicable.** Any PR implementing a design artifact, external specification, or stakeholder requirement links the source and states where deviation was *negotiated* versus where it must be checked for *drift*. Implementation drift from design intent with no artifact catching it is the characteristic S3 failure.
- **Block right, protected.** A block from any contributor — regardless of seniority — is procedurally identical to a block from the lead: overriding it requires the same written justification, visible in the PR. A block right that is career-risky to exercise does not exist.
- **Convention documents are onboarding-load-bearing.** §7 is enforced strictly: at this scale, an undocumented convention is re-discovered by every new team member, and the person who knew the answer may no longer be present.

### S4 — Public (external contributors, open source, published evidence)

Everything in S3, plus:

- **Maintainer model.** K2 is satisfied by maintainer review; `QUICKSTART.md` and the template are the complete contributor-facing requirement — nothing relies on contributors having read anything else.
- **Full mechanization.** Every §6 gate is CI-enforced with no manual fallback, because shared memory cannot be assumed.
- **The PR history is evidence.** At this scale, the merged-PR record is a public evidentiary artifact: tier declarations, verification tags, and scoped approvals are part of the project's demonstrable governance, auditable by parties who were never in the room. Write descriptions for that reader.

---

## §4 — Verification Status Tags

Every substantive claim in a Feature-tier or Critical-tier PR description carries exactly one tag:

| Tag | Meaning | Requirement |
|---|---|---|
| **Confirmed** | Verified by attached evidence | Must state *what it was confirmed against* — test run link, dependency version, environment — and the date. A Confirmed tag with no referent is Inferred. |
| **Inferred** | Follows from confirmed observations with stated reasoning | The reasoning is in the description, not implied. |
| **Unverified** | Assumed, not yet checked | **Only admissible with an attached closure plan:** what will be observed post-merge, by when, to confirm or kill the assumption. An Unverified tag with no closure plan is a blocked merge, not a disclosure. Inadmissible entirely on protected surfaces (K4). |
| **Time-sensitive** | True now, known to have an expiry condition | The expiry condition is named. |

**Decay rule.** Tags date-stamp against a dependency and environment state. A rebase across a dependency bump *invalidates* Confirmed status on every claim the bump could affect; those claims re-verify or re-tag before merge. Evidence rots silently unless the rot condition is declared.

**Staleness rule.** An open PR is a decaying evidence artifact. A PR open beyond the repository's declared staleness window (default: 14 days) requires re-verification of its Confirmed tags, not merely a rebase.

---

## §5 — Protected Surfaces

Each repository deploying this framework declares its protected surfaces at adoption — the classes of change where failure is silent, unrecoverable, or trust-breaking. Common classes:

- Data conventions: schemas, key formats, serialization, migration logic
- Sync, replication, or conflict-resolution semantics
- Permission, exposure, identity, or audit logic — anything defining what a party can see, prove, or deny
- Payment, deletion, or other irreversible user-facing operations
- Dependency versions of any library implementing the above
- Deploy and environment configuration

Changes to protected surfaces are automatically Critical tier regardless of size, and K4 applies: no Unverified tags on the protected claim.

---

## §6 — The Mechanized Layer

The following are removed from human checklists and enforced by tooling. The list is the *minimum*; repositories extend it. The principle: these are validity conditions, not content — invisible in the final product, load-bearing everywhere downstream, and exactly the class of rule humans skip under pressure.

- Structured commit format (`fix:` / `feat:` / `refactor:` / `chore:` + scope) via commit hook — makes history parseable by changelog tooling, semantic versioning, and any future automated or human session reconstructing intent
- Lint, type checks, formatting
- Test suite green; coverage floor where declared
- Dependency classification check (production dependencies not in dev-dependency scope)
- Known-pattern conformance checks where grep-detectable (repository-specific: required observer patterns, forbidden APIs, required error-handling wrappers)
- Diff-size advisory: PRs exceeding the declared review-effectiveness threshold (default 400 changed lines) receive an automated comment requiring either a split or a written justification

Any rule currently enforced by reviewer memory is a candidate for this layer. A convention enforced manually in review is a convention that has not yet been operationalized — not evidence of reviewer diligence.

### §6.1 — Where AI reviewers sit

AI review tools — structured PR-summary bots, inline suggestion tools, automated review assistants — belong to this layer, not to K2. They extend the mechanized layer's coverage upward: pattern-level findings, likely-bug heuristics, convention conformance beyond what grep-detectable checks catch, summaries that reduce reviewer reading cost. That coverage is cheap and worth having, and repositories should treat these tools as §6 extensions, subject to the same rule as every other mechanized check: green, not attested.

**K2 is a property of the review configuration, not the reviewer's substrate.** K2 is satisfied by any reviewer — human or AI — whose model of the intended behavior was built independently of the authoring process. The question is not whether the reviewer is human; it is whether their understanding of what the change was *supposed to do* was formed outside the process that produced the code.

**Diff-consuming tools fail K2 by construction — not by capability.** A tool whose input is the diff and the authored codebase operates on the same representation the authoring context produced. No improvement in capability changes this: the tool never received an independent account of intent, so it cannot check the code against one. This is a topology constraint, not a capability ceiling, and it applies regardless of how sophisticated the tool becomes. Such tools belong in §6; they do not satisfy K2.

**Independent configurations are assessed under §3's scale provisions.** A review conducted by a distinct model, receiving only upstream intent artifacts (the ticket, spec, or acceptance criteria — not the diff-producing conversation), and independently deriving and executing verification against those artifacts, may satisfy K2's independence criterion. Whether a given configuration meets that bar is itself a K2-grade judgment, made at the class level (§2.3) or as part of repository governance, not at merge time.

This does not alter S1's separate-session provision (§3): that mechanism derives what independence it has from context separation and review against the written spec — and is already named the weakest form of K2 (§9), compensated by external verification rather than credited as equivalent to a second human. The division of labor across scales remains: tooling catches what is mechanical and pattern-shaped, cheaply and before human attention is spent; K2 is reserved for the judgment that requires independence from the authoring context.

---

## §7 — Self-Healing Conventions

*(Design shorthand: the "Retro Rule.")*

Any PR that surfaces a convention gap — a pattern not yet documented, a failure mode not yet on the adversarial-test list, a protected surface not yet declared, an environment quirk not yet recorded — owes a **second deliverable**: the update to the relevant governing document. The code change and the convention update ship together or the PR does not close.

Without this rule the same gap is re-discovered serially instead of inherited; with it, the framework's supporting documents stay true without a separate maintenance process. This is the only mechanism keeping §5 and §6 accurate over time, and it is therefore itself a universal-class requirement at Critical tier.

---

## §8 — Derivatives and Inheritance

This document is the **parent**. Any deployment inside a specific team, organization, or product context is a **governed derivative**, and the following inheritance rules apply:

**Must be preserved by every derivative:**
- The two-switch architecture (tier × scale) and the upward-resolution rule for tier disputes
- The four universal requirements (K1–K4)
- The verification tag set and its admissibility rules (§4), including the decay rule
- The mechanization principle (§6): tooling holds what tooling can check
- The self-healing conventions rule (§7)
- The progressive-disclosure constraint (§0): contributor-facing files remain self-sufficient

**May be adapted by derivatives:**
- Tier vocabulary and examples, mapped to the local domain
- The specific field lists within the T2 and T3 blocks
- Protected-surface declarations (§5) — these are *expected* to be local
- Scale-gate details (staleness windows, diff thresholds, review-turnaround norms)
- The mechanized-layer contents beyond the §6 minimum
- Emergency change window (§10.1) — default is 1 business day; declare your override in CONTRIBUTING.md

**Two-way contribution:** a derivative that discovers an amendment-worthy improvement proposes it upstream to the parent through the parent's change-control process; the parent versions the change; other derivatives inherit it on their next revision. Derivative-local fields (client requirements, internal tool names, org-specific surfaces) never flow upstream. The parent never carries context-specific content.

**Context-separation rule** *(design shorthand: the "membrane rule")***:** context-specific derivatives are not published, cited, or shared outside their context. The parent is the only public artifact. This applies to attribution and lineage as well as content: derivatives carry the parent's one-line attribution only; `LINEAGE.md` is a parent-only artifact and does not ship with derivatives.

---

## §9 — Known Limits (stated, not hidden)

1. **S1's K2 is the weakest link in the framework.** A separate-session review is independent in context, not in kind. The compensating controls (external verification for network-facing changes; ecosystem-as-reviewer for boundary claims) are real but partial. Anything this framework's S1 mode approves on a protected surface should be treated as provisionally verified until an S2+ or external review touches it.
2. **The framework cannot detect its own ritual completion.** Scoped approvals and verification tags can be pencil-whipped like anything else. The mitigations are structural (few items, tier-gating, mechanization) rather than absolute. The observable symptoms of decay are uniform tags, unscoped approvals, and the metric signatures defined in §10 — the measurement layer exists as the partial detector for this limit. A derivative seeing those patterns should treat them as a governance finding.
3. **Tier declaration is honest-declaration-dependent.** K1 makes mis-tiering the reviewer's first check, but a colluding author and reviewer defeat it. At S3+, the diff-size advisory (§6) is the only mechanical backstop.
4. **This is v0.3.** The v0.1 architecture has been stress-tested analytically at one scale and extended across four; the v0.1.1 legibility pass responds to an external-readability review; the v0.2 additions respond to a comparative analysis against industry practice; the v0.3 additions respond to adversarial testing of v0.2. The framework has not yet accumulated usage evidence at S2–S4 — the §10 measurement layer defines what that evidence will look like, but none has been collected. Amendments through the change-control process are expected, not exceptional.
5. **The framework's writ ends at the PR funnel.** Every guarantee in this framework attaches only to changes that enter the PR process. Changes made outside it — production hotfixes applied directly, console or infrastructure changes, manual migrations, flag flips under incident pressure — are ungoverned, unrecorded, and invisible to §10. The emergency change path (§10.1) is the governed bypass for deadline-pressure changes; without it, high-urgency changes exit the perimeter entirely. Neither the PR process nor §10 can detect a change that bypassed the funnel. Repositories wanting coverage of out-of-band changes need observability tooling outside this framework's writ.
6. **Neither the governed path nor pre-clearance verifies upstream provenance.** A full T3 human review of a dependency bump does not read the upstream diff; K3's green CI verifies the behavior the test suite covers, not where the code came from. Pre-clearance (§2.3) removes the residual human-anomaly-detection opportunity on top of that. Repositories wanting supply-chain provenance assurance need dedicated tooling (e.g., SLSA attestations, sigstore, lockfile integrity checks) outside this framework's writ.

---

## §10 — Measurement

The framework's Known Limits (§9) include an admission with a consequence: the framework cannot detect its own ritual completion (Limit #2). Metrics are the partial detector for that limit — not proof of health, but the observable trace that pencil-whipping leaves. A repository deploying this framework at S2 scale or above should instrument six outcome metrics:

**Validity condition:** these metrics detect drift *within a stable review topology* — one where substantive review decisions are being made inside the PR process. If the team has shifted to deciding things pre-PR (pairing sessions, pre-agreed designs, decisions settling before the PR opens), these metrics will report a healthy profile on a process that has become a formality. A topology shift of that kind is not gaming to be caught by these metrics; it is a governance finding to be declared under §7, because it changes what the PR evidence artifact records. Investigate topology before concluding the metrics are healthy.

| Metric | What it is | What it detects |
|---|---|---|
| **Review latency** | Time from review request to first substantive response, and to approval | **Ritual completion.** Approval turnaround implausibly fast for the tier and diff — minutes on a Critical PR — is the signature of rubber-stamping. The other tail matters too: chronically slow review pushes authors toward larger, batched PRs, degrading the review it delays. |
| **PR size** | Distribution of changed lines per PR, tracked over time | **Reviewer overload.** A distribution drifting upward past the review-effectiveness threshold (§6) means the process is being outrun — authors are batching because review capacity, not discipline, is the binding constraint. |
| **Merge success rate** | Fraction of PRs merged without a substantive change request or tier escalation | **Evasion.** A rate approaching 100% does not mean quality is high; it means review is exerting no pressure. Tier declarations that never get disputed and reviews that never find anything are the aggregate symptom of the collusion and mis-tiering failure modes named in §9. |
| **Change failure rate** | Fraction of merged changes that cause an incident, rollback, or hotfix | **Real-world failure.** The ground truth the other three approximate. If the first three look healthy and this one is rising, the process has decayed into ceremony regardless of what the paperwork says. **Attribution requirement:** incidents, rollbacks, and hotfixes must be linked to a causal merged PR, or logged explicitly as *unattributed*. The unattributed rate is itself a signal — see below. |
| **Unattributed incident rate** | Fraction of incidents, rollbacks, and hotfixes with no linked causal PR | **Funnel bypass or attribution failure.** A rising unattributed rate signals either that changes are bypassing the PR process entirely, or that post-merge attribution is breaking down. Both are governance findings. This metric instruments the boundary of the funnel that the other four assume is closed. |
| **Emergency-path rate** | Fraction of changes processed via §10.1 (act-first, retrospective PR) | **Pressure-evasion signal.** A rising emergency rate means the compliant path is being priced out under deadline pressure — the framework's §0 commitment ("the bar does not move with deadline pressure") is eroding. Pairs with the unattributed incident rate: together they instrument the funnel boundary. |

**The instrumentation principle:** no targets. A target on any of these metrics converts it from a detector into a thing to be gamed — the same ritual-completion failure it exists to catch, one level up. What matters is *trend and shape*: a latency distribution compressing toward zero, a size distribution drifting up, a success rate pinned at the ceiling, a failure rate diverging from the others, an unattributed rate climbing, an emergency rate rising. Each is a governance finding to be investigated under §7, not a number to be managed toward.

At S1, formal instrumentation is optional; the solo practitioner's honest equivalent is noticing when their own separate-session reviews stop producing findings, and whether incidents are being linked back to their causal changes.

### §10.1 — Emergency Change Path

The framework's writ applies to all changes that enter the PR funnel (§9, Limit #5). When a change cannot wait for its tier's review — a live production incident, a security response, a time-critical dependency — the **emergency change path** provides a governed bypass. This is not an exemption from governance; it is governance with a different sequence.

**Act first, document immediately after.**

1. **Make the change.** Apply the fix directly. No PR ceremony blocks a live incident response.
2. **Open the retrospective PR within 1 business day** (repositories may adjust this window in their CONTRIBUTING.md to match their release cadence). **The retrospective PR carries the full evidence artifact for a Critical-tier change**: verification status tags applied honestly after the fact, boundary questions answered, root cause stated if applicable. The tag set applies without modification — "Confirmed" still means verified; "Unverified" still requires a closure plan. Honest retrospective tagging is the point: the emergency path does not lower the epistemic bar, it moves it.
3. **The retrospective PR is reviewed at Critical tier** regardless of the change's nominal size. Deploy and environment configuration is a protected surface (§5); most emergency changes touch it.
4. **Log it.** The emergency-path rate (§10) is instrumented. An unreviewed retrospective PR is an open governance finding until it closes.

**What this is not:** The emergency path is not a license to bypass governance routinely. A repository where the emergency path is used frequently has a governance problem, not an emergency problem — the §10 emergency-path rate is the detector for this. It is also not a workaround for scope disagreements or deadline pressure on non-emergency work; the standard path's "bar does not move" commitment (§0) holds for everything that is not a genuine emergency.

---

## §11 — Change Control

- Amendments to this parent document are versioned (v0.2, v0.3, …; patch versions for non-structural passes) with a dated changelog entry stating what changed and which deployment or analysis surfaced the need.
- Locked versions are not modified; queued improvements accumulate to the next version.
- Derivative-surfaced amendments credit the *class* of deployment (e.g., "surfaced by an S3 agency deployment"), never the context itself, per the context-separation rule.
- No amendment may violate the progressive-disclosure constraint (§0).

---

*Companion files: `QUICKSTART.md` (contributor path, required reading, 90 seconds) · `PULL_REQUEST_TEMPLATE.md` (the instrument) · `LINEAGE.md` (design rationale and term origins — optional context, never required reading).*

*J. Wright · UX Minds, LLC · AI-assisted (Claude / Anthropic)*
