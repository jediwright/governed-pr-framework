# Design Notes & Lineage

*Optional reading. Nothing in the PR process depends on this document — it exists for people who want to know **why** the framework is built the way it is, and where its mechanisms come from. If you're just here to submit a PR, `QUICKSTART.md` is all you need.*

**Framework:** The Governed Pull Request Framework v0.3
**Author:** J. Wright · UX Minds, LLC · [jediwright.com](https://www.jediwright.com)
**Status of this file:** Parent-only artifact. Derivative deployments carry a one-line attribution and do not ship this document.

---

## Why tiers are based on propagation, not size

Most review processes scale rigor by diff size. This framework scales it by **blast radius** — how far a failure would spread, and whether it would spread *visibly*.

The model comes from the author's [Tiered Content Framework](https://www.jediwright.com/content-strategy-framework) (TCF), a content-governance architecture that extends Atomic Design into the semantic layer. Its core rule: **govern at the lowest tier possible** — get the smallest unit right and everything built from it inherits the fix; let a defect propagate upward and you're correcting it everywhere instead of once. Applied to code changes, that rule produces the Low-risk / Feature / Critical tiering, and explains the counterintuitive consequence the quick start flags: a one-line schema change is Critical and a 300-line test file is Low-risk, because tier tracks propagation, not effort.

The same source explains the **mechanized layer** (§6 of the framework). The TCF distinguishes content from the *conditions under which content is valid* — constraints that are invisible in the final product but load-bearing everywhere downstream. In PR practice those are your lint rules, commit formats, dependency classifications, and required patterns: exactly the class of rule humans skip under pressure, and exactly what belongs in tooling rather than on a human checklist.

## Why claims carry verification tags

The Confirmed / Inferred / Unverified / Time-sensitive tag set adapts an **epistemic status schema** developed for the TCF's machine-legibility work — a field-level discipline for declaring how much trust a statement has earned, rather than letting confident prose stand in for evidence.

Two additions matter in the PR context:

- **The closure-plan requirement on Unverified.** An honest uncertainty flag with no plan to resolve it isn't disclosure — it's an exemption stamp. Requiring "what will be observed, by when" turns the tag into a closed loop (the build–measure–learn discipline from Lean practice).
- **The decay rule.** Evidence is point-in-time: "Confirmed" is confirmed *against something* — a dependency version, an environment — and rots silently when that referent changes. This mirrors the evidence-decay logic in the author's broader governance work, where any claim's verification is understood to have a shelf life unless its expiry condition is declared.

**On precedent and composition.** The components of this tag system have precedents in free practice under other names. GitHub branch protection's "dismiss stale pull request approvals when new commits are pushed" and Gerrit's vote-reset-on-new-patchset are the decay mechanism — evidence invalidated by a base-state change, re-verification before merge — shipped as stock behavior in default PR tooling. Gerrit's label vocabulary (Verified / Code-Review) and the Linux kernel's trailer conventions (Tested-by / Reviewed-by / Acked-by) are graduated attestation vocabularies whose values gate acceptance. The GSN Community Standard (Goal Structuring Notation, used in safety-critical engineering) expresses per-claim epistemic status — supported / undeveloped / assumed / justified — where admissibility is blocked while claims remain undeveloped and evidence-currency obligations apply; this is per-claim status with consequences and a shelf life, in the wild and freely published. Rust's `// SAFETY:` justification convention, enforced by clippy's `undocumented_unsafe_blocks` lint, is per-claim justification with a mechanical admissibility gate.

What this framework contributes is a **composed instrument**: author-side per-claim tags, closure-plan-or-blocked, decay/staleness, and K4 admissibility coupling — assembled into a lightweight PR template for general software development, a context none of the above were designed for. The novelty is compositional, not mechanistic. Two frameworks arriving at the same structure from different directions is treated as validation of the logic, not as undifferentiated precedent.

## Why the checklist is so short

The template's restraint is deliberate and research-backed. Aviation and surgical checklist studies (popularized by Atul Gawande's *The Checklist Manifesto*) converge on the same findings: effective checklists are short — roughly five to nine items per pause point — contain only items whose omission causes disasters *and* which get skipped under pressure, and fire at defined moments rather than continuously. Past that threshold, completion becomes ritual and the checklist trains the very inattention it was meant to prevent.

An earlier draft of this framework accumulated fifteen-plus fields. The stress test that produced v0.1 cut it back using a principle from the author's generative-governance work: **apply governance where decisions propagate silently if wrong — not everywhere.** That principle, not minimalism for its own sake, decides what survives at each tier.

## Why review must happen outside the authoring context

K2 — no PR approved by the session, person, or context that produced it — generalizes a rule learned expensively in the author's AI-assisted build practice: *review conducted in the same session that generated the code is not review; it is proofreading.* The author who wrote the code (human or AI) cannot independently audit it against a specification they also hold in working memory. The framework's scale gates exist largely to answer what "outside the authoring context" means honestly at each team size — including the admission (§9 of the framework) that a solo practitioner's separate-session review is the weakest form, compensated by external verification rather than papered over.

The **pre-mortem** — "it's two weeks from now and this PR caused an incident; what was it?" — is Gary Klein's decision-research technique, kept as the single open-ended adversarial item precisely because fixed failure-mode lists can't enumerate what they haven't seen.

The **reviewer-scope lines** at organizational scale ("Approved: X. Not evaluated: Y.") address a failure the author's multi-model evaluation work names precisely: false consensus — one reviewer's partial confidence laundered into total sign-off. Scoped approval is the review-side twin of the author-side verification tags: both make the *shape* of confidence visible instead of flattening it to a binary.

## Why deleted code needs a biography

The deletion-justification rule is Chesterton's Fence, operationalized: code may not be removed until the PR states why it existed. The addition here is what happens when nobody knows — that's recorded as a documentation gap (feeding the self-healing conventions rule), not treated as permission to delete. A convention nobody wrote down is the framework's problem to fix, not the code's fault for existing.

## Why the framework has a parent and derivatives

The inheritance protocol (§8) — a public parent, context-specific governed derivatives, a two-way contribution channel, and a strict rule that derivative-local content never flows upstream — follows the versioning and inheritance model the author developed for the TCF and its own derivative frameworks, and reflects the publication discipline of the author's [Pattern Commons](https://www.jediwright.com) series: reusable governance patterns published as versioned, amendable public artifacts, with locked versions never modified and improvements queued to the next release.

The same body of work supplies the framework's third framing of what a PR *is*: not just a change and a review request, but an **evidence artifact** — part of the permanent record from which future contributors, auditors, and automated systems reconstruct why a system is the way it is. At public scale, the PR history is an exhibit. The framework asks you to write for that reader.

## Sources outside the author's work

- **Empirical code-review research** (industry studies): defect detection collapses past roughly 200–400 changed lines; review *latency* shapes author behavior more than review rigor — slow reviews produce bigger PRs, which produce worse reviews. These findings set the diff-size advisory and the staleness window.
- **ITIL 4 Change Enablement:** cited as a convergence, not a source. The framework's propagation-based tiering was derived from blast-radius reasoning (see the TCF notes above) and then found to independently re-derive ITIL's Standard / Normal / Emergency change classification — and its underlying rationale: *the process must match the risk in front of it*. Two frameworks arriving at the same structure from opposite directions — content governance and AI-assisted build practice on one side, enterprise incident management on the other — is treated as validation of the logic, not as lineage. One concept is imported deliberately: the v0.2 pre-cleared change classes (§2.3) adopt ITIL's Standard-change mechanism — notably the one piece of ITIL that DevOps and continuous-deployment practice retained, because it is how automated pipelines coexist with change control at all. Nothing else crosses over: none of ITIL's process weight, service-management vocabulary, or change-board machinery appears anywhere in this framework, and no ITIL term appears in any contributor-facing file.
- **Agile/Lean practice:** Definition of Done (a fixed bar for "done" that deadline pressure cannot move); stop-the-line authority (any contributor may block, exercising it is never penalized); dual-track separation (discovery decisions do not get made silently inside delivery work — the materiality threshold for decision records).
- **Open-source convention:** structured commit messages, lightweight architecture decision records, feature-flag shippability, and the maintainer model at public scale.
- **PRD/BRD practice:** explicit out-of-scope declarations and requirement traceability, consolidated here into the single "Not in this PR" field and the fidelity-source line.

---

## The broader body of work

This framework is one instrument in a connected portfolio on governance — of content, of AI-assisted work, and of the infrastructure people depend on:

- **The Tiered Content Framework** — content governance from the field level to the enterprise level; the structural parent of this framework's tiering and mechanization logic. [jediwright.com/content-strategy-framework](https://www.jediwright.com/content-strategy-framework)
- **The Pattern Commons series** — reusable, versioned governance patterns extracted from working prototypes.
- **Writing on AI governance and worker data sovereignty** — the argument that the governance infrastructure institutions built for themselves should exist on the worker's side of the seam, backed by working local-first prototypes.

All at [jediwright.com](https://www.jediwright.com) and [systemsofthought.com](https://www.systemsofthought.com).

---

*J. Wright · UX Minds, LLC · AI-assisted (Claude / Anthropic)*
